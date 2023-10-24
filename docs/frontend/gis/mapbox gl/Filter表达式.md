# mapbox使用filter方法过滤地图——expression表达式语法注意事项

# 写在前面

mapbox的filter方法可以根据地图上每个feature的特定属性，过滤出符合条件的feature进行显示，是非常实用的一种方法。

但是在使用时，我们通常使用的是`基于属性的filter语法`（官网的示例也只使用了filter表达式），这种语法不够灵活，最为突出的问题在于，filter语法是根据`全等于`的标准进行过滤的，也就是必须类型相同数值相同能显示出来，而实际应用时常常需要进行类型转换，这是filter语法不支持的。

新版本里已经可以用`expression`表达式语法完全替代filter语法，因此我们可以使用expression进行更加灵活的操作，本文旨在介绍expression表达式语法设置filter的注意事项。
该注意事项可以解决报错`"Error: layers.counties-highlighted.filter[1][1]: string expected, array found"`，并且常见的`组合过滤器`报错或不生效问题也大都由`expression`表达式语法使用不当，忽视该注意事项造成的。

# filter官方文档

[docs.mapbox.com/help/glossa…](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.mapbox.com%2Fhelp%2Fglossary%2Ffilter%2F)

# 基于属性的filter语法（property-based filter syntax）

**老版本只能使用filter语法，不支持expression语法。**
若出现报错`expected one of [==, !=, >, >=, <, <=, in, !in, all, any, none, has, !has] `则可能是因为使用的mapbox版本过低，只支持filter语法，不支持expression语法导致。
文档中的`key`必须是字符串类型，也就是feature的属性名，不能写为表达式。
官方文档：[docs.mapbox.com/mapbox-gl-j…](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.mapbox.com%2Fmapbox-gl-js%2Fstyle-spec%2Fother%2F%23other-filter) ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/65a2c935479142969a59a20a430b9a39~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

# expression官方文档

即平时最常使用的表达式，但在设置filter时，filter语法的文档警告[Other filter](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.mapbox.com%2Fmapbox-gl-js%2Fstyle-spec%2Fother%2F%23other-filter)，强调了`只能使用expression或property-based filter syntax的一种，不能混用`。
[docs.mapbox.com/mapbox-gl-j…](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.mapbox.com%2Fmapbox-gl-js%2Fstyle-spec%2Fexpressions%2F)

# 以官网示例做说明：

链接：[docs.mapbox.com/mapbox-gl-j…](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.mapbox.com%2Fmapbox-gl-js%2Fexample%2Fqueryrenderedfeatures-around-point%2F)
在该示例中filter使用两次，如下：

```js
js复制代码// 在添加地图的时候定义filter
map.addLayer(
{
'id': 'counties-highlighted',
'type': 'fill',
'source': 'counties',
'source-layer': 'original',
'paint': {
'fill-outline-color': '#484896',
'fill-color': '#6e599f',
'fill-opacity': 0.75
},
'filter': ['in', 'FIPS', '']
},

// 在点击地图时设置filter
map.setFilter('counties-highlighted', ['in', 'FIPS', ...fips]);
```

**上述写法属于基于属性的filter语法，下面介绍expression写法：**

```js
js复制代码'filter': ['in', ['get', 'FIPS'], ['literal', []]]

map.setFilter('counties-highlighted', ['in', ['get', 'FIPS'], ['literal', fips]]);
```

参考[Type system](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.mapbox.com%2Fmapbox-gl-js%2Fstyle-spec%2Fexpressions%2F%23type-system) 必须使用`literal`说明`fips`为数组类型，而不是表达式。

示例中地图中feature的FIPS属性为数字类型，fips也是数字数组，若FIPS属性为字符串类型而fips是数字数组，则可以使用`to-number`进行`类型转换`：

```js
js复制代码map.setFilter('counties-highlighted', 
  ['in', ['to-number',['get', 'FIPS']], ["literal", fips]]);
```

# 解决报错`"Error: layers.counties-highlighted.filter[1][1]: string expected, array found"`

`再次强调，只能使用expression或property-based filter syntax的一种!` 混用则会导致报错！

```js
js复制代码// 错误写法：
map.setFilter("counties-highlighted", 
  ['all', 
    ["in", ['to-number',["get", 'FIPS']], ["literal", fips]], // expression
    ['in', 'FIPS', ...fips]，// property-based filter syntax
  ]);
```

**上述错误写法的报错原因：**
混用两种语法，会认为整个表达式都是filter语法即property-based filter syntax，并且无法解析。那么key必须是属性`'FIPS'`（string），而不是表达式`['to-number',["get", 'FIPS']]`，并且会将这个表达式认为数组类型（array）；
当遇到`"Error: layers.counties-highlighted.filter[1][1]: string expected, array found"`一定要检查是否将filter语法和expression语法混用！ ![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/519713887cf84aebb451f53dcbf660b3~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

```js
js复制代码//正确写法1
map.setFilter("counties-highlighted", 
  ['all', 
    ["in", ['to-number',["get", 'FIPS']], ["literal", fips]], // expression
    ["in", ["get", 'FIPS'], ["literal", fips]], // expression
  ]);
 //正确写法2
map.setFilter("counties-highlighted", 
  ['all', 
    ['in', 'FIPS', ...fips]，// property-based filter syntax
    ['!in', 'FIPS', ...[]], // property-based filter syntax
  ]);
```

## 几个特殊的filter语法

官网中共给出了13个filter语法的，其中10个都可以写成expression，如：

```js
js复制代码// property-based filter syntax
["in", key, v0, ..., vn]
// expression
["in",
    keyword: InputType (boolean, string, or number),
    input: InputType (array or string)
]: boolean
```

因此`['in', 'FIPS', ...fips]`可以写成`['in', ['get', 'FIPS'], ['literal', fips]]`

**但是下面三个只能使用filter语法，没有对应的expression表达式：**

```js
js复制代码["!has", `key`]   
["!=", `key`, `value`]   
["none", `f0`, ..., `fn`]  
```

也就是当使用`!has`,`!=`,`none`时，不能与使用任何expression表达式进行`组合过滤`！
当然，可以用expression中的`!`与`has`或`in`组合使用去表示filter语法：

```js
js
复制代码["!", boolean]: boolean   
```

例如`['!in', 'FIPS', ...fips]`可以写成`['!', ["in", ["get", 'FIPS'], ["literal", fips]]]`
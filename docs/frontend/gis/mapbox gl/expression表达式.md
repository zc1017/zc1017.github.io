# MapboxGL中的Expressions表达式

> 表达式（expressions)是Mapbox GL JS的一个高级功能，它为数据的添加和渲染展示提供了更多的灵活性。

### expression

任何layout、paint或者filter的值都可以用一个expression表达式来细化，一个expression表达式定义了用如下计算器计算属性值的公式。
Mapbox gl提供的表达式计算器有如下：

- **Mathematical operators**（数学 运算）：数学计算器用于数值计算和其他数值相关的属性
- **Logical operators**（逻辑 运算）：逻辑计算器用于计算布尔值和做条件决策
- **String operators**（字符串 运算）：字符计算器用于计算字符串
- **Data operators**（数据 运算）：提供调用数据源要素集属性的接口
- **Camera operators**（相机 运算）：提供定义当前地图视角参数的接口

### 语法



```json
[expression_name, argument_0, argument_1, ...]
```

expression_name是表达式运算符，后面跟着参与运算的多个参数，支持嵌套使用

### 所有支持的运算符



```go
// prettier-ignore
type ExpressionName =
    // Types
    | 'array' | 'boolean' | 'collator' | 'format' | 'literal' | 'number' | 'object' | 'string'
    | 'to-boolean' | 'to-color' | 'to-number' | 'to-string' | 'typeof'
    // Feature data
    | 'feature-state' | 'geometry-type' | 'id' | 'line-progress' | 'properties'
    // Lookup
    | 'at' | 'get' | 'has' | 'length'
    // Decision
    | '!' | '!=' | '<' | '<=' | '==' | '>' | '>=' | 'all' | 'any'
    | 'case' | 'match' | 'coalesce'
    // Ramps, scales, curves
    | 'interpolate' | 'interpolate-hcl' | 'interpolate-lab' | 'step'
    // Variable binding
    | 'let' | 'var'
    // String
    | 'concat' | 'downcase' | 'is-supported-script' | 'resolved-locale' | 'upcase'
    // Color
    | 'rgb' | 'rgba'
    // Math
    | '-' | '*' | '/' | '%' | '^' | '+' 
    | 'abs' | 'acos' | 'asin' | 'atan' | 'ceil' | 'cos' | 'e'
    | 'floor' | 'ln' | 'ln2' | 'log10' | 'log2' | 'max' | 'min' | 'pi' 
    | 'round' | 'sin' | 'sqrt' | 'tan'
    // Zoom, Heatmap
    | 'zoom' | 'heatmap-density';
```

### 示例

数学运算，计算（π* 3^ 2）也就是π乘以3的2次方



```json
['*', ['pi'], ['^', 3, 2]]
```

**get**，用于在数据源中读取属性的值，常嵌套在其他表达式中使用



```json
["get", "value"]
```

逻辑运算，常在过滤器中使用，筛选FID值大于50000的要素,
`number`用来转换格式，第二个参数为当第一个参数转换失败时采用的默认值



```json
{
    "filter":['>',['number',['get','FID'],0],50000]
}
```

**interpolate**，内插，采用线性算法，结合`zoom`级别，指定不同级别下的平滑半径
5级下半径为1，10级下半径为5，其它级别做线性插值



```json
{
    "circle-radius": [
        "interpolate", 
        ["linear"], ["zoom"], 
        5, 1, 
        10, 5
    ]
}
```

**step**，分级



```css
{
    circleColor: [
      'step',
      ['get', 'value'],
      '#51bbd6',
      50,
      '#f1f075',
      100,
      '#f28cb1'
    ],
}
```

**match**，匹配



```dart
{
    'circle-color': [
      'match',
      ['get', 'ethnicity'],
      'White', '#fbb03b',
      'Black', '#223b53',
      'Hispanic', '#e55e5e',
      'Asian', '#3bb2d0',
        /* other */ '#ccc'
    ]
}
```
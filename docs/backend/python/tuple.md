```python
# 元组tuple和列表list类似,有序，可以存放多种不同类型数据
# 区别在于列表可变，元组不可变,元组的元素不能修改

a=('a','b','c',1,2,3,[1,2,3])
print(a[5])
print(a[6][1])
print(type(a))
#a[1]=1 #元组不可变，报错

#列表的方法基本和元组相同

print(len(a))

print(a[1:5])
print(a.count('a'))

#拼接
b=('a','b','c')
print(a+b)
#元组不可变，因此 append ，extend(),pop(),remove()方法不可用

#元组深层次元素可变
a[6][1]='hello'
print(a)


a=("h","123","h")
print(max(a))
print(min(a))
print(len(a))
c="12345哈hahahah"
print(max(c))
print(min(c))
print(len(c))





```


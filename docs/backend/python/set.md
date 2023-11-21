```python
# 集合无序，唯一的
# 无序：不可用下标来取值
# 唯一：可以去重+-

#创建集合

#set()方式创建 ，里面可以是列表，元组，字典，字符串
set1=set([1,2,3,4,5,6])
print(set1) #{1, 2, 3, 4, 5, 6}
set1=set((1,2,3,4,5,6))
print(set1) #{1, 2, 3, 4, 5, 6}
set1=set({1:2,3:4,5:6})
print(set1) #{1,  3,  5}
set1=set('12345')
print(set1) #{'2', '4', '1', '3', '5'}

# {}方式创建，里面可以是数字，字符串，元组

set1 ={1,2,3,'123',(1,2,3)}
print(set1)

#set1 ={1,2,3,'123',[1,2,3]}   {}方式放集合会报错



#列表去重
list1=[1,2,3,4,5,6,1,2,3]
set1=set(list1)
print(set1) #{1, 2, 3, 4, 5, 6}

#元组去重
tuple1=(1,2,3,4,5,6,1,2,3)
set1=set(tuple1)
print(set1) #{1, 2, 3, 4, 5, 6}

#集合添加元素 add
set1.add(7)
print(set1) #{1, 2, 3, 4, 5, 6, 7}

# update 可以添加多个元素
set1.update([8,9,10])
print(set1) #{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

# 删除元素
set1.remove(10)
print(set1) #{1, 2, 3, 4, 5, 6, 7, 8, 9}
# set1.remove(11) #报错
# pop删除 随机：集合无序，pop删除是随机删除一个元素
set1.pop()
print(set1) 
#discard删除  和remove删除类似，也是删除元素，但是删除不存在的元素时不会报错
set1.discard(1)
print(set1) 
set1.discard(11)


#集合交集，并集，差集
set1={1,2,3,4,5,6}
set2={4,5,6,7,8,9}
# 交集
set3=set1 & set2
print(set3) #{4, 5, 6}
# 并集
set3=set1 | set2
print(set3) #{1, 2, 3, 4, 5, 6, 7, 8, 9}
# 差集
set3=set1 - set2
print(set3) #{1, 2, 3}





```


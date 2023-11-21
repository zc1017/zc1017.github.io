```python
# 列表有序，值可以改变，值可以重复
aa = ['1', 78, '2', '3', [1, 2, 3]]
print(aa[4][1])
print(len(aa))
aa[0] = 678
print(aa)

# 列表相加
list1 = [1, 2, 3]
list2 = [4, 5, 6]

print(list1+list2)
# 列表相乘
print(list1*3)

print('这是一个测试'*5)

#列表切片

list3=[1,2,3,4,5,6,7,8,9]
print(list3[0:3])
print(list3[-3:-1])
print(list3[-3:])
print(list3[::-1])

print(list3[::2])

#列表删除
#del 删除元素

list4 = [1, 2, 3, 4, 5, 6]
del list4[0]
print(list4)
#append
list4.append(7)
print(list4)

#insert

list5=["a","b","c"]
list5.insert(1,'test')
print(list5)
list5.insert(1,['test2','test3'])
print(list5)
#clear
#list5.clear()
print(list5)

#remove
list5.remove('test')
print(list5)

#pop
print(list5.pop(1))
print(list5)

print(list5.pop())
print(list5)


#index 
list6=['a','b','c','a','b','c','a','b','c']
#print(list6.index('bb'))
print(list6.index('b'))
print(list6.index('b',2,8))
#reverse
list6.reverse()
print(list6)

#extend 添加列表

list7=[1,2,3]
list7.extend([4,5,6])
list7.append([7,8,9])
print(list7)


#copy 
a=[1,2,3]
b=a.copy()
del a[0]
print(b)

# sort ASCII码 0-9<A-Z<a-z
a=["hello","world","hw","bug",'1','额']
a.sort()
print(a)
a.sort(reverse=True)
print(a)

#count
a=["hello","world","hw","bug",'1','额']
print(a.count('1'))



```


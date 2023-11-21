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

```


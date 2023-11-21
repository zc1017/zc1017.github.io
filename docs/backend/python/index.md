```python
import keyword
print(keyword.kwlist)
a = 1
b = 2
c = 3
d = """这是一个测试代码
呀呀呀啊呀呀"""
print(d)


print(a, b, c, d)
# e=input()
# print(e)
print("hello\tworld")
print("hello\rworld")
print("hello\bworld")
print(r"\r")
print(R"\r")
# 定义常量
PI = 3.14
print(PI)
PI = 1
print(PI)
print(2/4)
print(3/7)
print(7//3)
print(2**2)
print(2**2**2)
print(True == 1)
print(False == 0)
print(type(True) == type(1))
print(type(1))
print(type(1.1))
print(int(5.2))
print(type(1) or type(2.1))


aa = None
print(type(aa))

bb = "这是一个测试字符串测试这是一个"
print(bb[0])
print(bb[0:3])
print(bb[1:])
print(bb[0::2])
print(bb[::-1])


print(bb.find("测试"))
print(bb.find("测试", 6, 15))
print(bb[4])
print(bb.count('测试'))
print(bb.count('测试', 6, 15))

cc = 'This is a test,please check it'
dd =cc.replace('i', 'h')
print(cc)
print(dd)
ee =cc.replace('i', 'a',1)
print(ee)
print(cc.replace('i', 'a',2))
print(cc.upper())
print(cc.lower())

print('这是一个{},请输入{}'.format('测试',0))

ff=cc.split(' ')
print(ff)
print(','.join(ff))


ee=' 444zhe shi yi ge ce shi   4444     '
print(ee.strip())
ii='zhe shi yi ge ce shi'
print(ii.strip('4'))


print('我是%s'%('测试'))
print('测速度是%.2f'%(100.2345))
print('这是一个{},请输入{}'.format('测试',0))
aa = '你好' 
bb=12
print(f'这是一个{aa},请输入{bb}')

print(len(aa))

```


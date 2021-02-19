---
layout: post
author: 张开祥
biaoti: 关于类和实例的一些理解
---

# 关于类和实例的一些理解


关于面向对象程序设计内容的学习，有一些东西很困惑，读书的时候也是一带而过。有些东西是在碰到了困惑的时候，回头思考才有的一些理解。可能这也是学习过程中的常见现象。关于类和实例的一些困惑，在此作一些梳理，防止日后又记不清了。


```python
class First:
    def __init__(self):
        self.atti1 = 'first_class_attri1'
        
x = First()

print('First.__dict__内容为: ',Fisrt.__dict__)
print('*'*60)
print('x.__dict__的内容为：',x.__dict__)
```

    First.__dict__内容为:  {'__module__': '__main__', '__init__': <function Fisrt.__init__ at 0x000001E739B4BCA0>, '__dict__': <attribute '__dict__' of 'Fisrt' objects>, '__weakref__': <attribute '__weakref__' of 'Fisrt' objects>, '__doc__': None}
    ************************************************************
    x.__dict__的内容为： {'atti1': 'first_class_attri1'}



```python
以上内容说明，一个对象和一个实例的__dict__是不一样的。实例的__dict__好像少很多。
```


```python
class First:
    def __init__(self):
        self.name = 'firstclass'
    def read(self):
        print(self.__dict__)

class Second(First):
    def __init__(self):
        self.name = "secondclass"

f = First()
s = Second()


First.read(First)
First.read(Second)

First.read(f)
First.read(s)

f.read()
s.read()
```

    {'__module__': '__main__', '__init__': <function First.__init__ at 0x000001E739C1E8B0>, 'read': <function First.read at 0x000001E739C1EAF0>, '__dict__': <attribute '__dict__' of 'First' objects>, '__weakref__': <attribute '__weakref__' of 'First' objects>, '__doc__': None}
    {'__module__': '__main__', '__init__': <function Second.__init__ at 0x000001E739C1E820>, '__doc__': None}
    {'name': 'firstclass'}
    {'name': 'secondclass'}
    {'name': 'firstclass'}
    {'name': 'secondclass'}


上面的例子定义了两个类，First和Second类。可以通过instance.method的方式来调用方法，也可以通过class.method(object)的方式来调用。仔细体会一下，慢慢阅读和思考上面的例子有利于理解。其实instance.method是隐含地转换为class.method(instance)的。


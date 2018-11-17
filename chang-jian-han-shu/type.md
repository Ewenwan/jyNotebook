### 简述

type\(\) 函数如果你只有第一个参数则返回对象的类型，三个参数返回新的类型对象

### 语法

```
 |  type(object_or_name, bases, dict)
 |  type(object) -> the object's type
 |  type(name, bases, dict) -> a new type
```

#### 参数

* name:类的名称。

* bases:基类的元组。

* dict:字典，类内定义的命名空间变量。

### 返回值

一个参数返回对象类型, 三个参数，返回新的类型对象

### 实例

```
>>> type(1)
<class 'int'>
>>> type('name')
<class 'str'>


# 三个参数

>>> class Person(object):
...     num = 1
...
>>> person = type('person',(object,),dict(num=1))
>>> person
<class '__main__.person'>
>>> person.num
1
```

> 温馨提示
>
> isinstance\(\) 与 type\(\) 区别：
>
> * type\(\) 不会认为子类是一种父类类型，不考虑继承关系。
>
> * isinstance\(\) 会认为子类是一种父类类型，考虑继承关系。
>
> 如果要判断两个类型是否相同推荐使用 isinstance\(\)。




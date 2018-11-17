### 简述

sorted\(\)函数从_iterable中_的项返回一个新的排序列表

### 语法

```
sorted（iterable，*，key = None，reverse = False ）
```

#### 参数

* iterable -- 可迭代对象。

* key指定一个参数的函数，用于从每个列表元素中提取比较键：key=str.lower。默认值为None （直接比较元素）。

* reverse是一个布尔值。如果设置为True，则对列表元素进行排序，并且反转

### 返回值

一个参数返回对象类型, 三个参数，返回新的类型对象

### 实例

```
>>> a = [5,6,7,3,6]
>>> a
[5, 6, 7, 3, 6]
>>> sorted(a)
[3, 5, 6, 6, 7]
>>> sorted(a,reverse=True) # 反转
[7, 6, 6, 5, 3]
>>> a.sort() # 注意sort只为list定义，而sorted()函数可以接收任何的iterable
>>> a        
[3, 5, 6, 6, 7]

>>> test = [4,3,8,7,6,1,0,2]
>>> test
[4, 3, 8, 7, 6, 1, 0, 2]

# 利用key进行排序
>>> result = sorted(test,key=lambda x:x)
>>> result
[0, 1, 2, 3, 4, 6, 7, 8]
>>> result = sorted(test,key=lambda x:-x)
>>> result
[8, 7, 6, 4, 3, 2, 1, 0]
```

> 温馨提示
>
> **sort 与 sorted 区别：**
>
> sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。
>
> list 的 sort 方法返回的是对已经存在的列表进行操作，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。




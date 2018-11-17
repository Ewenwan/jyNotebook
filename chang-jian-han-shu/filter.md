### 简述

filter\(\)函数用于过滤序列，过滤掉不符合条件的元素，返回一个迭代器，产生可迭代对象，如果转换为列表，需要使用list\(\)。

该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判，然后返回 True 或 False，最后将返回 True 的元素放到新列表中。是真的。 如果function为None，则返回true的项。

### 语法

```
filter（function or None，iterable） - > filter对象
```

#### 参数

* function:函数
* iterable:可迭代的对象

### 返回值

返回一个可迭代对象

### 实例

```
>>> def isOdd(n):
...     return n%2 == 1
...
>>> test = filter(isOdd,[1,2,3,4,5,6,7])
>>> new_test = list(test)
>>> new_test
[1, 3, 5, 7]
```






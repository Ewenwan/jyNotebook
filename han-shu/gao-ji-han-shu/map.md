### 简述

map\(\) 会根据提供的函数对指定序列做映射。

第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

### 语法

```
map(func, *iterables)
```

#### 参数

* function:函数
* iterable:一个或多个序列

### 返回值

返回迭代器

### 实例

```
>>> def func(x):
...     return x*2
...
>>> map(func,[1,2,3,4,5])
<map object at 0x000001B76E4DABA8>
>>> list(map(func,[1,2,3,4,5]))
[2, 4, 6, 8, 10]
```




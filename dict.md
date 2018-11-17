### 语法

```
dict(**kwarg)
dict(mapping, **kwarg)
dict(iterable, **kwarg)
```

### 作用

创建一个字典

### 参数

* \*\*kwargs:关键字

* mapping:元素的容器。

* iterable:可迭代对象。

### 实例

```
>>>dict()                        # 创建空字典
{}
>>> dict(a='a', b='b', t='t')     # 传入关键字
{'a': 'a', 'b': 'b', 't': 't'}
>>> dict(zip(['one', 'two', 'three'], [1, 2, 3]))   # 映射函数方式来构造字典
{'three': 3, 'two': 2, 'one': 1} 
>>> dict([('one', 1), ('two', 2), ('three', 3)])    # 可迭代对象方式来构造字典
{'three': 3, 'two': 2, 'one': 1}
```




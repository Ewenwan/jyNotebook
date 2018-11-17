### 语法

```
frozenset([iterable])
```

### 作用

返回一个冻结的集合，冻结后集合不能再添加或删除任何元素

### 参数

* iterable: 可迭代的对象，比如列表、字典、元组等等

### 实例

```
>>>a = frozenset(range(10))     # 生成一个新的不可变集合
>>> a
frozenset([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> b = frozenset('runoob') 
>>> b
frozenset(['b', 'r', 'u', 'o', 'n'])   # 创建不可变集合
```




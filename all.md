### 语法

```
all(iterable)
```

### 作用

用于判断给定的可迭代参数 iterable 中的所有元素是否都为 TRUE，如果是返回 True，否则返回 False。元素除了是 0、空、FALSE 外都算 TRUE

### 参数

* iterable:元组或列表

### 实例

```
>>> all([1,2,3,""])
False
>>> all(['1'])
True
```




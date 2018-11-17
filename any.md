### 语法

```
any(iterable)
```

### 作用

用于判断给定的可迭代参数 iterable 是否全部为 False，则返回 False，如果有一个为 True，则返回 True。元素除了是 0、空、FALSE 外都算 TRUE

### 参数

* iterable:元组或列表

### 实例

```
>>> any([1,2,''])
True
>>> any([])
False
```




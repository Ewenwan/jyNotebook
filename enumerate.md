### 语法

```
enumerate(sequence, [start=0])
```

### 作用

于将一个可遍历的数据对象\(如列表、元组或字符串\)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中

### 参数

* sequence:一个序列、迭代器或其他支持迭代对象。

* start:下标起始位置。

### 实例

```
>>> a = ["a","b","c","d"]
>>> list(enumerate(a))
[(0, 'a'), (1, 'b'), (2, 'c'), (3, 'd')]
>>> list(enumerate(a,start=2))
[(2, 'a'), (3, 'b'), (4, 'c'), (5, 'd')]


>>> for i,element in enumerate(a):
...     print(i,element)
...
0 a
1 b
2 c
3 d
```




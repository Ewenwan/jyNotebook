### 语法

```
reversed(seq)
```

### 作用

反转的迭代器，即将序列反转

### 参数

* seq: 要转换的序列，可以是 tuple, string, list 或 range

### 实例

```
>>> a = "hello"
>>> list(reversed(a))
['o', 'l', 'l', 'e', 'h']

>>> b = ('h','e','l','l','o')
>>> list(reversed(b))
['o', 'l', 'l', 'e', 'h']

>>> c = ['h','e','l','l','o']
>>> list(reversed(c))
['o', 'l', 'l', 'e', 'h']

>>> d = range(5,9)
>>> list(reversed(d))
[8, 7, 6, 5]
```




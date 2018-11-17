### 语法

```
str.partition(seq)
```

### 作用

在第一次出现sep时拆分字符串，并返回包含分隔符之前的部分的3元组，分隔符本身以及分隔符之后的部分。如果找不到分隔符，则返回包含字符串本身的3元组，后跟两个空字符串

### 参数

* seq: 指定的分隔符。

### 实例

```
>>> str = "www.python.org"
>>> str.partition(".")
('www', '.', 'python.org')
>>> str.partition(",")
('www.python.org', '', '')
```




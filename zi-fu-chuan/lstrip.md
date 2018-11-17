### 语法

```
str.lstrip([chars])
```

### 作用

截掉字符串左边的空格或指定字符

### 参数

* chars:指定截取的字符或者字符串，默认为空格

### 实例

```
>>> str = "   HelloWorld"
>>> str.lstrip()
'HelloWorld'

>>> str = "********HelloWorld"
>>> str.lstrip("**")
'HelloWorld'

>>> str = "=-=-HelloWorld"
>>> str.lstrip("=-")
'HelloWorld'
```




### 语法

```
str.rsplit(sep = None)
```

### 作用

删除字符串字符串末尾的空格

### 参数

* chars -- 指定删除的字符（默认为空格）

### 实例

```
>>> str = "HelloWorld   "
>>> str.rstrip("")
'HelloWorld   '

>>> str.rstrip(" ")
'HelloWorld'

>>> str.rstrip()
'HelloWorld'

>>> str = "HelloWorld******"
>>> str.rstrip("*")
'HelloWorld'
```




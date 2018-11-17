### 语法

```
str.zfill(width)
```

### 作用

将长度为 width 的字符串，进行原字符串右对齐，并且前面填充0

### 参数

* width:指定字符串的长度。原字符串右对齐，前面填充0

### 实例

```
>>> str = "HelloWorld"
>>> str.zfill(20)
'0000000000HelloWorld'
```




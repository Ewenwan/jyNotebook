### 语法

```
str.center(width[,fillchar])
```

### 作用

为字符串指定宽度为 width并且 居中，fillchar 为填充的字符，默认为空格。

### 参数

* width:字符串的总宽度
* fillchar:填充字符

### 实例

```
>>> str = "abc"
>>> str.center(20)
'        abc         '
>>> str.center(20,'a')
'aaaaaaaaabcaaaaaaaaa'
>>> str.center(20,'*')
'********abc*********'
```




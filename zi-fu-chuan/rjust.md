### 语法

```
str.rjust(width[, fillchar])
```

### 作用

* width -- 指定填充指定字符后中字符串的总长度.

* fillchar -- 填充的字符，默认为空格。

### 实例

```
>>> str = "Hello World"
>>> str.rjust(50)
'                                       Hello World'
>>> str.rjust(50,"*")
'***************************************Hello World'
```




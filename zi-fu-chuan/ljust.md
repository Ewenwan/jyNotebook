### 语法

```
str.ljust(width[, fillchar])
```

### 作用

返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格。

### 参数

* width -- 指定字符串长度。

* fillchar -- 填充字符，默认为空格。

### 实例

```
>>> str = "Hello World"
>>> str.ljust(50,'-')
'Hello World---------------------------------------'
```




### 语法

```
str.endswith(suffix[, start[, end]])
```

### 作用

用于判断字符串是否以指定后缀结尾，如果以指定后缀结尾返回True，否则返回False。可选参数"start"与"end"为检索字符串的开始与结束位置。

### 参数

* suffix:该参数可以是一个字符串或者是一个元素。

* start:字符串中的开始位置。

* end:字符中结束位置。

## 返回值

### 实例

```
>>> str = "dada5da5d4ad4ca4adqqjckzcjq"
>>> suffix = "jc"
>>> str.endswith(suffix)
False
>>> str.endswith(suffix,21)
False
>>> str.endswith(suffix,0,22)
True

>>> suffix = "jq"
>>> str.endswith(suffix)
True
```




### 语法

```
str.startswith(str[, start[, end]])
```

### 作用

返回True字符串是否与开始前缀，否则返回False

### 参数

* str:检测的字符串。

* start-- 可选参数用于设置字符串检测的起始位置。

* end-- 可选参数用于设置字符串检测的结束位置。

### 实例

```
>>> str = "HelloWorld"
>>> str.startswith("llo")
False
>>> str.startswith("Hello")
True

>>> str.startswith("Hello",2)
False
>>> str.startswith("Hlo",2)
False
>>> str.startswith("llo",2)
True
```




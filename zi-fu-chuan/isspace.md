### 语法

```
str.isspace()
```

### 作用

如果字符串中只包含空白，则返回 True，否则返回 False.

### 实例

```
>>> str = "   "
>>> str.isspace()
True

>>> str = "   \t"
>>> str.isspace()
True

>>> str = "   \n\t\r"
>>> str.isspace()
True

>>> str = "a"
>>> str = "a\t"
>>> str.isspace()
False
```




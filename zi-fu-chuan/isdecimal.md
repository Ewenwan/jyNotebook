### 语法

```
str.isdecimal()
```

### 作用

如果字符串中的所有字符都是十进制字符并且至少有一个字符，则返回true，否则返回false

### 实例

```
>>> str = 123466
>>> str.isdecimal()

>>> str = "0o123"
>>> str.isdecimal()
False
```




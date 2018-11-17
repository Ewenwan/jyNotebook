### 语法

```
str.isupper()
```

### 作用

如果字符串中包含至少一个区分大小写的字符，并且所有这些\(区分大小写的\)字符都是大写，则返回 True，否则返回 False

### 实例

```
>>> str = "dada"
>>> str.isupper()
False
>>> str = "dadaAasd"
>>> str.isupper()
False
>>> str = "ADAD"
>>> str.isupper()
True
```




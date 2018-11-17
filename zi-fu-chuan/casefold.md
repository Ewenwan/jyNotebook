### 语法

```
str.casefold()
```

### 作用

将字母变成小写字母。Casefolding类似于lowercasing但更具攻击性，因为它旨在删除字符串中的所有大小写区别。例如，德语小写字母'ß'相当于"ss"。因为它已经是小写的，所以lower\(\)什么都不做'ß'; casefold\(\) 将其转换为"ss"。

### 实例

```
>>> str = "ADASDASD"
>>> str.casefold()
'adasdasd'

>>> str = 'ß'
>>> str.casefold()
'ss'
>>> str.lower()
'ß'
```




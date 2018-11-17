### 语法

```
str.expandtabs(tabsize=8)
```

### 作用

把字符串中的 tab 符号\('\t'\)转为空格，tab 符号\('\t'\)默认的空格数是 8

### 参数

* tabsize:指定转换字符串中的 tab 符号\('\t'\)转为空格的字符数

### 实例

```
>>> str="\t123"
>>> str
'\t123'
>>> str.expandtabs(tabsize=10)
'          123'
>>> str.expandtabs(tabsize=8)
'        123'
```




### 语法

```
str.replace(old, new[, max])
```

### 作用

replace\(\) 方法把字符串中的 old（旧字符串） 替换成 new\(新字符串\)，如果指定第三个参数max，则替换不超过 max 次。

### 参数

* old:将被替换的子字符串。

* new:新字符串，用于替换old子字符串。

* max:可选字符串, 替换不超过 max 次

### 实例

```
>>> str = "www.python.org"
>>> str.replace(str,'www.python.com')
'www.python.com'

>>> str = "isisisisisis"
>>> str.replace("is","am",3)
'amamamisisis'
```




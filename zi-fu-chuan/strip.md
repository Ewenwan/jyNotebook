### 语法

```
str.strip([chars])
```

### 作用

移除字符串头尾指定的字符序列生成的新字符串

### 参数

* chars:指定移除的字符序列

### 实例

```
>>> str = "******HelloWolrd******"
>>> str.strip("*")
'HelloWolrd'
>>> str = "   HelloWorld   "
>>> str.strip()
'HelloWorld'
```




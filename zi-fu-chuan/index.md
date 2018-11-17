### 语法

```
str.index(str, begin=0, end=len(string))
```

### 作用

检测字符串中是否包含子字符串 str ，如果指定 begin（开始） 和 end（结束） 范围，则检查是否包含在指定范围内，该方法与 python find\(\)方法一样，只不过如果str不在 string中会报一个异常。

### 参数

* str -- 指定检索的字符串
* beg -- 开始索引，默认为0
* end -- 结束索引，默认为字符串的长度

### 实例

```
>>> str = "HelloWorld"
>>> str2 = "llo"
>>> str.index(str2)
2
>>> str.index(str2,5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: substring not found
>>> str.index(str2,1)
2
```




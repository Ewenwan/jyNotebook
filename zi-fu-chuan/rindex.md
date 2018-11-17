### 语法

```
str.rindex(str, begin=0 end=len(string))
```

### 作用

类似于 index\(\)，不过是从右边开始

### 参数

* str:查找的字符串

* begin:开始查找的位置，默认为0

* end:结束查找位置，默认为字符串的长度。

### 实例

```
>>> str = "HelloWorld"
>>> str2 = "llo"
>>> str.rindex(str2)
2
>>> str.rindex(str2,5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: substring not found
>>> str.rindex(str2,1)
2
```




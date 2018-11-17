### 语法

```
str.find(str, begin=0, end=len(string))
```

### 作用

检测字符串中是否包含子字符串 str ，如果指定 begin（开始） 和 end（结束） 范围，则检查是否包含在指定范围内，如果指定范围内如果包含指定索引值，返回的是索引值在字符串中的起始位置。如果不包含索引值，返回-1。

### 参数

* str:指定检索的字符串

* beg:开始索引，默认为0

* end: 结束索引，默认为字符串的长度

### 实例

```
>>> str = "HelloWorld"
>>> str2 = "llo"
>>> str.find(str2)
2
>>> str.find(str2,3)
-1
>>> str.find(str2,1)
2
```




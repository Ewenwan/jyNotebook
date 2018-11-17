### 语法

```
str.rfind(str, begin=0 end=len(string))
```

### 作用

类似于 find\(\)函数，不过是从右边开始查找.

### 参数

* str:查找的字符串

* begin:开始查找的位置，默认为0

* end:结束查找位置，默认为字符串的长度。

### 实例

```
>>> str = "HelloWorld"
>>> str2 = "llo"
>>> str.rfind(str2)
2
>>> str.rfind(str2,3)
-1
>>> str.rfind(str2,1)
2
```




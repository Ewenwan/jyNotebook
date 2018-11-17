### 语法

```
str.count(sub, start= 0,end=len(string))
```

### 作用

用于统计字符串里某个字符出现的次数。可选参数为在字符串搜索的开始与结束位置

### 参数

* sub:搜索的子字符串

* start:字符串开始搜索的位置。默认为第一个字符,第一个字符索引值为0。

* end:字符串中结束搜索的位置，但是不包括最后一个。字符中第一个字符的索引为 0。默认为字符串的最后一个位置。

### 实例

```
>>> str = "abcdefghijklmnopqrstuvwxyz"
>>> str.count('a',4,5)
0
>>> str.count('a',1,5)
0
>>> str.count('a',0,5)
1
>>> str.count('c',0,2)
0
>>> str.count('c',0,3)
1
>>> str.count('cd',0,3)
0
>>> str.count('cd',0,4)
1
```




### 语法

```
str.maketrans(intab, outtab)
```

### 作用

创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。

### 参数

* intab:字符串中要替换的字符组成的字符串
* outtab:相应的映射字符的字符串

### 实例

```
>>> intab = "abcde"
>>> outtab = "12345"
>>> tab = str.maketrans(intab,outtab)
>>> str = "book,coffee,done....,apple"
>>> str.translate(tab)
'2ook,3off55,4on5....,1ppl5'
```




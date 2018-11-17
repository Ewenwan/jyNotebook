### 语法

```
str.translate(table)
bytes.translate(table[, delete])    
bytearray.translate(table[, delete])
```

### 作用

根据 str 给出的表\(包含 256 个字符\)转换 string 的字符, 要过滤掉的字符放到 deletechars 参数中

### 实例

```
intab = "aeiou"
outtab = "12345"
trantab = str.maketrans(intab, outtab)   # 制作翻译表

str = "this is string example....wow!!!"
print (str.translate(trantab))
```

运行结果:

`th3s 3s str3ng 2x1mpl2....w4w!!!`

如何过滤掉的字符 o

```
# 制作翻译表
bytes_tabtrans = bytes.maketrans(b'abcdefghijklmnopqrstuvwxyz', b'ABCDEFGHIJKLMNOPQRSTUVWXYZ')
# 转换为大写，并删除字母o
print(b'runoob'.translate(bytes_tabtrans, b'o'))
```

运行结果:

```
b'RUNB'
```




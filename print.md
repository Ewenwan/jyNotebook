### 语法

```
print(*objects, sep=' ', end='\n', file=sys.stdout)
```

### 作用

打印输出

### 参数

* objects:复数，表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。

* sep:用来间隔多个对象，默认值是一个空格。

* end:用来设定以什么结尾。默认值是换行符 \n，我们可以换成其他字符串。

* file:要写入的文件对象。

### 实例

```
>>> print("HelloWorld")
HelloWorld

>>> name = "angle"
>>> age = 18

>>> print(name,age)
angle 18

>>> print("angle""age")
angleage
>>> print("angle","age")
angle age

>>> print(name,age,sep='*')
angle*18
>>> print(name,age,sep=',')
angle,18

>>> print(name,age,sep=',',end='-')
angle,18-


>>> print(name,age,sep=',',end='-',file='d:\1.txt')
```




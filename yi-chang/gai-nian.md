### 什么是语法错误？

语法错误，一般是代码出现错误，导致程序不能运行

```
>>> if True
  File "<stdin>", line 1
    if True
          ^
SyntaxError: invalid syntax
>>> if True:
...     print(True)
...
True
```

这里if语句后面没有写上冒号\(:\)导致程序不能运行，从而产生了语法错误

### 什么是异常？

有时候一条语句或表达式在语法上是正确的，但是试图执行语句时可能会引发错误，所以运行期间检测到的错误称为异常

```
>>> 2/3
0.6666666666666666
>>> 2/0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
```

第一个表达式2/3能够正常运行，而下面的同样的格式的表达式却曝出ZeroDivisionError错误，这个就是异常，意思是除数不能为0


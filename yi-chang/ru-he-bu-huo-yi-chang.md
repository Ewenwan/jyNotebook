### 异常处理

python中使用try...except处理程序抛出的异常

##### 语法

```
try:
    语句1
except:
    语句2
except:
    ....


try:
    语句1
except:
    语句2
except:
    ....
else:
    pass
```

try语句按如下方式工作：

* 首先，执行_try_子句 （在try/except和关键字之间的部分）。

* 如果没有异常发生，_except_子句 在try语句执行完毕后就被忽略了。

* 如果在 try 子句执行过程中发生了异常，那么该子句其余的部分就会被忽略。

  如果异常匹配于except关键字后面指定的异常类型，就执行对应的except子句。然后继续执行语句之后的代码。

* 如果最终仍找不到对应的处理语句，它就成为一个_未处理异常_，终止程序运行，显示提示信息。

* 一个 try 语句可能包含多个 except 子句，分别指定处理不同的异常

```
>>> name = int(input())
aad
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: 'aad'
>>> try:
...     a = int(input())
...     print(a/0)
... except ValueError:
...     print(ValueError)
... except:
...     pass
...
asd
<class 'ValueError'>
```

try … except 语句可以带有一个 else子句，该子句只能出现在所有 except 子句之后。当 try 语句没有抛出异常时，需要执行一些代码，可以使用这个子句

```
>>> try:
...     print("正常")
... except:
...     print("错误")
... else:
...     print("还要运行")
...
正常
还要运行
```

使用else子句比在try子句中附加代码要好，因为这样可以避免try…except意外的截获本来不属于它们保护的那些代码抛出的异常。

发生异常时，可能会有一个附属值，作为异常的_参数_存在。这个参数是否存在、是什么类型，依赖于异常的类型。

在异常名（列表）之后，也可以为 except 子句指定一个变量。这个变量绑定于一个异常实例，它存储在`instance.args`的参数中。为了方便起见，异常实例定义了\_\_str\_\_\(\)，这样就可以直接访问过打印参数而不必引用`.args`。这种做法不受鼓励。相反，更好的做法是给异常传递一个参数（如果要传递多个参数，可以传递一个元组），把它绑定到 message 属性。一旦异常发生，它会在抛出前绑定所有指定的属性。

```
>>> try:
...    raise Exception('spam', 'eggs')
... except Exception as inst:
...    print(type(inst))    # the exception instance
...    print(inst.args)     # arguments stored in .args
...    print(inst)          # __str__ allows args to be printed directly,
...                         # but may be overridden in exception subclasses
...    x, y = inst.args     # unpack args
...    print('x =', x)
...    print('y =', y)
...
<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x = spam
y = eggs
```

对于那些未处理的异常，如果一个它们带有参数，那么就会被作为异常信息的最后部分（“详情”）打印出来。

异常处理器不仅仅处理那些在 try 子句中立刻发生的异常，也会处理那些 try 子句中调用的函数内部发生的异常。例如:

```
>>> def this_fails():
...     x = 1/0
...
>>> try:
...     this_fails()
... except ZeroDivisionError as err:
...     print('Handling run-time error:', err)
...
Handling run-time error: int division or modulo by zero
```




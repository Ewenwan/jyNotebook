断言函数用来什么某个条件是真的，其作用是测试一个条件是否成立，如果不成立，则抛出异常

---

先来看看断言函数assert的语法:

```
语法:

assert condition (expression)
```

如果condition为false，就抛出一个AssertionError异常

expression为可选参数，可以自定以打印的内容

实例:

```
>>> a = 1
>>> b = 2
>>> assert a > b
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError
```

```
>>> assert a > b,'{} is less than {}'.format(a,b)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError: 1 is less than 2
```




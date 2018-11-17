### 语法

```
delattr(object, name)
```

### 作用

删除属性

### 参数

* object:对象
* name:必须是对象的属性

### 实例

```
>>> class test:
...     a=1
...     b=2
...     c=3
...
>>> test.a
1
>>> test.b
2
>>> test.c
3
>>> delattr(test,"c")
>>> test.c
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: type object 'test' has no attribute 'c'
```




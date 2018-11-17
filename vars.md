### 语法

```
vars([object])
```

### 作用

返回对象object的属性和属性值的字典对象

### 参数

* object:对象

### 实例

```
>>> vars()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'name': 'angle', 'age': 18, 'lst': [1, 2, 34], 'i': 34, 'a': [1, 2, 3, 4], 'func': <function func at 0x000001BB7C96C730>, 'v': <memory at 0x000001BB7C92C408>, 'it': <list_iterator object at 0x000001BB7C9EE080>, 'x': 5, 'C': <class '__main__.C'>, 'b': ('h', 'e', 'l', 'l', 'o'), 'c': ['h', 'e', 'l', 'l', 'o'], 'd': range(5, 9), 'f': 1.234567, 'test': <class '__main__.test'>, 'result': slice(None, 2, None), 'value': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9], 'cobj': <__main__.C object at 0x000001BB7C9EE978>, 'dict': {'name': 'angle'}}
>>> class A():
...     num = 1
...
>>> vars(A)
mappingproxy({'__module__': '__main__', 'num': 1, '__dict__': <attribute '__dict__' of 'A' objects>, '__weakref__': <attribute '__weakref__' of 'A' objects>, '__doc__': None})
>>> a = A()
>>> vars(a)
{}
```




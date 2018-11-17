### 语法

```
staticmethod(function)
```

### 作用

返回函数的静态方法

### 实例

```
 class A(object):
    @staticmethod
    def func():
        print('python');



A.func();          # 静态方法无需实例化
a= A()
a.func()        # 也可以实例化后调用
```




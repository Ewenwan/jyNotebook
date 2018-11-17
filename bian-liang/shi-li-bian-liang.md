### 什么是实例变量？

实例变量是定义在方法中的变量，使用self绑定到实例上的变量，只是对当前实例起作用

### 如何使用？

在类的内部，实例变量`self.实例变量`的形式访问；在类的外部使用`对象名.实例变量`的形式访问。

```
class A:

    def __init__(self,name):
        self.name = name

a1 = A("angle")
a2 = A("miku")

print(a1.name,a2.name)
```

运行结果：

```
angle miku
```




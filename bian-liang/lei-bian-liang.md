### 什么是类变量？

* 类变量就是定义在类中，但是在函数体之外的变量。通常不使用self.变量名赋值的变量。类变量通常不作为类的实例变量的，类变量对于所有实例化的对象中是公用的。
* 通过类名可以直接访问，也可以通过实例名直接访问，此变量在类中全局共享，实例之间也是全局共享

### 如何使用？

在类中定义变量，自调用时就开始生效，直到类销毁

```
class A:
    number = 0
    def add(self):
        A.number += 1

a1 = A()
a2 = A()

print(a1.number)
print(a2.number)

a1.add()
print(a1.number)
print(a2.number)


a2.add()
print(a1.number)
print(a2.number)
```

运行结果:

```
0
0
1
1
2
2
```




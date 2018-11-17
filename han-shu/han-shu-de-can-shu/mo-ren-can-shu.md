### 默认参数有什么用?

默认参数可以在参数定义的过程中，为形参进行赋值，当函数调用的时候，不传递实参，则默认使用形参的初始值代替。

举个小栗子

```
def person(name,age,sex='未知'):
    print('{0}的年龄是{1},性别{2}'.format(name,age,sex))


person(name='angle',age='18')
person(name='angle',age='18',sex='男')
```

是不是很简单，那么继续往下学习


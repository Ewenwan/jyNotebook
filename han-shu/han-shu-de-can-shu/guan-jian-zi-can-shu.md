由于在调用函数的时候，有时候可能会很粗心不小心把参数位置的顺序给弄错了，从而导致函数无法按照预期实现要求。

因此关键字参数是为了解决这个问题而出现的，有了这个就可以很简单的解决这个潜在的问题了。

举个例子

```
def person(name,age):
    print('{0}的年龄是{1}'.format(name,age))

person("angle","18")

person("18","angle")

person(age="18",name="angle")

person(name="angle",age="18")
```

运行结果:

```
angle的年龄是18
18的年龄是angle
angle的年龄是18
angle的年龄是18
```

从结果可以看到关键字参数是很有用的，因为参数的顺序一不小心弄错，会导致程序无法完成预期的结果的


### 什么是内嵌函数？

内嵌函数其实就是一个函数在其内部在套一个函数，和嵌套循环一样，又可以叫做内部函数

示例:

```
def outFunc(name):

    print("outFunc()正在被调用")

    def inFunc(name):

        print("inFunc()正在被调用")
        return name

    return inFunc(name)


print(outFunc("angle"))
```

运行结果:

```
outFunc()正在被调用
inFunc()正在被调用
angle
```

是不是很简单，但是这个只能调用outFunc\(\)函数，而inFunc\(\)函数只能在outFunc\(\)函数中调用，而在outFunc\(\)函数外调用，会进行报错，因为inFunc\(\)函数的作用域只在outFunc\(\)函数内才生效

```
def outFunc(name):

    print("outFunc()正在被调用")

    def inFunc(name):

        print("inFunc()正在被调用")
        return name

    return inFunc(name)

inFunc("angle")
```

运行结果:

```
def outFunc(name):

    print("outFunc()正在被调用")

    def inFunc(name):

        print("inFunc()正在被调用")
        return name

    return inFunc(name)

inFunc("angle")
```




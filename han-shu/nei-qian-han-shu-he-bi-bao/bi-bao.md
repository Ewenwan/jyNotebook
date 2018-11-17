### 什么是闭包？

python中的闭包从表现形式上定义为:如果在一个内部函数里，对在外部作用域\(但不是在全局作用域\)的变量进行引用，那么内部函数就被认为是闭包。

举个小栗子

```
def outFunc(param1):

    def inFunc(param2):

        print("inFunc()函数,param2参数值为{}".format(param2))

        return param1 * param2

    # 注意，这里返回的闭包的结果
    return inFunc

test = outFunc(3)
# 这里其实调用的是inFunc(param2),参数5传给的是param2
result = test(5)
print(result)
```

运行结果:

```
inFunc()函数,param2参数值为5
15
```

可以将

```
test = outFunc(3)
result = test(5)
```

缩写为

```
result = outFunc(3)(5)
```

这两者之间是等价的

```
def outFunc(param1):

    def inFunc(param2):

        print("inFunc()函数,param2参数值为{}".format(param2))

        return param1 * param2
    return inFunc

result = outFunc(3)(5)
print(result)
```

运行结果

```
inFunc()函数,param2参数值为5
15
```




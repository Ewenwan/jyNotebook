已经知道了如何定义函数，那么该如何调用这个函数，接下来继续以上面的那个例子作为示例，进行讲解

```
def fib(n):                # 定义一个函数名称，用来计算fibonacci数
    a,b = 1,1              # 赋值
    for i in range(n):    
        print(a,end=' ')
        a,b = b,a+b
    print()

fib(10)                    # 调用函数, 并传入一个参数
```

看，这样就调用了，是不是很简单

运行结果:

```
1 1 2 3 5 8 13 21 34 55
```

### 函数引用

```
def outFunc():

    print("outFunc()正在被调用")

# 引用函数
outfunc = outFunc
# 通过引用调用函数
outfunc()

# 调用函数
outFunc()



print(id(outfunc))
print(id(outFunc))
```

运行结果:

```
outFunc()正在被调用
outFunc()正在被调用
2357814673888
2357814673888
```




### 语法

```
issubclass(class, classinfo)
```

### 作用

用于判断参数 class 是否是类型参数 classinfo 的子类，如果是则返回True，否者返回False

### 参数

* class:类

* classinfo:类

### 实例

```
class A:
    pass
class B(A):
    pass

print(issubclass(B,A))    # 返回 True
```




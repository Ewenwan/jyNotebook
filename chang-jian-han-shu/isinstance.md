### 简述

isinstance\(\)函数:判断一个对象是否是一个已知的类型

### 语法

```
isinstance(obj, class_or_tuple, /)
```

#### 参数

* object:实例对象
* class\_or\_tuple:可以是直接或间接类名，基本类型或者由其组成的元组

### 返回值

如果对象的类型与参数class\_or\_tuple的类型相同则返回True，否者返回False

### 实例

```
>>> num = 10.0
>>> isinstance(num,float)
True
>>> isinstance(num,int)
False
>>> isinstance(num,(float,int,str)) # 元祖中有一个与num的类型相同则返回True
True
```

> 温馨提示
>
> isinstance\(\) 与 type\(\) 区别：
>
> * type\(\) 不会认为子类是一种父类类型，不考虑继承关系。
>
> * isinstance\(\) 会认为子类是一种父类类型，考虑继承关系。
>
> 如果要判断两个类型是否相同推荐使用 isinstance\(\)。




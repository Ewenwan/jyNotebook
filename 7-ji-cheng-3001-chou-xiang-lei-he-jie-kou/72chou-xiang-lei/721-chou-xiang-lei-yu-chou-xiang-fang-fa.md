抽象类是以修饰符abstract修饰的类，定义抽象类的语法格式如下:

```
abstract class 类名
{
    声明成员变量;
    返回值的数据类型 方法名(参数表)
    {
        ...
    }
    abstract 返回值的数据类型 方法名 (参数表) --- 抽象发方法，在抽象方法里，不能定义方法体
}
```

注意:

1. 由于抽象类是需要被集成的，所以abstract类不能用final来修饰。也就是说，一个类不能既是最终类，又是抽象类，即关键字abstract与final不能合用
2. abstract不能与private、static、final或native并列修饰同一个方法




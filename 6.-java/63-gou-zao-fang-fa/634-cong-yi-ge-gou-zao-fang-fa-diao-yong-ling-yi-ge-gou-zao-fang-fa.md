```
package lei;

public class box {
    private String name;
    private String sex;
    public box(String name,String sex)
    {
        this(name);    //用this关键字来调用另一构造方法
        this.sex = sex;
    }

    public box(String name)
    {
        this.name = name; // 
    }

    public String getName()
    {
        return name;
    }
}
```

在某一构造方法中调用另一构造方法时，必须使用this关键字来调用，否则编译时将出现错误

this关键字必须写在构造方法内的第一行位置


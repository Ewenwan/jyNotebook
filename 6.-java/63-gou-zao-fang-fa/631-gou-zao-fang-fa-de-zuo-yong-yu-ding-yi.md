构造方法是一种特殊的方法，是在对象被创建时初始化对象的成员的方法

构造方法的方法与类名完全相同

构造方法没有返回值

构造方法定义后，创建对象时就会自动调用它，因此构造方法不需要再程序中直接调用，而是在对象产生时自动执行

```
package lei;

public class box {
    private String name;
    public box(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }
}



package lei;

public class test1 {

    public static void main(String[] args) {
        box b = new box("angle");
        System.out.println(b.getName());
    }

}
```




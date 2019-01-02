由于抽象类的目的是要根据它的格式来创建新的类，所以抽象类里的抽象方法并没有定义处理数据的方法体，而是要保留给由抽象类派生出的子类来定义

```
public abstract class superbox {
    private int num;

    abstract public int get1(int a,int b);

}

public class box extends superbox{


    @Override
    public int get1(int a, int b) {
        System.out.println(a+b);
        return 0;
    }
}

public class test1 {

    public static void main(String[] args) {
        box a = new box();
        a.get1(0, 0);
    }

}
```




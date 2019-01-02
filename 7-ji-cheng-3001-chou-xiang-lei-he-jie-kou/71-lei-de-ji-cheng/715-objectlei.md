在java语言中有一个特殊的类object，该类是java.lang类库中的一个类，所有类都是直接或间接地继承该类而得到的，即如果某个类没有使用extends关键字，则该类默认为java.lang.Object类的子类

---

Object类常用的方法

| 方法 | 功能说明 |
| :--- | :--- |
| public boolean equals\(Object obj\) | 判断两个对象变量所指向的是否为同一个对象 |
| public String toString\(\) | 将调用toString\(\)方法的对象转换成字符串 |
| public final Class getClass\(\) | 返回运行getClass\(\)方法的对象所属的类 |
| protected Object clone\(\) | 返回调用该方法的对象一个副本 |

* getSuperclass\(\)方法获得父类
* 对象运算符instanceof:测试一个指定对象是否指定类或它的子类的实例，若是，则返回true，否则返回false




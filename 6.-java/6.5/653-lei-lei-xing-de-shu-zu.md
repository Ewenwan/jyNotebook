* 声明类类型的数组变量，并用new运算符分配内存空间给数组
* 用new创建新的对象，分配内存空间给它，并让数组元素指向它

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


package lei;

public class test1 {

	public static void main(String[] args) {
		box arr[];
		arr = new box[3];
		arr[0] = new box("angle1");
		arr[1] = new box("angle2");
		arr[2] = new box("angle3");
		for(box a:arr)
			 System.out.println(a.getName());
	}

}

```




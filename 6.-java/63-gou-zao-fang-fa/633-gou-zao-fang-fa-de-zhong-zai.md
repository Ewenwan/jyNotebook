所谓重载，是指同一个类内定义相同名称的多个方法，这些同名的方法或者参数的个数不同、或者参数的个数相同但类型不同，则这些同名的方法便可具有不同的功能

```
package lei;

public class box {
	private String name;
	public box(String name)
	{
		this.name = name;
	}
	
	public box()
	{
		
	}
	public String getName()
	{
		return name;
	}
}

```




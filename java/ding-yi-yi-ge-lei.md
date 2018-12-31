```

public class UserDemo {
	private String name;
	private int age;
	
	public UserDemo(String name,int age)
	{
		this.name = name;
		this.age = age;
	}
	
	public UserDemo()
	{
		
	}
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}
	
	//重写toString方法
	@Override
	public String toString()
	{
		return "我的名字叫"+this.name+"现在我已经有"+this.age+"岁了";
	}
	
	
}

```




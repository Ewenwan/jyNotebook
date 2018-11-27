```
import java.util.Scanner;
import java.util.Comparator;
import java.util.List;
import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;
import java.util.Iterator;

// 自定义排序类
class StudentComparator implements Comparator{

	@Override
	public int compare(Object a, Object b) {
		
		Student s1 = (Student) a;
		Student s2 = (Student) b;
		
		if(s1.getS() < s2.getS())
			return 1;
		else if(s1.getS() > s2.getS())
			return -1;
		else
			if( s1.getK() > s2.getK())
				return 1;
			else
				return -1;
	}
	
	
}

// student类
class Student {
	int k,s;
	
	public Student(int k,int s) {
		this.k = k;
		this.s = s;
	}
	
	public int getK() {
		return this.k;
	}
	
	public void setK(int k) {
		this.k = k;
	}

	public int getS() {
		return this.s;
	}
	
	public void setS(int s) {
		this.s = s;
	}
	
	
}


public class yx_Main {

	public static void main(String[] args) {
		Scanner sca = new Scanner(System.in);
		int n,m;
		
		// 读入数据
		n = sca.nextInt();
		m = sca.nextInt();
		m = (int) Math.floor(m*1.5);
		
		//创建列表
		List<Student> students = new ArrayList<>();
		for(int i=0;i<n;i++)
		{
			int k,s;
			k = sca.nextInt();
			s = sca.nextInt();
			
			//创建实例对象
			Student stu = new Student(k,s);
			students.add(stu);
		}
		
		Collections.sort(students, new StudentComparator());
		int a;
		int count = 0;
		//创建迭代对象
		Iterator it = students.iterator();
		//判断是否有下一个对象
		while(it.hasNext()) {
			count++;
			//获取迭代对象的值
			Student stu = (Student) it.next();
            System.out.println(stu.getK() + " " + stu.getS());
            if(count == m)
            {
            	while(it.hasNext())
            	{
            		Student stu2 = (Student) it.next();
            		if(stu2.getS()!= stu.getS())
            			break;
            		else
            		{
            			System.out.println(stu2.getK() + " " + stu2.getS());
            			count++;
            		}
            	}
            	break;
            }
        }
	}

}

//6 3
//1000 90
//3239 88
//2390 95
//7231 84
//1005 95
//1001 88

```




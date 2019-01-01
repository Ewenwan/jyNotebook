### 什么是JDBC?

java数据库连接，是java语言中用来规范客户端程序如何来访问数据库的应用程序接口，提供了操作数据库的方法

### 为什么要使用JDBC?

JDBC:java database connectivity SUN公司提供的一套操作数据库的标准规范

JDBC与数据库驱动的关系:接口与实现的关系

JDBC规范\(掌握四个核心对象\)

* DriverManager:用于注册驱动
* Connection:表示数据库创建的连接
* Statement:操作数据库sql语句的对象
* ResultSet:结果集或一张虚拟表

### 执行流程

* 连接数据库
* 为数据库传递查询和更新指令
* 处理数据库响应并返回的结果

### JDBC结构

#### 双层结构

![](/assets/java-1.2-1.png)

* 作用:此架构中，java Applet或应用直接访问数据源
* 条控件:要求Driver能与数据库进行交互
* 机制:用户命令传给数据库或其他数据源，随之结果被返回
* 部署:数据源可以在另一台机器上，用户通过网络连接，称为C/S配置（可以是内联网或者是互联网）

```
proprietary protocol:所有控制权
DBMS:数据库管理系统
client machine:客户端机器
database server:数据库服务
```

#### 三层结构

![](/assets/java-1.2-2.png)

* 引入了中间层服务
* 流程:命令和结构都会经过该层
* 吸引:可以增加企业数据的访问控制，以及多种类型的更新；另外可以简化应用部署，并在多数情况下有性能的优势

### 开始操作数据库

* 导入mysql的jdbc的jar包
* 创建项目文件
* 加载驱动程序

```
String driver = "com.mysql.jdbc.Driver";
// 加载驱动
Class.forName(this.driver);
```

* 获得数据库连接

```
// jdbc数据库连接地址
private String URL = "jdbc:mysql://localhost:3306/train_sql";
// 用户名
private String USER = "root";
// 密码
private String PASSWORD = "123456";
// 获得数据库连接
this.conn = DriverManager.getConnection(this.URL, this.USER, this.PASSWORD);
```

* 创建Statement\PreparedStatement兑现

```
conn.createStatement();
conn.prepareStatement();
```

* 添加

```
    public void insert(String name,int age) throws SQLException
    {
        /*
         第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

        INSERT INTO table_name
        VALUES (value1,value2,value3,...);
        第二种形式需要指定列名及被插入的值：

        INSERT INTO table_name (column1,column2,column3,...)
        VALUES (value1,value2,value3,...);
         * */
        String sql = "insert into people values('"+name+"',"+age+")";
        System.out.println(sql);
        this.stmt.execute(sql);
        this.close();
    }
```

* 删除

```
    public void del(String name) throws SQLException
    {
        /*
         DELETE FROM table_name
         WHERE some_column=some_value;
         * */
        String sql = "delete from people where name='"+name+"'";
        this.stmt.execute(sql);
        this.close();
    }
```

* 更新

```
    public void update(String name,int age) throws SQLException
    {
        /*
           UPDATE table_name
           SET column1=value1,column2=value2,...
           WHERE some_column=some_value;
        */
        String sql = "update people set age= "+age+" where name='"+name+"'";
        this.stmt.executeUpdate(sql);
        this.close();
    }
```

* 查询

```
    public void find(String name) throws SQLException
    {
        String sql = "select * from people where name='"+name+"'";
        this.rs = this.stmt.executeQuery(sql);
        while(rs.next())
            System.out.println(rs.getString("name")+"的岁数是"+rs.getInt("age"));
        this.close();
    }

    public void findall() throws SQLException
    {
        String sql = "select * from people;";
        this.rs = this.stmt.executeQuery(sql);
        while(rs.next())
            System.out.println(rs.getString("name")+"的岁数是"+rs.getInt("age"));
        this.close();
    }
```

* 最后一定要记住关闭

```
    public void close() throws SQLException
    {    
        if(rs != null)
            this.rs.close();
        if(stmt != null)
            this.stmt.close();
        if(conn != null)
        this.conn.close();

    }
```

* 完整sql实例

```
package com.train.demo1;
import java.sql.*;

public class sqlDemo {

    String driver = "com.mysql.jdbc.Driver";

    // jdbc数据库连接地址
    private String URL = "jdbc:mysql://localhost:3306/train_sql";
    // 用户名
    private String USER = "root";
    // 密码
    private String PASSWORD = "123456";

    Connection conn;
    Statement stmt;
    ResultSet rs;



    public sqlDemo() throws ClassNotFoundException, SQLException
    {
        // 加载驱动
        Class.forName(this.driver);
        // 获得数据库连接
        this.conn = DriverManager.getConnection(this.URL, this.USER, this.PASSWORD);
        // 实例化createStatement对象和ResulSet对象,开始操作数据库
        this.stmt = conn.createStatement();
        this.rs = null;

        this.start();
    }

    public void start() throws SQLException
    {
        // 创建表，字段为name和age
        String sql = "create table people(name char(50),age int)";
        // 判断某表是否存在
        String exists = "SELECT COUNT(*) as number FROM information_schema.TABLES WHERE TABLE_NAME='people'";
        // 返回查询结果
        ResultSet e = this.stmt.executeQuery(exists);
        // 定义flag标志，默认未创建
        int flag = 0;
        // 判断下一个是否有数据
        if(e.next())
            flag = e.getInt("number");
        if(flag == 0)
            stmt.execute(sql);
    }

    public void insert(String name,int age) throws SQLException
    {
        /*
         第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

        INSERT INTO table_name
        VALUES (value1,value2,value3,...);
        第二种形式需要指定列名及被插入的值：

        INSERT INTO table_name (column1,column2,column3,...)
        VALUES (value1,value2,value3,...);
         * */
        String sql = "insert into people values('"+name+"',"+age+")";
        System.out.println(sql);
        this.stmt.execute(sql);
        this.close();
    }

    public void del(String name) throws SQLException
    {
        /*
         DELETE FROM table_name
         WHERE some_column=some_value;
         * */
        String sql = "delete from people where name='"+name+"'";
        this.stmt.execute(sql);
        this.close();
    }

    public void find(String name) throws SQLException
    {
        String sql = "select * from people where name='"+name+"'";
        this.rs = this.stmt.executeQuery(sql);
        while(rs.next())
            System.out.println(rs.getString("name")+"的岁数是"+rs.getInt("age"));
        this.close();
    }

    public void findall() throws SQLException
    {
        String sql = "select * from people;";
        this.rs = this.stmt.executeQuery(sql);
        while(rs.next())
            System.out.println(rs.getString("name")+"的岁数是"+rs.getInt("age"));
        this.close();
    }

    public void update(String name,int age) throws SQLException
    {
        /*
           UPDATE table_name
           SET column1=value1,column2=value2,...
           WHERE some_column=some_value;
        */
        String sql = "update people set age= "+age+" where name='"+name+"'";
        this.stmt.executeUpdate(sql);
        this.close();
    }

    public void close() throws SQLException
    {    
        if(rs != null)
            this.rs.close();
        if(stmt != null)
            this.stmt.close();
        if(conn != null)
        this.conn.close();

    }
}
```

* 测试

```
package com.train.demo1;
import java.sql.*;

public class test {

    public static void main(String[] args) {
        String name = "angle";
        int age = 18;

        int uage = 100;
        try {
            sqlDemo sd = new sqlDemo();
//            //插入
//            sd.insert(name, age);

//            //删除
//            sd.del(name);

//            //更新
//            sd.update(name, uage);

//            //单个查询
//            sd.find(name);

//            //查询全部
//            sd.findall();

        } catch (ClassNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (SQLException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

}
```

* 预编译对象使用（PreparedStatement对象）

```
package com.train.jdbc;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import org.junit.Test;

import com.mysql.jdbc.PreparedStatement;
import com.train.test.*;

//create database student charset=utf8;
//use student;
//create table users(id int not null auto_increment primary key,username varchar(255),password varchar(255));
//desc student;
public class JdbcDemo {
	// 获取数据库地址
	static String url = "jdbc:mysql://localhost:3306/student?characterEncoding=utf-8";
	static String username = "root";
	static String password = "123456";
	
	public  static void main(String[] args) {
//		User user = new User(2, "a","b");
		List<User> items =  findUser(new User(2,null,null));
		for(User item:items)
			System.out.println(item);
//		findallUser();
	}
	
	
	public static void start()
	{
		try {
			Class.forName("com.mysql.jdbc.Driver");
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	}
	
	public static void addUser(User user)
	{
		start();
		try {
			Connection conn = DriverManager.getConnection(url, username, password);
			
			//创建StateMent对象
			//preparedstatement:预编译对象
			String sql = "insert into users(username,password) values(?,?)";
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			//设置参数
			ps.setString(1, user.getUsername());
			ps.setString(2, user.getPassword());
			//执行、更新
			int flag = ps.executeUpdate();
			System.out.println(flag);
			
			
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void updateUser(User user)
	{
		start();
		try {
			Connection conn = DriverManager.getConnection(url, username, password);
			String sql = "update users set username=?,password=? where id=?";
			
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			ps.setString(1, user.getUsername());
			ps.setString(2, user.getPassword());
			ps.setInt(3, user.getId());
			
			int flag = ps.executeUpdate();
			System.out.println(flag);
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	
	public static void delUser(User user)
	{
		start();
		try {
			Connection conn = DriverManager.getConnection(url, username, password);
			String sql = "delete from users where id=?";
			
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			ps.setInt(1, user.getId());
			
			int flag = ps.executeUpdate();
			System.out.println(flag);
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	public static List<User> findUser(User user)
	{
		List<User> luser = new ArrayList<User>();
		start();
		try {
			Connection conn = DriverManager.getConnection(url, username, password);
			String sql = "select * from users where id=?";
			
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			ps.setInt(1, user.getId());
			ResultSet rs = ps.executeQuery();
			
			while(rs.next())
			{
				Integer id = rs.getInt("id");
				String username = rs.getString("username");
				String password = rs.getString("password");
				luser.add(new User(id,username,password));
				System.out.println("用户名:"+rs.getString("username")+","+rs.getString("password"));
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return luser;
	}
	
	public static void findallUser()
	{
		start();
		try {
			Connection conn = DriverManager.getConnection(url, username, password);
			String sql = "select * from users";
			PreparedStatement ps = (PreparedStatement) conn.prepareStatement(sql);
			ResultSet rs = ps.executeQuery();
			
			while(rs.next())
				System.out.println("用户名:"+rs.getString("username")+","+rs.getString("password"));
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
}

```

* 预编译的作用
  * 可以优先sql
  * 更加方便




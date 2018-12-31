### 什么是JDBC?

java数据库连接，是java语言中用来规范客户端程序如何来访问数据库的应用程序接口，提供了操作数据库的方法

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




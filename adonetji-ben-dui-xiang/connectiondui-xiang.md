```
'导入包'
imports System.Data.SqlClient

'Data Source=服务器名称;Initial Catalog=数据库名称;Integrated Security=True;本地验证'
Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"

'定义数据库连接对象|创建Connection对象'
Dim conn As SqlConnection = New SqlConnection(connstr)

'打开数据库连接'
conn.Open()

'得到ConnectionString,连接的数据库字符串'
Dim str As String = conn.ConnectionString.ToString();


'关闭连接'
conn.Close()
```

---

## SqlConnection对象的ConnectionString属性

| 参数 | 说明 |
| :--- | :--- |
| Data Source\(server\) | 指定数据源\(服务器\)名称 |
| Initial Catalog\(database\) | 指定数据库名 |
| User ID\(uid\) | 指定登录数据库服务器的用户名 |
| Password \(pwd\) | 指定登录数据库服务器的用户口令 |
| Integrated Security | 指定采用信任模式连接 |

---

## SqlConnection对象的常用方法

| 方法 | 说明 |
| :--- | :--- |
| BeginTransaction | 开始一个数据库事务 |
| Open | 打开数据库连接 |
| Close | 关闭数据库连接 |
| Dispose | 显示释放对象时关闭数据库连接 |
| CreateCommand | 创建并返回一个与该连接相关的Command对象 |




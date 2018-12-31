使用command对象对数据库进行增、删、查、改操作

---

## SqlCommand对象的常用属性

| 属性 | 说明 |
| :--- | :--- |
| CommandText | 设置或获取在数据源上执行的SQL语句或存储过程名 |
| CommandType | 设置或获取一个CommandType对象，指明如何理解CommandText属性，如StoredProcedure表示是存储过程名，Text表示sql文本命令 |
| Connection | 设置或返回与Command相关的Connection对象 |
| SqlTransaction | 返回该命令所处的Transaction\(事务\)对象 |
| Parameters | 返回SQL的参数集合 |

---

## SqlCommand对象的常用方法

| 方法 | 说明 |
| :--- | :--- |
| ExecuteReader | 执行CommandText中的SQL查询语句，查询值返回到DATAReader对象 |
| ExecuteScalar | 返回单个值，如求和、求最大值等sql聚合函数 |
| ExceuteNonQuery | 执行增、删、改等无返回值的sql操作 |
| Cancel | 放弃命令的执行 |
| Prepare | 将命令预存与数据源，加快执行效率 |

---

```
'引入命名空间'
imporst System.Data.Client

Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"

'创建Connection对象'
Dim conn As SqlConnection = New SqlConnection(connstr)

'打开数据库连接'
conn.Open()

'定义sqlstr命令'
Dim sqlstr As String  = "delete from 表名 where 字段名=" + 字段值

'创建command对象'
'Dim com As SqlCommand = New SqlCommand(sqlstr,conn)'
Dim com As SqlCommand = New SqlCommand()
com.Connection = conn
com.CommandText = sqlstr

'执行sql语句'
com.ExecuteNonQuery()

'关闭连接'
conn.Close()


'要添加事务，如下'

'启动事务'
SqlTransaction  myTrans = con.BeginTransaction();

com.ExecuteNonQuery();

com.Transaction = myTrans

'提交事务'
myTrans.Commit()
```




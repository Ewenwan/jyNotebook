## 导入包

```
Imports System.Data.SqlClient
```

## 参数含义

```
Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;
Integrated Security=True"

Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;
user=id;password=password"
```

* source:服务器名称
* Catalog:指定数据库名称
* Integrated Security=True:本地验证
* user:用户名id
* password:密码password

---

## 创建联接对象

```
Dim conn As SqlConnection = New SqlConnection(connstr)
```

---

## 打开联接&关闭连接

```
conn.Open()
conn.Close()
```

---

## 创建sql命令对象--用于提交sql语句\(进行交互\)

```
Dim sqlcom As SqlCommand = New SqlCommand(sqlstr,conn)

sqlcom.ExceuteNonQuery()
```

---




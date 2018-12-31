* Dim str as String:定义为字符串类型
* Request.From\("id"\):获取html页面的id属性值
* 注意在vb中是以''/单引号进行注释
* Response.Write\(""\):向页面传入数据

---

## ASP表单

---

### 用户输入

Request对象可用于从表单取回用户信息

```
<td width="100px"><asp:Label ID="Label1" runat="server" Text="姓名"></asp:Label></td>
<td width="140px"><asp:TextBox ID="sname" runat="server"></asp:TextBox></td>
```

用户输入的信息可通过两种方式取回:Request.QueryString或Request.Form

#### Request.QueryString

Request.QueryString命令用于搜集使用method="get"的表单中的值。

#### Request.Form

Request.Form命令用于搜集使用"post"方法的表单中的值

---

## sqlDataReader的用法

```
Dim com As SqlCommand = New SqlCommand(sqlstr, conn)
Dim sreader As SqlDataReader = com.ExecuteReader
```

---

### 属性

* Depth:返回类型为int，取得表示当前行嵌入深度的值
* FieldCount:其返回类型为int，取得当前行的列数
* IsColsed：返回类型为bool，表示是否关闭数据读取
* RecordAffected:返回类型为int，取得执行sql语句增加、修改或删除的行数

### 方法

* Reader\(\):返回类型为bool，读取该行
* GetValue\(\):返回类型为object，返回指定的列
* GetValues\(\):返回类型为int，将当前所有列的值复制到指定对象数组，这个方法的int是数组元素的个数
* NextResult\(\):返回类型为bool，将数据迭代下一行
* close\(\):关闭sqldatareader对象
* ExecuteReader\(\):执行sql语句并查询

---

## DataAdapter类和DataSet对象

```
Dim sp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
Dim ds As DataSet = New DataSet
sp.Fill(ds)
```




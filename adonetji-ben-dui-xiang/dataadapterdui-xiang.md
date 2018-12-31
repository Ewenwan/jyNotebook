DataAdapter对象，用来从数据源中获取数据的，是DataSet和数据库之间的桥梁，用于检索和保存数据。DataAdapter对象从数据源得到的数据填充在DataSet中，并将在DataSet中对数据进行修改提交回数据源

DataAdapter一般要与DataSet共同使用来操作数据库中的数据

---

## DataAdapter对象的常用属性

| DeleteCommand | 获取或设置用来从数据源删除数据的SQL命令，此属性只有在调用Update\(\)方法并从数据源中删除数据行时使用，其主要用途是告知DataAdapter对象如何从数据源中删除数据行 |
| :--- | :--- |
| InsertCommand | 获取或设置用来从数据源插入数据的SQL命令，使用原则同上 |
| SelectCommand | 获取或设置用来从数据源选取数据行的SQL命令 |
| UpdateCommand | 获取或设置用来更新数据源数据行的SQL命令 |

---

## DataAdapter对象的常用方法

| 方法 | 说明 |
| :--- | :--- |
| Fill | 向DataSet中填充数据，并创建一个DataTable |
| FillSchema | 向指定的DataSet添加一个DataTable |
| Update | 将DataSet中修改的数据写回数据源 |

```
’创建数据库适配器对象，从Student表中查询所有信息‘
Dim sda As SqlDataAdapter  = New SqlDataAdapter (sqlstr,conn)

'创建数据集对象'
Dim ds As DataSet = New DataSet()

'通过数据适配器将数据填充到DataSet中'
sda.Fill(ds);

'通过GridView控件，在界面上显示数据集中的内容'
GridView1.DataSource = ds
GridView1.DataBind();
```

---

## 调用存储过程

```
创建存储过程
create procedure p_selectDept
    @dept varchar(20)
as
    select * from student where sdept = @dept


··
'设置要执行存储的名称'
Dim sda As SqlDataAdapter = New SqlDataAdapter("p_selectDept",conn)

'设置命令对象的类型'
sda.SelectCommand.CommandType = CommandType.StoredProcedure

'添加存储过程中的参数'
sda.SelectCommand.Parameters.Add("@dept",SqlDbType.VarChar,20).Value = TxtDept.Text.ToString()

Dim ds As DataSet = New DataSet()
sda.Fill(ds)

GridView1.DataSource = ds
GridView1.DataBind()
```




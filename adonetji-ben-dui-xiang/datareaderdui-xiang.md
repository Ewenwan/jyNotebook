DataReader对象用于从数据库中读取仅向前的只读数据流。通过DataReader对象读取的数据，在内存中一次只存放一行，从而减轻了系统对内存的需求，提高了程序性能；DataReader通过Command对象的ExecuteReader\(\)方法的返回值获得，通过自身的Read\(\)方法实现数据的逐行读取

---

## DataReader对象的常用属性

| 属性 | 说明 |
| :--- | :--- |
| FieldCount | 获取字段的数目 |
| IsClosed | True表示DataReader关闭，False表示DataReader打开 |
| Item | 集合对象，获取或设置字段的内容，name为字段名，ordinal为字段序号，ordinal的起始值为0，表示第1行 |
| RecordsAffected | 获取执行sql命令后有多少行受到了影响 |

---

## DataReader对象的常用方法

| 方法 | 说明 |
| :--- | :--- |
| Close\(\) | 关闭 |
| GetBoolean\(ordinal\) | 获取ordinal+1列的内容，返回值为Boolean类型 |
| GetByte\(ordinal\) | 获取ordinal+1列的内容，返回值为Byte类型 |
| GetDataTypeName\(ordinal\) | 获取ordinal+1列的数据类型名称 |
| GetFieldType\(ordinal\) | 获取ordinal+1列的数据类型 |
| GetName\(ordinal\) | 获取ordinal+1列的字段名称 |
| Read\(\) | 读取下一条数据，返回True表示还有下一条数据，否则表示数据读取完毕 |

```
Dim comm As SqlCommand = New SqlCommand(sqlstr, conn)
Dim dr As SqlDataReader = comm.ExecuteReader
If dr.Read Then
   cname.Text = dr("cname")
   credit.Text = dr("credit")
   semester.Text = dr("semester")
   
   

’下拉列表‘
while(dr.Read)
{
   this.DropDownList1.Items.Add(dr("sname").ToString())
}
```




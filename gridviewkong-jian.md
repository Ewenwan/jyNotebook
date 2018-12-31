* GridView控件以表格的形式在页面显示数据

GridView有两个用于绑定数据源的属性:DataSourceID和DataSource

---

## GridView控件的常用属性

| 属性 | 说明 |
| :--- | :--- |
| AllowPaging | 指定是否启用分页 |
| AllowSorting | 指定是否启用排序 |
| AlternatingRowStyle | 设置GridView控件中的交替数据行外观 |
| Columns | 获取GridView中显示的字段集合 |
| DataKeyNames | 获取或设置GridView中主键字段的名称 |
| DataKeys | 获取GridView中的每一行的主键值 |
| EditIndex | 获取或设置要编辑的行的索引 |
| PageCount | 获取要显示的总页数 |
| PageIndex | 获取或设置当前页的索引 |
| PageSize | 获取或设置每页显示的行数 |
| SelectedDataKey | 获取选中行的主键 |
| SelectedIndex | 获取选中行的索引 |
| SelectedRow | 获取选中的行 |
| SelectedValue | 获取选中的行的键值 |
| SortExpression | 获取排序表达式 |
| ShowFooter | 指定是否显示脚注 |
| ShowHeader | 指定是否显示标题 |

---

## GridView控件的常用方法

| 方法 | 说明 |
| :--- | :--- |
| FindControl | 在当前的容器中搜索服务器控件 |
| HasControls | 确定服务器控件是否包含子控件 |
| Sort | 排序 |

---

## GridView控件的常用事件

| 事件 | 说明 |
| :--- | :--- |
| PageIndexChanged | 页面索引变化之后 |
| PageIndexChanging | 页面索引变化之前 |
| PreRender | 加载Control之后，呈现之前的状态 |
| RowCancelingEdit | 编辑模式中，单击某一行"取消"按钮后 |
| RowCommand | 单击GridView控件的按钮时 |
| RowCreated | 创建行时 |
| RowDataBound | 数据行绑定数据时 |
| RowDeleted | 单击某一行"删除按钮"，使某一行删除后 |
| RowDeleting | 单击某一行"删除"按钮，再某一行删除前 |
| RowEditing | 单击某一行"编辑"按钮 |
| RowUpadted | 单击某一行"更新"按钮，使某一行更新后 |
| RowUpdating | 单击某一行"更新"按钮，使某一行更新前 |
| SelectedIndexChanged | 单击某一行"选择"按钮，处理相应选择操作后 |
| SelectedIndexChanging | 单击某一行"选择"按钮，处理相应选择操作前 |
| Sorted | 单击列排序超链接，排序操作处理后 |
| Sorting | 单击列排序超链接，排序操作处理前 |

```
    Protected Sub GridView1_PageIndexChanging(ByVal sender As Object, ByVal e As System.Web.UI.WebControls.GridViewPageEventArgs) Handles GridView1.PageIndexChanging
        GridView1.PageIndex = e.NewPageIndex
        Dim sqlstr As String = "select a.sno,b.sname,a.cno,c.cname,a.grade from sc a,studetn b,course c where a.sno=b.sno and a.cno=c.cno and a.sno like '" & TextBox1.Text & "%' and c.cname like'" & TextBox2.Text & "%'"
        Dim dp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
        Dim dt As DataSet = New DataSet
        dp.Fill(dt)
        GridView1.DataSource = dt
        GridView1.DataBind()

    End Sub
```

---

## 其他控件

DataList控件:该控件默认以表格形式显示数据

DetailsView控件:该控件采用表格布局，可以依次显示，编辑，删除或插入记录，通常用于更新和插入新数据

FormView控件:该控件可以自动对数据进行进行分页，一次显示一条记录的内容

Repeater控件:该控件没有内置的显示功能，必须通过创建模板来控件Repeater的布局

DropViewList控件:下拉列表

```
# 获取下拉列表值
Dim sdept As String = DropDownList1.SelectedValue
```

---

```
# 更换数据源
Dim f As String = DropDownList1.SelectedValue
Dim sqlstr As String = "select * from employment where flag='" + f + "'"
Dim dp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
Dim dt As DataSet = New DataSet
dp.Fill(dt)
GridView1.DataSource = dt
GridView1.DataBind()



Dim sdept As String = DropDownList1.SelectedValue
'Response.Write("<script>alert('" + sdept + "')</script>")'
Dim sqlstr As String = "select * from graduation where gdepartment= '" & sdept & "'"
'更换GridView的数据库命令'
SqlDataSource1.SelectCommand = sqlstr
```




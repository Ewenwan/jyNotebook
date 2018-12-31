```
Course_update.aspx


<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Course_update.aspx.vb" Inherits="Course_update" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <script type="text/javascript" src="JS/jquery-1.8.2.min.js"></script>
    <script type="text/ecmascript" src="Scripts/jquery-1.4.1-vsdoc.js"></script>
    <script type="text/javascript" src="Scripts/jquery-1.4.1.js"></script>
    <script type="text/javascript" src="Scripts/jquery-1.4.1.min.js"></script>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <table cellpadding=0 cellspacing=0>
            <tr>
                <td width="100px">课程号</td>
                <td width="140px"><asp:TextBox ID="cno" runat="server"></asp:TextBox></td>
                <td width="100px"><asp:Label ID="Label1" runat="server" Text="课程名"></asp:Label></td>
                <td width="140px"><asp:TextBox ID="cname" runat="server"></asp:TextBox></td>
            </tr>
            <tr>
            <td width="100px"><asp:Label ID="Label2" runat="server" Text="学分"></asp:Label></td>
            <td width="140px"><asp:TextBox ID="credit" runat="server"></asp:TextBox>
                <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ErrorMessage="不能为空" ControlToValidate="credit" Display="Dynamic"></asp:RequiredFieldValidator>
                <asp:CompareValidator ID="CompareValidator1" runat="server" ErrorMessage="必须为数字" ControlToValidate="credit" Type="Integer" Operator="DataTypeCheck" Display="Dynamic"></asp:CompareValidator>
            </td>
                <td width="100px">学期</td>
                <td width="140px"><asp:TextBox ID="semester" runat="server"></asp:TextBox></td>
            </tr>
            <tr>
                <td colspan="4" align="right"><asp:Button ID="Button1" runat="server" Text="提交"/></td>
            </tr>
        </table>
        <asp:HiddenField ID="HiddenField1" runat="server"/>
    </div>
    </form>
</body>
</html>
```

```
Coures_update.aspx.vb


Imports System.Web.Configuration
Imports System.Data.SqlClient

'利用隐藏的输入框，将value值保存，这样就可以全部进行修改'

Partial Class Course_update
    Inherits System.Web.UI.Page
    Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        'Response.Write("<script>alert(1)</script>")'
        If Not IsPostBack Then
            If Not Request.QueryString("cno") Is Nothing Then
                cno.Text = Request.QueryString("cno".ToString)
                HiddenField1.Value = cno.Text.Trim
                Dim conn As SqlConnection = New SqlConnection(connstr)
                conn.Open()
                Dim sqlstr As String = "select * from course where cno = '" & Request.QueryString("cno").ToString & "'"
                Dim comm As SqlCommand = New SqlCommand(sqlstr, conn)
                Dim dr As SqlDataReader = comm.ExecuteReader
                If dr.Read Then
                    cname.Text = dr("cname")
                    credit.Text = dr("credit")
                    semester.Text = dr("semester")
                End If
                conn.Close()
            End If
        End If
    End Sub

    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        If cno.Text.Trim <> "" And cname.Text.Trim <> "" And credit.Text.Trim <> "" And semester.Text.Trim <> "" Then
            Dim conn As SqlConnection = New SqlConnection(connstr)
            Try
                conn.Open()
                Dim sqlstr As String = "update course set cno='" & cno.Text.Trim & "',cname='" & cname.Text.Trim & "',credit='" & credit.Text.Trim & "',semester='" & semester.Text.Trim & "' where cno='" & HiddenField1.Value & "'"
                Dim com As SqlCommand = New SqlCommand(sqlstr, conn)
                '更新执行操作'
                com.ExecuteScalar()
                '使用 ExecuteScalar 方法从数据库中检索单个值（例如一个聚合值）。与使用 ExecuteReader 方法，然后使用 SqlDataReader 返回的数据执行生成单个值所需的操作相比，此操作需要的代码较少'
                Response.Write("<script>alert('更新成功')</script>")
                conn.Close()
            Catch ex As Exception
                Response.Write(ex.ToString)
            Finally
                conn.Close()
                Response.Redirect("Course_list.aspx")
            End Try
        End If
    End Sub
End Class
```




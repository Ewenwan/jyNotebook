Student\_insert.aspx.vb实例

```
Imports System.Data.SqlClient
Imports System
Imports System.Web
Imports System.Web.UI

Partial Class Student_insert
    Inherits System.Web.UI.Page
    Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"

    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        '接收表单'

        Dim sno As String = Request.Form("sno")
        Dim sname As String = Request.Form("sname")
        Dim ssex As String = Request.Form("ssex")
        Dim sage As String = Request.Form("sage")
        Dim sdept As String = Request.Form("sdept")
        '连接字符串'
        'Dim connstr As String ="Data Source=(local);Initial Catalog=student;User ID=miku;Password=123456";'

        '创建联接对象'
        Dim conn As SqlConnection = New SqlConnection(connstr)
        Try
            '打开联接'
            conn.Open()
            '生成sql语句'
            Dim sqlstr As String = "insert into student values ('" & sno & "','" & sname & "','" & ssex & "'," & sage & ",'" & sdept & "')"
            'Response.Write(sqlstr)'

            ''创建命令对象'
            Dim sqlcom As SqlCommand = New SqlCommand(sqlstr, conn)
            sqlcom.ExecuteNonQuery()
            'Response.Write("<script>alert('删除成功')</script>")'
            conn.Close()
        Catch ex As Exception
            Response.Write(ex.ToString)
        Finally
            conn.Close()
        End Try
    End Sub
End Class
```

## student\_index.aspx实例

```
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Student_insert.aspx.vb" Inherits="Student_insert" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
         <table cellpadding=0 cellspacing=0>
                <tr>
                    <td width="100px">学号</td>
                    <td width="140px"><asp:TextBox ID="sno" runat="server"></asp:TextBox></td>
                    <td width="100px"><asp:Label ID="Label1" runat="server" Text="姓名"></asp:Label></td>
                    <td width="140px"><asp:TextBox ID="sname" runat="server"></asp:TextBox></td>
                </tr>
                <tr>
                    <td width="100px"><asp:Label ID="Label2" runat="server" Text="性别"></asp:Label></td>
                    <td width="140px"><asp:TextBox ID="ssex" runat="server"></asp:TextBox></td>
                    <td width="100px">年龄</td>
                    <td width="140px"><asp:TextBox ID="sage" runat="server"></asp:TextBox></td>
                </tr>
                <tr>
                    <td>系别</td>
                    <td><asp:TextBox ID="sdept" runat="server" ></asp:TextBox></td>
                    <td colspan="2" align="right"><asp:Button ID="Button1" runat="server" Text="提交"/></td>
                </tr>
            </table>
        </div>
    </form>
</body>
</html>
```

---

## 




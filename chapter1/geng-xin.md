## student\_update.aspx.vb实例

```
Imports System.Data.SqlClient

Partial Class Student_update
    Inherits System.Web.UI.Page
    Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        Dim conn As SqlConnection = New SqlConnection(connstr)
        Try
            conn.Open()
            Dim sqlstr As String = "update student set sname='" & sname.Text & "',ssex='" & ssex.Text & "',sage='" & sage.Text & "',sdept='" & sdept.Text & "' where sno='" & sno.Text & "'"
            Dim com As SqlCommand = New SqlCommand(sqlstr, conn)
            Response.Write(sqlstr)
            com.ExecuteScalar()

           ' Response.Write("<script>alert('更新成功')</script>")'
            conn.Close()
        Catch ex As Exception
            Response.Write(ex.ToString)
        Finally
            conn.Close()
        End Try
    End Sub

    '页面载入时读取数据'
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        If Not IsPostBack Then
            If Not Request.QueryString("sno") Is Nothing Then
                '连接字符串'
                Dim conn As SqlConnection = New SqlConnection(connstr)
                conn.Open()
                Dim sqlstr As String = "select * from student where sno='" & Request.QueryString("sno").ToString & "'"
                Dim com As SqlCommand = New SqlCommand(sqlstr, conn)
                Dim sreader As SqlDataReader = com.ExecuteReader
                If sreader.Read Then
                    sno.Text = sreader("sno")
                    sname.Text = sreader("ssex")
                    sage.Text = sreader("sage")
                    sdept.Text = sreader("sdept")
                End If
                conn.Close()
            End If
        End If
    End Sub
End Class
```

## student\_update.aspx实例

```
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Student_update.aspx.vb" Inherits="Student_update" %>

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
                <td width="140px"><asp:TextBox ID="sno" runat="server" Enabled="False"></asp:TextBox></td>
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
                <td><asp:TextBox ID="sdept" runat="server"></asp:TextBox></td>
                <td colspan="2" align="right"><asp:Button ID="Button1" Text="提交" runat="server" /></td>
            </tr>
        </table>
    </div>
    </form>
</body>
</html>
```

效果图:![](/assets/update_student.png)




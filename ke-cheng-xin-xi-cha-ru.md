```
Course_insert.aspx


<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Course_insert.aspx.vb" Inherits="Course_insert" %>

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
                     <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" 
                            ErrorMessage="不能为空" ControlTovalidate="credit" Display="Dynamic"></asp:RequiredFieldValidator>
                        <asp:CompareValidator ID="CompareValidator1" runat="server" ErrorMessage="必须为数字" ControlToValidate="credit" Operator="DataTypeCheck" Display="Dynamic" Type="Integer"></asp:CompareValidator>
                    </td>
                    <td width="100px">学期</td>
                    <td width="140px"><asp:TextBox ID="semester" runat="server"></asp:TextBox></td>
                </tr>
                <tr>
                    <td colspan="4" align="right"><asp:Button ID="Button1" runat="server" Text="提交"/></td>
                </tr>
            </table>
        </div>
    </div>
    </form>
</body>
</html>
```

```
Course_insert.aspx.vb



Imports System.Web.Configuration
Imports System.Data.SqlClient

Partial Class Course_insert
    Inherits System.Web.UI.Page
    '获取数据库配置信息'
    'Private strcon As String = WebConfigurationManager.ConnectionStrings("studentConnectionString").ConnectionString'
    'Data Source=服务名称;Initial Catalog=数据库名称;Integrated Security=True---本地验证'
    Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        Dim cno As String = Request.Form("cno")
        Dim cname As String = Request.Form("cname")
        Dim credit As String = Request.Form("credit")
        Dim semester As String = Request.Form("semester")
        '连接数据库'
        Dim conn As SqlConnection = New SqlConnection(connstr)
        Try
            conn.Open()
            Dim sqlstr As String = "insert into course values('" & cno & "','" & cname & "'," & credit & "," & semester & ")"
            Dim comm As SqlCommand = New SqlCommand()
            comm.Connection = conn
            comm.CommandText = sqlstr
            comm.ExecuteNonQuery()
            Response.Write("<script>alert('增加成功')</script>")
            conn.Close()
        Catch ex As Exception
            Response.Write(ex.ToString)
        Finally
            conn.Close()
            Response.Redirect("Course_list.aspx")
        End Try
    End Sub
End Class
```




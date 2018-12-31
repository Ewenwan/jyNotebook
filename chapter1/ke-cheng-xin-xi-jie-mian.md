## course\_list.aspx.vd实例

```
Imports System.Data.SqlClient
Imports System.Data

Partial Class Course_list
    Inherits System.Web.UI.Page
    Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        Dim sqlstr As String = "select * from course where cno like'" & cno.Text.Trim & "%' and cname like '" & cname.Text & "%'"
        Dim sp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
        Dim ds As DataSet = New DataSet
        sp.Fill(ds)
        GridView1.DataSource = ds
        GridView1.DataBind()
    End Sub

    Protected Sub Button2_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button2.Click
        Response.Write("<script>window.onload=function(){ShowArtDlg('增加课程信息','course_insert.aspx','600px','200px','true');}</script>")
    End Sub

    Protected Sub Button3_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button3.Click
        If GridView1.SelectedIndex >= 0 Then
            Dim cno As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(1).Text
            Response.Write("<script>window.onload=function(){ShowArtDlg('修改课程信息','course_update.aspx?cno=" & cno & "','600px','200px','true');}</script>")
        End If
    End Sub

    Protected Sub Button4_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button4.Click
        If GridView1.SelectedIndex >= 0 Then
            Dim cno As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(1).Text
            Dim sqlstr As String = "delete from course where cno'" & cno & "'"
            Dim conn As SqlConnection = New SqlConnection(connstr)
            Try
                conn.Open()
                Dim sqlcom As SqlCommand = New SqlCommand(sqlstr, conn)
                sqlcom.ExecuteNonQuery()
                Response.Write("<script>alert('删除成功')</script>")
                Button1_Click(Nothing, Nothing)
                conn.Close()
            Catch ex As Exception
                Response.Write(ex.ToString)
            Finally
                conn.Close()
            End Try
        End If
    End Sub

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        If Not IsPostBack Then
            Dim Sqlstr As String = "select * from course"
            Dim sp As SqlDataAdapter = New SqlDataAdapter(Sqlstr, connstr)
            Dim ds As DataSet = New DataSet
            sp.Fill(ds)
            GridView1.DataSource = ds
            GridView1.DataBind()
        End If
    End Sub
End Class
```

## course\_list.aspx实例

```
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Course_list.aspx.vb" Inherits="Course_list" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <table>
            <tr>
                <td>
                    <table>
                        <tr>
                            <td>
                                <asp:Label ID="Label1" runat="server" Text="课程号"></asp:Label>
                            </td>
                            <td>
                                <asp:TextBox ID="cno" runat="server"></asp:TextBox>
                            </td>
                            <td>
                                <asp:Label ID="Label2" runat="server" Text="课程名"></asp:Label>
                            </td>
                            <td>
                                <asp:TextBox ID="cname" runat="server"></asp:TextBox>
                            </td>
                            <td>
                                <asp:Button ID="Button1" runat="server" Text="查询" />
                            </td>
                        </tr>
                    </table>
                </td>
            </tr>
            <tr>
                <td>
                    <asp:Button ID="Button2" runat="server" Text="新增"/>
                    <asp:Button ID="Button3" runat="server" Text="修改"/>
                    <asp:Button ID="Button4" runat="server" Text="删除"/>
                </td>
            </tr>
        </table>
        <asp:GridView ID="GridView1" runat="server" AllowPaging="True" 
            AllowSorting="True" AutoGenerateColumns="False" DataKeyNames="Cno" 
            DataSourceID="SqlDataSource1">
            <Columns>
                <asp:CommandField ShowSelectButton="True" />
                <asp:BoundField DataField="Cno" HeaderText="Cno" ReadOnly="True" 
                    SortExpression="Cno" />
                <asp:BoundField DataField="Cname" HeaderText="Cname" SortExpression="Cname" />
                <asp:BoundField DataField="Credit" HeaderText="Credit" 
                    SortExpression="Credit" />
                <asp:BoundField DataField="Semester" HeaderText="Semester" 
                    SortExpression="Semester" />
            </Columns>
        </asp:GridView>
        <asp:SqlDataSource ID="SqlDataSource1" runat="server" 
            ConnectionString="<%$ ConnectionStrings:学生数据库ConnectionString %>" 
            SelectCommand="SELECT * FROM [Course]"></asp:SqlDataSource>
    </form>
</body>
</html>
```




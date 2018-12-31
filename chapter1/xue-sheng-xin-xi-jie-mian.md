```
Student_list.aspx


<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Student_list.aspx.vb" Inherits="Student_list" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <style type="text/css">
        .style1
        {
            width: 540px;
        }
    </style>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <table>
            <tr>
                <td class="style1">
                    <table>
                        <tr>
                           <td>
                               <asp:Label ID="Label1" runat="server" Text="学号"></asp:Label>
                           </td>
                           <td>
                               <asp:TextBox ID="sno" runat="server"></asp:TextBox>
                           </td>
                           <td>
                               <asp:Label ID="Label2" runat="server" Text="系别"></asp:Label>
                           </td>
                           <td>
                               <asp:TextBox ID="sdept" runat="server"></asp:TextBox>
                           </td>
                           <td>
                               <asp:Button ID="Button1" runat="server" Text="查询" />
                           </td>
                        </tr>
                    </table>
                </td>
            </tr>
            <tr>
                <td class="style1">
                    <asp:Button ID="Button2" runat="server" Text="新增"/>
                    <asp:Button ID="Button3" runat="server" Text="修改"/>
                    <asp:Button ID="Button4" runat="server" Text="删除"/>
                </td>
            </tr>
            <tr>
                <td class="style1">
                    <asp:GridView ID="GridView1" runat="server" AllowPaging="True" 
                        AllowSorting="True" AutoGenerateColumns="False" BackColor="White" 
                        BorderColor="#CCCCCC" BorderStyle="None" BorderWidth="1px" CellPadding="3" 
                        DataKeyNames="Sno" DataSourceID="SqlDataSource1" style="margin-right: 0px" 
                        Width="447px">
                        <Columns>
                            <asp:CommandField ShowSelectButton="True" />
                            <asp:BoundField DataField="Sno" HeaderText="Sno" ReadOnly="True" 
                                SortExpression="Sno" />
                            <asp:BoundField DataField="Sname" HeaderText="Sname" SortExpression="Sname" />
                            <asp:BoundField DataField="Ssex" HeaderText="Ssex" SortExpression="Ssex" />
                            <asp:BoundField DataField="Sage" HeaderText="Sage" SortExpression="Sage" />
                            <asp:BoundField DataField="Sdept" HeaderText="Sdept" SortExpression="Sdept" />
                        </Columns>
                        <FooterStyle BackColor="White" ForeColor="#000066" />
                        <HeaderStyle BackColor="#006699" Font-Bold="True" ForeColor="White" />
                        <PagerStyle BackColor="White" ForeColor="#000066" HorizontalAlign="Left" />
                        <RowStyle ForeColor="#000066" />
                        <SelectedRowStyle BackColor="#669999" Font-Bold="True" ForeColor="White" />
                        <SortedAscendingCellStyle BackColor="#F1F1F1" />
                        <SortedAscendingHeaderStyle BackColor="#007DBB" />
                        <SortedDescendingCellStyle BackColor="#CAC9C9" />
                        <SortedDescendingHeaderStyle BackColor="#00547E" />
                    </asp:GridView>
                    <asp:SqlDataSource ID="SqlDataSource1" runat="server" 
                        ConnectionString="<%$ ConnectionStrings:学生数据库ConnectionString %>" 
                        SelectCommand="SELECT * FROM [Student]"></asp:SqlDataSource>
                </td>
            </tr>
        </table>
    </div>
    </form>
</body>
</html>
```





```
Student_list.aspx.vb


Imports System.Data.SqlClient
Partial Class Student_list
    Inherits System.Web.UI.Page
    Dim connstr As String = "Data Source=(local);Initial Catalog=student;Integrated Security=True"
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        Dim sqlstr As String = "select * from student where sno like '" & sno.Text.Trim & "%' and sdept like '" & sdept.Text.Trim & "%'"
    End Sub

    Protected Sub Button2_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button2.Click
        'Response.Write("<script>window.open('student_insert.aspx')</script>")'
        Response.Write("<script>window.onload=function() {ShowArtDig('增加学生信息','student_insert.aspx','600px','200px','true');}</script>")
    End Sub

    Protected Sub Button3_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button3.Click
        If GridView1.SelectedIndex >= 0 Then
            Dim sno As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(1).Text
            Response.Write("<script>window.onload=function(){ShowArtDlg('修改学生信息','student_update.aspx?sno=" & sno & "','600px','200px','true');}</script>")
            'Response.Write("<script>window.open('student_update.aspx?sno="& sno &"');</script>")'
        End If
    End Sub

    Protected Sub Button4_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button4.Click
        If GridView1.SelectedIndex >= 0 Then
            Dim sno As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(1).Text
            Dim sqlstr As String = "delete from student where sno '=" & sno & "'"
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
End Class

```




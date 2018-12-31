```
Sc_list.aspx

<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Sc_list.aspx.vb" Inherits="Sc_list" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <table>
            <tr>
                <td>学号</td>
                <td width="140px"><asp:TextBox ID="TextBox1" runat="server"></asp:TextBox></td>
                <td>课程</td>
                <td width="140px"><asp:TextBox ID="TextBox2" runat="server"></asp:TextBox></td>
                <td><asp:Button ID="Button1" runat="server" Text="查询"/></td>
            </tr>
            <tr>
                <td>学号</td>
                <td width="140px">
                    <asp:DropDownList ID="DropDownList1" runat="server" Width="100px" 
                        DataSourceID="SqlDataSource2" DataTextField="Sname" DataValueField="Sno">
                    </asp:DropDownList>
                    <!-- 'select distinct 列 from 表，选取不重复行' -->
                    <asp:SqlDataSource ID="SqlDataSource2" runat="server" 
                        ConnectionString="<%$ ConnectionStrings:学生数据库ConnectionString %>" 
                        SelectCommand="SELECT [Sname], [Sno] FROM [Student]"></asp:SqlDataSource>
                </td>

                <td>课程</td>
                <td width="140px">
                    <asp:DropDownList DataSourceID="SqlDataSource3" ID="DropDownList2" 
                        runat="server" DataTextField="Cname" DataValueField="Cno">
                </asp:DropDownList>
                <asp:SqlDataSource ID="SqlDataSource3" runat="server" 
                        ConnectionString="<%$ ConnectionStrings:学生数据库ConnectionString %>" 
                        SelectCommand="SELECT [Cno], [Cname] FROM [Course]"></asp:SqlDataSource>
                </td>
                <td><asp:Button ID="Button2" runat="server" Text="选课"/></td>
             </tr>
             <tr>
              <!--添加选择栏 <asp:CommandField ShowSelectButton="True" />-->
                <td colspan="5">
                    <asp:Button ID="Button3" runat="server" Text="删除"/>
                    <asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" 
                        DataKeyNames="Sno,Cno" BackColor="LightGoldenrodYellow" BorderColor="Tan" 
                        BorderWidth="1px" CellPadding="2" ForeColor="Black" GridLines="None">
                        <AlternatingRowStyle BackColor="PaleGoldenrod" />
                        <Columns>
                            <asp:CommandField ShowSelectButton="True" />
                            <asp:BoundField DataField="Sno" HeaderText="Sno" ReadOnly="True" 
                                SortExpression="Sno" />
                            <asp:BoundField DataField="Cno" HeaderText="Cno" ReadOnly="True" 
                                SortExpression="Cno" />
                            <asp:BoundField DataField="Grade" HeaderText="Grade" SortExpression="Grade" />
                        </Columns>
                        <FooterStyle BackColor="Tan" />
                        <HeaderStyle BackColor="Tan" Font-Bold="True" />
                        <PagerStyle BackColor="PaleGoldenrod" ForeColor="DarkSlateBlue" 
                            HorizontalAlign="Center" />
                        <SelectedRowStyle BackColor="DarkSlateBlue" ForeColor="GhostWhite" />
                        <SortedAscendingCellStyle BackColor="#FAFAE7" />
                        <SortedAscendingHeaderStyle BackColor="#DAC09E" />
                        <SortedDescendingCellStyle BackColor="#E1DB9C" />
                        <SortedDescendingHeaderStyle BackColor="#C2A47B" />
                    </asp:GridView>
                    <asp:SqlDataSource ID="SqlDataSource1" runat="server" 
                        ConnectionString="<%$ ConnectionStrings:学生数据库ConnectionString %>" 
                        SelectCommand="SELECT * FROM [SC]"></asp:SqlDataSource>
                </td>
             </tr>
        </table>
    </div>
    </form>
</body>
</html>
```



```
Sc_list.aspx.vb

Imports System.Data
Imports System.Data.SqlClient
Imports System.Web.Configuration

Partial Class Sc_list
    Inherits System.Web.UI.Page
    Dim connstr As String = "Data Source=DESKTOP-A2E0KFM\MYSQLEXPRESS;Initial Catalog=学生数据库;Integrated Security=True"
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        If Not IsPostBack Then
            Dim sqlstr As String = "select a.sno,b.sname,a.cno,c.cname,a.grade from sc a,student b,course c where a.sno=b.sno and a.cno = c.cno"
            Dim dp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
            Dim dt As DataSet = New DataSet
            dp.Fill(dt)
            GridView1.DataSource = dt
            GridView1.DataBind()

        End If
    End Sub

    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        Dim sqlstr As String = "select a.sno,b.sname,a.cno,c.cname,a.grade from sc a,student b, course c where a.sno=b.sno and a.cno=c.cno and a.sno like '" & TextBox1.Text & "%' and c.cname like '" & TextBox2.Text & "%'"
        Dim dp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
        Dim dt As DataSet = New DataSet
        dp.Fill(dt)
        GridView1.DataSource = dt
        GridView1.DataBind()
    End Sub

    Protected Sub Button2_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button2.Click
        '读取选中的值'
        Dim sno As String = DropDownList1.SelectedValue
        Dim cno As String = DropDownList2.SelectedValue

        If sno <> "" And cno <> "" Then
            Dim conn As SqlConnection = New SqlConnection(connstr)
            conn.Open()
            Dim sqlstr As String = "insert into sc(sno,cno) values ('" & sno & "','" & cno & "')"
            Dim comm As SqlCommand = New SqlCommand(sqlstr, conn)
            comm.ExecuteNonQuery()
            'Response.Write("<script>alert('选课成功')</script>")'
            Response.Write(sqlstr)
            conn.Close()
            Button1_Click(Nothing, Nothing)
        End If

    End Sub

    Protected Sub Button3_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button3.Click
        If GridView1.SelectedIndex >= 0 Then
            'GridView.Rows.Item(GridView.SelectedIndex).Cells(index).Text 获取索引的第一个字'
            Dim sno As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(1).Text
            Dim cno As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(2).Text
            'Dim grade As String = GridView1.Rows.Item(GridView1.SelectedIndex).Cells(3).Text '
            Dim sqlstr As String = "delete from sc where sno='" & sno & "' and cno='" & cno & "'"
            Dim conn As SqlConnection = New SqlConnection(connstr)
            Try
                conn.Open()
                Dim sqlcom As SqlCommand = New SqlCommand(sqlstr, conn)
                sqlcom.ExecuteNonQuery()
                Response.Write(sqlstr)
                'Response.Write("<script>alert('删除成功')</script>")'
                Button1_Click(Nothing, Nothing)
                conn.Close()
            Catch ex As Exception
                Response.Write(ex.ToString)
            Finally
                conn.Close()
            End Try
        End If
    End Sub

    Protected Sub GridView1_PageIndexChanging(ByVal sender As Object, ByVal e As System.Web.UI.WebControls.GridViewPageEventArgs) Handles GridView1.PageIndexChanging
        GridView1.PageIndex = e.NewPageIndex
        Dim sqlstr As String = "select a.sno,b.sname,a.cno,c.cname,a.grade from sc a,studetn b,course c where a.sno=b.sno and a.cno=c.cno and a.sno like '" & TextBox1.Text & "%' and c.cname like'" & TextBox2.Text & "%'"
        Dim dp As SqlDataAdapter = New SqlDataAdapter(sqlstr, connstr)
        Dim dt As DataSet = New DataSet
        dp.Fill(dt)
        GridView1.DataSource = dt
        GridView1.DataBind()

    End Sub
End Class

```




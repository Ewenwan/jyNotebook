```
default.aspx


<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <!--link type="text/css" href="Styles/Site.css"/-->
    <script src="JS/jquery-1.8.2.min.js" type="text/javascript"></script>
    <script src="Scripts/jquery-1.4.1-vsdoc.js" type="text/javascript"></script>
    <script src="Scripts/jquery-1.4.1.js" type="text/javascript"></script>
    <script src="Scripts/jquery-1.4.1.min.js" type="text/javascript"></script>
    <style type="text/css">
            .nav1{
        width:150px;
        height:100%;
        margin-top:100px;
    }
    .nav2
    {
        border:1px soild blue;
        margin-top:-80px;
        position:absolute;
        left:35%;
        }
       .nav2 iframe
       {
            border:1px soild blue;
           width:600px;
           height:600px;
           }
        .top h1
        {
            text-align:center;
               position:absolute;
               top:0;
               width:100%;
            font-family:"楷体";
            }
            
           .foot
           {
               position:absolute;
               bottom:0;
               width:100%;
               }
    </style>
</head>
<body>
    <div class="main">
        <div class="top">
            <h1>学生选课管理系统</h1>
        </div>
        <div class="center">
            <div class="nav1">
                <ul>
                    <li><a href="Course_list.aspx" target="myframe">课程管理</a></li>
                    <li><a href="student_list.aspx" target="myframe">学生管理</a></li>
                    <li><a href="Sc_list.aspx" target="myframe">选课管理</a></li>
                </ul>
            </div>
            <div class="nav2">
                <iframe id="myframe" name="myframe" frameborder="0" src="student_list.aspx"></iframe>
            </div>
        </div>
    </div>
           
        <div class="foot">
         <center><label style="width:30px;">悦心学生管理系统</label></center>
        </div>
                 
        </body>
</html>

```




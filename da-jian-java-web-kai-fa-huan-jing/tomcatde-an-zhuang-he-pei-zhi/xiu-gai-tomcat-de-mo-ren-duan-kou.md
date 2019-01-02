Tomcat的默认服务器的端口号为8080

---

修改Tomcat的配置文件修改其默认端口的步骤:

* 采用记事本打开Tomcat安装下的conf文件夹下的servlet.xml文件

![](/assets/2.png)

* 在servlet.xml文件中找到如下代码:![](/assets/3.png)

* 将上面的代码中的port="8080"修改为port="x",x为自己想修改的端口号，即可将Tomcat的默认端口设置为x

_**tips:**_在修改端口时，注意避免与公用端口冲突。一般使用默认的8080端口


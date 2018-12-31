## Request对象的常用属性

| 属性 | 说明 |
| :--- | :--- |
| ApplicationPath | 获取服务器上的ASP.NET应用程序的虚拟目录 |
| ClientCertificate | 获取客户端安全认证信息 |
| Browser | 获取或设置客户端浏览器的功能信息 |
| Form | 获取表单变量的集合（post请求） |
| QueryString | 获取HTTP查询字符串变量的集合（get请求） |
| TotalBytes | 获取当前输入流中的字节数 |
| Url | 获取有关当前请求的URL信息 |
| Path | 获取当前情趣的相对地址 |
| PhysicalPath | 获取当前请求的网页的真实路径 |
| UserHostAdress | 获取客户端的主机ip地址 |
| UserHostName | 获取客户端的主机名 |

---

## Request对象的常用方法

| BinaryRead | 以二进制方式读取当前输入流中指定字节数的数据 |
| :--- | :--- |
| MapPath\(path\) | 将当前请求的URL中的虚拟路径映射到服务器上的物理路径 |
| SaveAs\(path,true\|false\) | 将HTTP请求的信息保存到磁盘中 |




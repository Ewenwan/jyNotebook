* Web.config文件是一个xml文本文件，应用程序的每一个目录中都可以有web.config文件。
* 所有配置信息都在&lt;configuration&gt;和&lt;/configuration&gt;根元素之间。
* 应用程序的全局常量等信息在&lt;appSetting&gt;和&lt;/appSettings&gt;标记之间定义。
* 在&lt;connectionStrings&gt;和&lt;/connectionStrings&gt;标记之间用于定义数据库连接字符串。
* 在&lt;system.web&gt;和&lt;/system.web&gt;标记之间用来配置应用程序所需要的不同的环境参数

---

## 配置数据库连接字符串

### 数据库连接字符串的属性

| 属性 | 意义 |
| :--- | :--- |
| Data Source\(server\) | 指定数据源\(服务器\)的名称 |
| Initial Catalog\(database\) | 指定数据库的名称 |
| User ID\(uid\) | 指定登录数据库服务器的用户名称 |
| Password\(pwd\) | 指定登录数据库服务器的用户命令 |
| Integrated Security | 指定连接是否是安全的 |

```
"Data Source=服务名称;Initial Catalog=数据库名称;User=用户名;Password=密码;Integrated Security=true;"
```




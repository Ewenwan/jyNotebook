Glocal.asax文件，也就是ASP.NET应用程序文件，包含用于响应ASP.NET或HTTPModule引发的应用程序级别事件的代码，位于ASP.NET应用程序的根目录下

---

## Global.asax文件中的基本事件

| 事件 | 作用 |
| :--- | :--- |
| Application\_Start | Application对象开始时，触发该事件。该事件中可以与整个应用程序相关的初始化工作 |
| Application\_End | Application对象结束时，触发该事件。该事件中可以进行与整个应用程序相关的信息的处理 |
| Application\_Error | 出现未处理错误时，触发该事件 |
| Session\_Start | Session对象开始时，触发该事件。该事件中可以进行单一用户相关的初始化工作 |
| Session\_End | Session对象结束时，触发该事件。该事件可以进行与单一用于相关的信息的处理 |

```
void Application_Start(Object sender,EventAges e)
{
    '处于全局状态下'
}
```




## HTML 本地存储对象

HTML 本地存储提供了两个客户端存储数据的对象:

* window.localStorge - 存储没有截止日期的数据
* window.sessionStorge - 针对一个session来存储数据\(当关闭浏览器标签页\)

_在使用本地存储时，要先检测localStorage和sessionStorage的浏览器支持_

```
if(typeof(Storage) != "undefined")
{
    //针对localStorage/sessionsStorage的代码
}else{
    //抱歉!不支持web storage
}
```

---

## localStorage对象

localStorage对象存储的是没有截止日期的数据。当浏览器被关闭时数据不会本删除，重新打开后能够使用

```HTML
<html>
    <head></head>
    <body>
        <div id="result"></div>
        <script>
            //check browser support
            if(typeof(Storage) !== "undefined")
            {
                //Store
                localStorage.setItem("lastname","angle");
                //Retrieve
                document.getElementById("result").innerHTML = localStorage.getItem("lastname");
            }
            else
                documnet.getElementById("result").innerHTML = "抱歉！浏览器不支持";
        </script>
    </body>
</html>
```

实例解释:

* localStorage 名称/值对,其中:name="lastname",value="angle"
* 取回"lastname"的值，并把它插到id="result"的元素中

```HTML
//存储
localStorage.lastname = "angle";
//取回
document.getElementById("result").innerHTML = localStorage.lastname;
```

删除"lastname"localStorage项目的语法如下:

```HTML
localStorage.removeItem("lastname");
```

实例:对用户点击按钮的次数进行计数

```HTML
<html>
    <head>
        <script>
            function clickCounter()
            {
                if(typeof(Storage)!=="undefined")
                {
                    if(localStorage.clickcount)
                        localStorage.clickcount = Number(localStorage.clickcount)+1;
                    else
                        localStorage.clickcount = 1;
                    document.getElementById("result").innerHTML = "点击这个按钮"+localStorage.clickcount+"次.";
                }
                else
                    document.getElementById("result").innerHTML = "浏览器不支持";
            }
        </script>
    </head>
    <body>
        <p><button onclick="clickCounter()" type="button">请点击这里</button></p>
        <div id="result"></div>
    </body>
</html>
```

---

## sessionStorage对象

sessionStorage对象等同localStorage,不同之处在于只对一个session存储数据。如果用户关闭具体的浏览器标签页,数据也会被删除

实例:在当前session中对用户点击按钮进行计数

```HTML
<html>
    <head>
        <script>
            function clickCounter()
            {
                if(typeof(Storage)!=="undefined")
                {
                   if (sessionStorage.clickcount)
                        sessionStorage.clickcount = Number(sessionStorage.clickcount)+1;
                    else
                        sessionStorage.clickcount = 1;
                    document.getElementById("result").innerHTML ="点击按钮"+sessionStorage.clickcount+"次";
                }
                else
                    document.getElementById("result").innerHTML = "不支持";
            }
        </script>
    </head>
    <body>
        <p><button onclick="clickCounter()" type="button">点击</button></p>
        <div id="result"></div>
    </body>
</html>
```




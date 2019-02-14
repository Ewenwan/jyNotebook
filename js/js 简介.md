## javascript是脚本语言

javascript是一种轻量级的编程语言

javascript是可插入HTML页面的编程代码

javascript插入HTML页面后，可由所有的现代浏览器执行

---

javascript:写入HTML输出

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <p>
            <script>
                document.write("<h1>angle</h1>");
            </script>
        </p>
    </body>
</html>
```

---

## JavsScript:对事件作出反应

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <button type="button" onclick="alert('你好')">点这里</button>
    </body>
</html>
```

---

## javascript:改变HTML内容

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <p id="demo">我没变</p>
        <script>
            function myFunction()
            {
                x = document.getElementById("demo");
                x.innerHTML="我变了";
            }
        </script>
        <button type="button" onclick="myFunction()">点这里</button>
    </body>
</html>
```

---

## javascript:改变HTML图像

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <script>
            function changeImage()
            {
                element=document.getElementById('myimage')
                if (element.src.match("eg_bulbon"))
                {
                    element.src = "http://www.w3school.com.cn//i/eg_bulboff.gif";
                }
                else
                {
                    element.src = "http://www.w3school.com.cn/i/eg_bulbon.gif";
                }
            }
        </script>
        <img id="myimage" onclick="changeImage()" src="http://www.w3school.com.cn//i/eg_bulboff.gif"/>
        <p>开关</p>
    </body>
</html>
```

---

### javascript:改变HTML样式

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <p id="demo">
            我目前没变颜色
        </p>
        <script>
            function myFunction()
            {
                x = document.getElementById("demo");
                x.style.color = "red";
            }
        </script>
        <button type="button" onclick="myFunction()">点了后文本颜色改变</button>
    </body>
</html>
```

---

## javascript:验证输入

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        输入如果的不是数字，浏览器会弹出提示框。
        <input type="text" id="demo" />
        <script>
            function myFunction()
            {
                var x = document.getElementById("demo").value;
                if(x==""||isNaN(x))
                    alert("Not Numeric");    
            }
        </script>
        <button type="button" onclick="myFunction()">点这里</button>
    </body>
</html>
```




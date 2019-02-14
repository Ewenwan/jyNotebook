_tips:函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块_

实例:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <script>
            function myFunction()
            {
                alert("Hello World")
            }
        </script>
    </head>
    <body>
        <button onclick="myFunction()">点击</button>        
    </body>

</html>
```

---

## javascript函数语法

函数包括在花括号中代码块，在函数名前使用function关键词

```
function functionname()
{
    这里是要执行的代码
}
```

---

## 调用带参数的函数

```
function myFunction(*args)
```

\*args代表至少有0个参数

---

## 带有返回值的参数

通过return语句实现,和c/c++一样

```
function myfunction()
{
    var x=5;
    return x;
}
```

```
var myVar = myfunction();
```

myVar变量的值是5，也是函数"myFunction\(\)"所返回的值

即使不把它保存为变量，您也可以使用返回值：

```
document.getElementById("demo").innerHTML=myFunction();
```

---

## 局部 JavaScript 变量

在 JavaScript 函数内部声明的变量（使用 var）是_局部_变量，所以只能在函数内部访问它。（该变量的作用域是局部的）。

可以在不同的函数中使用名称相同的局部变量，因为只有声明过该变量的函数才能识别出该变量。

只要函数运行完毕，本地变量就会被删除。

## 全局 JavaScript 变量

在函数外声明的变量是_全局_变量，网页上的所有脚本和函数都能访问它。

## JavaScript 变量的生存期

JavaScript 变量的生命期从它们被声明的时间开始。

局部变量会在函数运行以后被删除。

全局变量会在页面关闭后被删除。

## 向未声明的 JavaScript 变量来分配值

如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明。

这条语句：

```
carname="Volvo";
```

将声明一个_全局_变量 carname，即使它在函数内执行。


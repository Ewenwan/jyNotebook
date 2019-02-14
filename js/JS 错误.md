## JavaScript 测试和捕捉

_和java一样_

_try_语句允许我们定义在执行时进行错误测试的代码块。

_catch_语句允许我们定义当 try 代码块发生错误时，所执行的代码块。

JavaScript 语句_try_和_catch_是成对出现的。

### 语法

```
try
  {
  
//在这里运行代码

  }
catch(err)
  {
  
//在这里处理错误

  }
```







## Throw 语句

throw 语句允许我们创建自定义错误。

正确的技术术语是：创建或_抛出异常_（exception）。

如果把 throw 与 try 和 catch 一起使用，那么您能够控制程序流，并生成自定义的错误消息。

### 语法

```
throw 
exception
```

异常可以是 JavaScript 字符串、数字、逻辑值或对象。

```
<script>
function myFunction()
{
try
  {
  var x=document.getElementById("demo").value;
  if(x=="")    throw "empty";
  if(isNaN(x)) throw "not a number";
  if(x>10)     throw "too high";
  if(x<5)      throw "too low";
  }
catch(err)
  {
  var y=document.getElementById("mess");
  y.innerHTML="Error: " + err + ".";
  }
}
</script>

<h1>My First JavaScript</h1>
<p>Please input a number between 5 and 10:</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">Test Input</button>
<p id="mess"></p>
```




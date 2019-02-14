_tips:html中的脚本必须位于&lt;script&gt;与&lt;/script&gt;标签之间。脚本可被放置在HTML页面的&lt;body&gt;和&lt;/body&gt;部分中_

---

## &lt;script&gt;标签

&lt;script&gt;&lt;/script&gt;之间的代码行包含了javascript

```
<script>
    alert("My First JavaScript");
</script>
```

---

## &lt;body&gt;中的javascript

javascript会在页面加载时向HTML的&lt;body&gt;写文本

```
<html>
    <head>
    </head>
    <body>
        <script>
            document.write("<h1>this is a heading</h1>");
            document.write("<p>this is a paragraph</p>");
        </script>
    </body>
</html>
```

---

_tips:通常把javascript代码放在&lt;head&gt;部分中，或者放在页面底部。这样可以把它们安置到同一位置，不会干扰页面的内容。_

---

## &lt;head&gt;中的javascript函数

```
<!doctype html>
<html>
    <head>
        <script>
            function myFunction()
            {
                x = document.getElementById("demo").innerHTML = "java"
            }
        </script>
    </head>
    <body>
        <p id="demo">A paragraph</p>
        <button type="button" onclick="myFunction()">Try it</button>
    </body>
</html>
```

---

## &lt;body&gt;中的javascript函数

```
<!DOCTYPE html>
<html>
    <body>
        
        <h1>My Web Page</h1>
        
            <p id="demo">A Paragraph</p>
            
            <button type="button" onclick="myFunction()">Try it</button>
            
            <script>
            function myFunction()
            {
            document.getElementById("demo").innerHTML="My First JavaScript Function";
            }
            </script>
    
    </body>
</html>
```

---

## 外部的javascript

需使用外部文件，在&lt;script&gt;标签的"src"属性中设置该.js文件

```
<!DOCTYPE html>
<html>
    <body>
    <script src="myScript.js"></script>
    </body>
</html>
```

在 &lt;head&gt; 或 &lt;body&gt; 中引用脚本文件都是可以的。实际运行效果与您在 &lt;script&gt; 标签中编写脚本完全一致。


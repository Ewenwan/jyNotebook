# 2.2.2 网页的结构

网页的一般结构，都是 html 标签内嵌套 head 和 body 标签，head 内定义网页的配置和引用，body 内定义网页的正文。

```text
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>This is a test</title>
    </head>
    <body>
        <div id="header">
           header
        </div>    
        <div id="container">
            <div class="wrapper">
                <h2 class="title">Hello World</h2>
                <p class="text">Hello, this is a paragraph.</p>
            </div>
        </div>
        <div id="footer">
            footer
        </div>
    </body>
</html>
```


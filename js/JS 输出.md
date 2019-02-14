tips:_JavaScript 通常用于操作 HTML 元素。_

操作HTML元素

如需从 JavaScript 访问某个 HTML 元素，您可以使用 document.getElementById\(id\) 方法。

```
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p id="demo">我的第一个段落</p>

<script>
document.getElementById("demo").innerHTML="我的第一段 JavaScript";
</script>

</body>
</html>
```

---

## 写到文档输出

document.write\(\)仅仅向文档输出写文档

如果在文档已完成加载后document.write,整个HTML页面将被覆盖

```
<!DOCTYPE HTML>
<html>
    <head></head>
    <body>
        <script>
            document.write("<p>angle</p>");
        </script>
    </body>
</html>
```

---




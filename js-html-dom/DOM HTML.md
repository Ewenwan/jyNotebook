HTML DOM 允许javascript改变HTML元素的内容

---

## 改变HTML输出流

javascript能够创建动态的HTML内容

```
<!DOCTYPE html>
<html>
    <body>
        <script>
            document.write(Date());
        </script>
    </body>
</html>
```

_tips:不要在文档加载后使用document.write\(\),这会将覆盖原来文档_

### 改变HTML内容

修改HTML内容的最简单的方法时使用innerHTML属性

语法:

```
document.getElementById(id).innerHTML = new HTML
```

实例:

```
<html>
    <body>
        <p id="p1">Hello World</p>
        <script>
            document.getElementById("p1").innerHTML = "New text";
        </script>
    </body>
</html>
```

---

## 改变HTML属性

语法:

```
document.getElementById(id).attribute = new value
```

```
<!DOCTYPE HTML>
<html>
    <body>
        <img id="image" stc="xxx.gif">
        
        <script>
            document.getElementById("image").src = "xxx.jpg";
        </script>
    </body>
</html>
```

例子解释:

* 上面的HTML文档含有id="iamge"的&lt;img&gt;元素
* 使用HTML DOM来获得id="image"的元素
* javascript更改此元素的属性\(把"xxx.gif"更换成"landscape.jpg"\)




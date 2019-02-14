## javascript HTML DOM 元素\(节点\)

添加和删除节点\(HTML 元素\)

---

## 创建新的HTML元素

向HTML DOM添加新元素，必须首先创建该元素\(元素节点\)，然后向一个已存在的元素追加该元素

```
<!DOCTYPE HTML>
<html>
    <body>
        <div id="div1">
            <p id="p1">这是一个段落1</p>
            <p id="p2">这是另一个段落2</p>
        </div>
        <script>
            var para = document.createElement("p");
            var node = document.createTextNode("这是新段落3");
            para.appendChild(node);

            var element = document.getElementById("div1");
            element.appendChild(para);
        </script>
    </body>
</html>
```

解释:

创建新的&lt;p&gt;元素

```
var para = document.createElement("p");
```

向&lt;p&gt;元素添加文本，创建文本节点

```
var node = document.createTextNode("这是新的段落。");
```

向&lt;p&gt;元素追加文本节点

```
para.appendChild(node);
```

找到已有元素

```
var element.document.getElementById("div1");
```

追加新元素&lt;p&gt;

```
element.appendChild(para);
```

---

删除已有的HTML元素

删除HTML元素，必须首先获得该元素的父元素

实例:

```
<div id="div1">
    <p id="p1">这是一个段落</p>
    <p id="p2">这是另一个段落</p>
</div>
<script>
    var parent = document.getElementById("div1");
    var child = document.getElementById("p1");
    parent.removeChild(child);
</script>
```

例子解释：

这个 HTML 文档含有拥有两个子节点（两个 &lt;p&gt; 元素）的 &lt;div&gt; 元素：

```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>
```

找到 id="div1" 的元素：

```
var parent=document.getElementById("div1");
```

找到 id="p1" 的 &lt;p&gt; 元素：

```
var child=document.getElementById("p1");
```

从父元素中删除子元素：

```
parent.removeChild(child);
```

常用的解决方案:找到要删除的子元素，然后使用其parentNode属性来找到父元素

```
var child = document.getElemtnById("p1");
child.parentNode.removeChild(child);
```




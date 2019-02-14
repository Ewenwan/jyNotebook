HTML DOM 允许javascript改变HTML元素的样式

## 改变HTML样式

语法:

```
document.getElementById(id).style.property = new style
```

实例1:

改变&lt;p&gt;元素的样式

```
<p id="p2">Hello Wordl</p>
<script>
    document.getElementById("p2").style.color = "blue";
</script>
```

实例2:

```
<h1 id="id1">Heading 1</h1>
<button type="button" onclick="document.getElementById("id1").style.color='red'"></button>
```




## 框架

通过使用框架，可以在同一个浏览器窗口中显示不止一个页面**。**每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。

使用框架的坏处：

* 开发人员必须同时跟踪更多的HTML文档
* 很难打印整张页面

---

框架结构标签\(&lt;frameset&gt;\)

* 框架结构标签（）定义如何将窗口分割为框架
* 每个 frameset 定义了一系列行或列
* rows/columns 的值规定了每行或每列占据屏幕的面积

框架标签\(Frame\)

* Frame 标签定义了放置在每个框架中的 HTML 文档。

---

## 垂直框架

```HTML
<html>
    <frameset cols="25%,50%,25%">
        <frame src="http://www.w3school.com.cn/example/html/frame_a.html">
        <frame src="http://www.w3school.com.cn/example/html/frame_b.html">
        <frame src="http://www.w3school.com.cn/example/html/frame_c.html">
    </frameset>
</html>
```

## 水平框架

```HTML
<html>
<frameset rows="25%,50%,25%">
  <frame src="http://www.w3school.com.cn/example/html/frame_a.html">
  <frame src="http://www.w3school.com.cn/example/html/frame_b.html">
  <frame src="http://www.w3school.com.cn/example/html/frame_c.html">
</frameset>
</html>
```

_tips:cols和rows属性中的百分比，每一个百分比对应着一个frame标签，注意:总百分比加起来为100%_

---

## noframes标签

```HTML
<noframes>
    <body>您的浏览器无法处理框架！</body>
</noframes>
```

## noresize标签--禁止调整框架窗口尺寸

```HTML
<html>
  <frameset cols="50%,*,25%">
    <frame src="/example/html/frame_a.html" noresize="noresize" />
    <frame src="/example/html/frame_b.html" />
    <frame src="/example/html/frame_c.html" />
  </frameset>
</html>
```




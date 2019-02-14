## Canvas用于在网页上绘制图形

---

## 什么是Canvas?

HTML的canvas元素使用javascript早网页上绘制图像

画布是一个矩形区域，可以控制其每一像素

canvas拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法

---

## 创建Canvas元素

向HTML页面添加canvas元素

规定元素的id、宽度和高度

```HTML
<canvas id="myCanvas" width="200" height="100"></canvas>
```

---

## 通过javascript来绘制

canvas元素本身是没有绘图能力的，所有的绘制工作必须在javascript内部完成

```HTML
    <html>
        <head>
            <script type="text/javascript">
                var c = document.getElementById("myCanvas");
                var cxt = c.getContext("2d");
                cxt.fillstyle="red";
                cxt.fillRect(0,0,100,100);
            </script>
        </head>
        <body>
            <canvas id="myCanvas" width="200" height="200"></canvas>
        </body>
    </html>
```




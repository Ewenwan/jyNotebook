## 导航条 = 链接列表

实例:

```
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <ul>
            <li><a href="#one">one</a></li>
            <li><a href="#two">two</a></li>
            <li><a href="#three">three</a></li>
            <li><a href="#four">four</a></li>
        </ul>
    </body>
</html>
```

去掉圆点和外边距

```
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            ul{
                list-style-type:none;
                margin:0;
                padding:0;
            }
        </style>
    </head>
    <body>
        <ul>
            <li><a href="#one">one</a></li>
            <li><a href="#two">two</a></li>
            <li><a href="#three">three</a></li>
            <li><a href="#four">four</a></li>
        </ul>
    </body>
</html>
```

* 解释:
* list-style-type:none - 删除圆点。导航栏不需要列表标记
* 把外边距和内边距设置为0可以去除浏览器的默认设定

## 垂直导航栏

如需构建导航栏，只需定义&lt;a&gt;元素的样式

```
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            ul{
                list-style-type:none;
                margin:0;
                padding:0;
            }
           /* a{
                display:block;
                width:60px;
                background-color:pink;
            }*/
            a:link,a:visited{
                display:block;
                width:120px;
                background-color:pink;
                text-align:center;
                padding:4px;
                text-decoration:none;
                text-transform:uppercase;
                color:white;
            }
            a:hover,a:active{
                background-color:red;
            }
        </style>
    </head>
    <body>
        <ul>
            <li><a href="#one">one</a></li>
            <li><a href="#two">two</a></li>
            <li><a href="#three">three</a></li>
            <li><a href="#four">four</a></li>
        </ul>
    </body>
</html>
```

解释:

* display:block - 把链接显示为块级元素可使整个链接区域可点击
* width:60px -块元素默认占用全部可用宽度。需要规定60像素的高度
* text-decoration:none - 去除下划线
* text-tansform:uppercase - 将字母转换成大写字母
* padding - 内边距设置为4像素
* text-align:center - 设置文本居中
* a:link - 未访问的链接
* a;visited - 用户已访问的链接
* a:hover - 鼠标指针位于链接的上方
* a:active - 链接呗点击的时刻

## 水平导航栏

有两种创建水平导航栏的方法。使用行内或浮动列表项

两种都可以，但是如果希望链接拥有相同的尺寸，就必须使用浮动方法

## 行内列表项

构建水平导航栏的方法之一是将&lt;li&gt;元素规定为行内元素

```
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            ul{
                list-style-type:none;
                margin:0;
                padding:0;
            }
           /* a{
                display:block;
                width:60px;
                background-color:pink;
            }*/
            a:link,a:visited{
               /* display:block;*/
                width:120px;
                background-color:pink;
                text-align:center;
                padding:4px;
                text-decoration:none;
                text-transform:uppercase;
                color:white;
            }
            a:hover,a:active{
                background-color:red;
            }
            li{
                display:inline;
            }
        </style>
    </head>
    <body>
        <ul>
            <li><a href="#one">one</a></li>
            <li><a href="#two">two</a></li>
            <li><a href="#three">three</a></li>
            <li><a href="#four">four</a></li>
        </ul>
    </body>
</html>
```

解释:

* display:inline -默认地,&lt;li&gt;元素是块元素

## 对列表项进行浮动

为了让所有链接拥有相等的宽度，浮动&lt;li&gt;元素并规定&lt;a&gt;元素的宽度

```
<!DOCTYPE HTML>
<html>
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            ul{
                list-style-type:none;
                margin:0;
                padding:0;
            }
           /* a{
                display:block;
                width:60px;
                background-color:pink;
            }*/
            a:link,a:visited{
               /* display:block;*/
                width:120px;
                background-color:pink;
                text-align:center;
                padding:4px;
                text-decoration:none;
                text-transform:uppercase;
                color:white;
            }
            a:hover,a:active{
                background-color:red;
            }
            li{
                float:left;
            }
        </style>
    </head>
    <body>
        <ul>
            <li><a href="#one">one</a></li>
            <li><a href="#two">two</a></li>
            <li><a href="#three">three</a></li>
            <li><a href="#four">four</a></li>
        </ul>
    </body>
</html>
```

解释:

* float:lfet - 使用float来把块元素滑向彼此
* display:block - 把链接显示为块元素可使整个链接区域可点击（不仅仅是文本），同时也允许规定宽度
* width:60px - 由于块元素默认占用全部可用宽度，链接无法滑动至彼此相邻






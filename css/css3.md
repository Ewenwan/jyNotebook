## css3用户界面

* resize
* box-sizing
* outline-offset

---

## css3 Resizing

在css3，resize属性规定是否可用户调整元素尺寸

实例:

规定div元素可由用户调整大小

```
div{
    resize:both;
    overflow:auto;
}
```

---

## css3 Box Sizing

box-sizing属性允许以确切的方式定义适应某个区域的具体内容

实例:规定两个并排的带边框方框

```
div{
    box-sizing:border-box;
    -moz-box-sizing:border-box;
    -webkit-box-sizing:border-box;
    width:50%;
    float:left;
}
```

---

## css3 outline offset

outline-offset属性对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓

轮廓与边框有两点不同:

* 轮廓不占用空间
* 轮廓可能是非矩形

实例:规定边框边缘之外 15 像素处的轮廓：

```
div{
    border:2px solid black;
    outline:2px solid red;
    outline-offset:15px;
}
```

## 新的用户界面属性

下面的表格列出了所有的转换属性：

| 属性 | 描述 | CSS |
| :--- | :--- | :--- |
| [appearance](http://www.w3school.com.cn/cssref/pr_appearance.asp) | 允许您将元素设置为标准用户界面元素的外观 | 3 |
| [box-sizing](http://www.w3school.com.cn/cssref/pr_box-sizing.asp) | 允许您以确切的方式定义适应某个区域的具体内容。 | 3 |
| [icon](http://www.w3school.com.cn/cssref/pr_icon.asp) | 为创作者提供使用图标化等价物来设置元素样式的能力。 | 3 |
| [nav-down](http://www.w3school.com.cn/cssref/pr_nav-down.asp) | 规定在使用 arrow-down 导航键时向何处导航。 | 3 |
| [nav-index](http://www.w3school.com.cn/cssref/pr_nav-index.asp) | 设置元素的 tab 键控制次序。 | 3 |
| [nav-left](http://www.w3school.com.cn/cssref/pr_nav-left.asp) | 规定在使用 arrow-left 导航键时向何处导航。 | 3 |
| [nav-right](http://www.w3school.com.cn/cssref/pr_nav-right.asp) | 规定在使用 arrow-right 导航键时向何处导航。 | 3 |
| [nav-up](http://www.w3school.com.cn/cssref/pr_nav-up.asp) | 规定在使用 arrow-up 导航键时向何处导航。 | 3 |
| [outline-offset](http://www.w3school.com.cn/cssref/pr_outline-offset.asp) | 对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓。 | 3 |
| [resize](http://www.w3school.com.cn/cssref/pr_resize.asp) | 规定是否可由用户对元素的尺寸进行调整。 | 3 |

部分实例:

```
<!DOCTYPE html>
<html>
<head>
<style>
button
{
position:absolute;
}

button#b1
{
top:20%;left:25%;
nav-index:1;
nav-right:#b2; nav-left:#b4;
nav-down:#b2; nav-up:#b4;
}

button#b2
{
top:40%;left:50%;
nav-index:2;
nav-right:#b3; nav-left:#b1;
nav-down:#b3; nav-up:#b1;
}

button#b3
{
top:70%;left:25%;
nav-index:3;
nav-right:#b4; nav-left:#b2;
nav-down:#b4; nav-up:#b2;
}

button#b4
{
top:40%;left:0%;
nav-index:4;
nav-right:#b1; nav-left:#b3;
nav-down:#b1; nav-up:#b3;
}
</style>
</head>
<body>

<button id="b1">Button 1</button>
<button id="b2">Button 2</button>
<button id="b3">Button 3</button>
<button id="b4">Button 4</button>

</body>
</html>
```




## css3边框

创建圆角边框 -- border-radius

向矩形添加阴影 -- box-shadow

使用图片来绘制边框 -- border-image

---

## css3圆角边框

border-radius属性用于创建圆角

实例:向div元素添加圆角

```
div{
    border:2px solid;
    border-radius:20px;
    -moz-border-radius:25px;/*old firfox*/
}
```

解释:

border-radius:设置圆角像素为20px

注释：

按此顺序设置每个 radii 的四个值。如果省略 bottom-left，则与 top-right 相同。如果省略 bottom-right，则与 top-left 相同。如果省略 top-right，则与 top-left 相同。

```
例子 1
border-radius:2em;
等价于：

border-top-left-radius:2em;
border-top-right-radius:2em;
border-bottom-right-radius:2em;
border-bottom-left-radius:2em;
例子 2
border-radius: 2em 1em 4em / 0.5em 3em;
等价于：

border-top-left-radius: 2em 0.5em;
border-top-right-radius: 1em 3em;
border-bottom-right-radius: 4em 0.5em;
border-bottom-left-radius: 1em 3em;
```

---

## css3边框阴影

box-shadow属性用于向方框添加阴影

向div元素添加方框阴影

可选值:

h-shadow:水平阴影的位置。允许负值

v-shadow:垂直阴影的位置。允许负值

blur:可选。模糊距离

spread:可选。阴影的尺寸

color:可选。阴影的颜色

inset:可选。将外部阴影\(outset\)改为内部阴影

```
div{
    box-shadow:10px 10px 50px red;
}
```

---

## css边框图片

border-image属性可以使用图片来创建边框

```
border-image:url(xxxx)
```

可选值:

| 值 | 描述 |
| :--- | :--- |
| border-image-source | 用在边框的图片的路径 |
| border-image-slice | 图片边框向内偏移 |
| border-image-width | 图片边框的宽度 |
| border-image-outset | 边框图像区域超出边框的量 |
| border-image-repeat | 图像边框是否应平铺\(repeated\)，铺满\(rounded\)或拉伸\(stretched\) |

---

## 新的边框属性

| 属性 | 描述 |
| :--- | :--- |
| [border-image](http://www.w3school.com.cn/cssref/pr_border-image.asp) | 设置所有 border-image-\* 属性的简写属性。 |
| [border-radius](http://www.w3school.com.cn/cssref/pr_border-radius.asp) | 设置所有四个 border-\*-radius 属性的简写属性。 |
| [box-shadow](http://www.w3school.com.cn/cssref/pr_box-shadow.asp) | 向方框添加一个或多个阴影。 |




## 背景色

background-color属性为元素定义背景色

```HTML
body{
    background-color:red;
}
```

可选值:

transparent:透明

color\_name:颜色名称

hex\_name:16进制颜色名称

rgb\_name:rgb代码的背景颜色

---

## 背景图像

background-image属性,设置背景图像

```HTML
body{
    background-image:url(图片的位置);
}
```

---

## 背景重复

background-reapt属性，设置图像是否重复

可能的值:

repeat：背景图像将在垂直方向和水平方向重复

repeat-x:背景图像将在水平方向重复

repeat-y:背景图像将在垂直方向重复

no-repeat:背景图像将仅显示一次

---

## 背景定位

background-position属性可以改变图像在背景中的位置

可能的值:

top、left、right、bottom

top left

top center

top right

center left

center center

center right

bottom left

bottom right

bottom center

百分比:x% y%:第一个值水平位置，第二个是垂直位置

xpos,ypos：第一个水平位置，第二个垂直位置,即坐标

---

## 背景关联

background-attachment属性设置背景图像是否固定或者页面的其余部分滚动

可选值:

scroll:背景图像会随着页面其余部分的滚动而滚动

fixed:当页面其余部分滚动时，背景图像不会滚动

---

| 属性 | 值 |
| :--- | :--- |
| background | 将背景属性设置在一个声明中 |
| background-attachment | 背景图像是否固定或者随着页面的其余部分滚动 |
| background-color | 设置元素的背景颜色 |
| background-image | 把图像设置为背景 |
| background-position | 设置背景图像的起始位置 |
| background-repeat | 设置背景图像是否及如何重复 |




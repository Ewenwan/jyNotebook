## css边框属性

---

## outline属性

outline\(轮廓\)是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用

可选值:

outline-color:规定边框的颜色

outline-style:规定边框的样式

outline-width:规定边框的宽度

---

## outline-color属性

outline\(轮廓\)是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。outline属性可设置元素周围的轮廓线

可选值:

color\_name:规定颜色值为颜色名称的轮廓颜色

hex-number:规定颜色值为十六进制值得轮廓颜色

rgb\_number:规定颜色值为rgb代码的轮廓的颜色

invert:默认。执行颜色反转\(逆向的颜色\)。可使轮廓在不同的背景颜色中都是可见的

```HTML
p{
//outline-color:red;
outline-color:#00ff00;
}
```

---

## outline-style属性

outline-style属性用于设置元素的整个轮廓的样式。样式不能是none，否则轮廓不会出现

可选值:

none:默认。定义无轮廓

dotted:点状的轮廓

dashed:虚线轮廓

solid:实现轮廓

double:双线轮廓，双线的宽度等同于outline-width的值

groove:3d凹槽轮廓，此效果取决于outline-color值

ridge:3d凹边轮廓。此效果取决于outline-color值

inset:3d凹边轮廓。此效果取决于outline-color值

outset:3d凸边轮廓。此效果取决于outline-color值

```HTML
p{
    outline-style:dashed;
}
```

---

## outline-width属性

outline-width属性设置元素整个轮廓的宽度，只有当轮廓样式不是none时，这个宽度才会起作用，如果样式为none，宽度会重置为0

可选值:

thin:规定细轮廓

medium:默认。规定中等的轮廓

thick:规定粗的轮廓

length:允许规定轮廓粗细的值




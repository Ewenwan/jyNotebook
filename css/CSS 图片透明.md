## opacity属性

opacity属性设置元素的不透明级别

可选值:

value:规定不透明度，从0.0\(完全透明\)到1.0\(完全不透明\)

---

## 实例1 - 创建透明图像

opacity属性定义透明度

```
img{
    opacity:0.4;
    filter:alpha(opacity=40); /* 针对 IE8 以及更早的版本 */
}
```

## 实例2 - 图形透明度 - Hover效果

当鼠标溢出图像后，图像会再次透明

```
img{
    opacity:0.4;
    filter:alpha(opacity=40);
}
img:hover{
    opacity:1.0;
    filter:alpha(opacity=100);
}
```




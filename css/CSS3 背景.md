## background-size属性

background-size属性规定背景图片的尺寸

## 语法

| 值 | 描述 |
| :--- | :--- |
| length | 设置背景图像的高度和宽度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。 |
| percentage | 以父元素的百分比来设置背景图像的宽度和高度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。 |
| cover | 把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。背景图像的某些部分也许无法显示在背景定位区域中。 |
| contain | 把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。 |

---

## background-origin属性

background-origin属性规定背景图片的定位区域

背景图片可以放置于 content-box、padding-box 或 border-box 区域。

![](http://www.w3school.com.cn/i/background-origin.gif "背景图片的定位区域")

---

## 多重背景图片

允许使用多个背景图像

```
body{
    background-image:url(xx.gif),url(xxx.gif);
}
```

---

## background-clip属性

background-clip属性规定背景的绘制区域

可选值:

border-box:背景被裁剪到边框盒

padding-box:背景被裁剪到内边距框

contetn-box:背景被裁剪到内容框

---

## 新的背景属性

| 属性 | 描述 |
| :--- | :--- |
| background-clip | 规定背景的绘制区域。 |
| background-origin | 规定背景图片的定位区域。 |
| background-size | 规定背景图片的尺寸。 |






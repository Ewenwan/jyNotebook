_tips:css框模型\(Box Model\)规定了元素框处理元素内容、内边距、边框和外边距的方式。_

## css框模型

![](/assets/VTMAK\($OE]4@WH1$A~BYGZS.png)

---

tips:内边距、边框和外边距都是可选的，默认值是零。但是，许多元素将由用户代理样式表设置外边距和内边距。可以通过将元素的 margin 和 padding 设置为零来覆盖这些浏览器样式。这可以分别进行，也可以使用通用选择器对所有元素进行设置

```HTML
*{
    margin:0;
    padding:0;
}
```

---

假设框的每个边上有10个像素的外边距和5个像素的内边距。如果希望这个元素达到100个像素，就需将内容的宽度设置为70像素，如图:

![](/assets/QQ截图20180508182211.png)

```HTML
#box{
    width:70px;
    margin:10px;
    padding:5px;
}
```

---

* 扩展

术语

element:元素

padding:内边距/填充

border:边框

margin:外边距/空白/空白边






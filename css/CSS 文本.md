## 缩进文本

text-indent属性规定文本块中首行文本的缩进

可选值:

length:定义固定的缩进

百分比:定义基于父元素宽度的百分比的缩进

---

## 水平对齐

text-align属性规定元素中的文本的水平对齐方式

可选值:

left、right、center

jusify:实现两端对齐文本效果

---

## 字间隔

word-spacing属性增加或减少单词间的空白\(即字间隔\)，即定义元素中字之间插入多少个空白符

可选值:

normal:定义单词间的标准空间

length:定义单词间的固定空间

```HTML
<html>
    <head>
        <style>p{word-spacing:20px;}</style>
    </head>
    <body>
        <p>angle miku</p>
    </body>
</html>
```

---

## 字母间隔

letter-spacing属性增加或减少字符间的空白\(字符间距\)，即定义了在文本字符框之间插入多少空间

可选值:

normal:规定字符间没有额外的空间

length:定义字符间的固定空间\(允许使用负值\)

---

## 字符转换

text-transform属性处理文本的大小写

可选值:

none:定义带有小写字母和大写字母的标准的文本

capitalize:文本中的每个单词以大写字母开头

uppercase:定义仅有大写字母

lowercase:定义无大写字母，仅有小写字母

---

## 文本装饰

text-decoration属性规定添加到文本的装饰

可选值:

none:定义标准的文本

underline:定义文本下的一条线

overline:定义文本上的一条线

line-through:定义穿过文本下的一条线

bink:定义闪烁的文本

---

## 处理空白符

white-space属性设置如何处理元素内的空白

可选值:

normal：空白会被浏览器忽略

pre:空白会被浏览器保留

nowrap:文本不会换行，文本会在在同一行上继续，直到遇到&lt;br&gt;标签为止

pre-wrap:保留空白符序列，但是正常地进行换行

pre-line:合并空白符序列,但是保留换行符

---

## 文本方向

direction属性规定文本的方向/书写方向

该属性指定了块的基本书写方向,以及针对Unicode双向算法的嵌入和覆盖方向

可选值:

ltr:文本方向从左到右

rtl:文本方向从右到左

---

## css文本属性

| 属性 | 描述 |
| :--- | :--- |
| color | 设置文本颜色 |
| direction | 设置文本方向 |
| line-height | 设置行高 |
| letter-spacing | 设置字符间距 |
| text-align | 对齐元素中的文本 |
| text-decoration | 向文本添加修饰 |
| text-indent | 缩进元素中的文本的首行 |
| text-shadow | 设置文本阴影 |
| text-transform | 控制元素中的字母 |
| unicode-bidi | 设置文本方向 |
| white-space | 设置元素中空的处理方式 |
| word-spacing | 设置字间距 |




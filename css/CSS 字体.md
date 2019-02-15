## css字体系列

通用字体系列:Serif、Sans-serif、Monospace、Cursive、Fantasy

特定字体系列:具体的字体系列\(如"Times"或"Courier"\)

---

## 指定字体系列

font-family规定元素的字体系列

font-family可以同时有多个值，如果浏览器不支持第一个字体，则会尝试下一个字体。

可选值:

family-name/generic-family:用于某个元素的字体名称或/即类族名称的一个优先表

```HTML
body{
    family-font:Serif;
}
```

---

## 字体风格

font-style属性定义字体的风格

可选值:

normal:文本正常显示

italic:文本斜体显示

oblique:文本倾斜显示

---

## 字体变形

font-variant属性设置小型大写字母的字体显示文本

可选值:

normal:正常文本

small-caps:小号的大写字母的字体

```HTML
<html>
    <head>
        <style>
            p{
                font-variant:small-caps;
            }
        </style>
    </head>
    <body>
        <p>angle</p>
    </body>
</html>
```

---

## 字体加粗

font-weight属性设置文本的粗细

可选值:

normal:默认值

bold:定义粗体字体

bolder:定义更粗的字体

lighter:定义更细的字体

100~900:定义由粗到细的字体。

tips:400等同于normal，700等同于bold

---

## 字体大小

font-size属性可设置字体的尺寸

可选值:

xx-small、x-small、small、medium、large、x-large、xx-large:设置字体有小到大

smaller:把font-size设置为比父元素更小的尺寸

larger:把font-size设置为比父元素更大的尺寸

length:把font-size设置为一个固定的值

百分比\(%\):把font-size设置基于父元素的一个百分比值

_tips:1em = 16px_

---

| 属性 | 描述 |
| :--- | :--- |
| font | 所有对字体的属性设置都可以在font里声明 |
| font-family | 设置字体的系列 |
| font-size | 设置字体的尺寸 |
| font-style | 设置字体风格 |
| font-variant | 以小型大写字体或者正常字体显示文本 |
| font-weight | 设置字体的粗细 |




## 设置链接的样式

链接的四种状态:

* a:link -- 普通的、未被访问的链接
* a:visited -- 用户已访问的链接
* a:hover -- 鼠标指针位于链接的上方
* a:active -- 链接被点击的时刻

```HTML
a:link{color:red;} /*未被访问的链接*/
a:visited{color:pink;}/*已被访问的链接*/
a:hover{color:green;}/*鼠标指针移动到链接上*/
a:active{color:blue;}/*正在被点击的链接*/
```

设置的顺序:

* a:hover必须位于a:link和a:visited之后
* a:active必须位于a:hover之后

---

## 文本修饰

text-decoration属性大多用于去掉链接中的下划线

```HTML
a{text-decoration:none;}
```

---

## 背景色

background-color属性规定链接的颜色




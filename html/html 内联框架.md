## HTML Iframe

iframe用于在网页内显示网页

**添加iframe的语法:**

```HTML
<iframe src="URL"></iframe>
```

URL指向隔离页面的位置

---

## Iframe - 设置高度和宽度

height 和 width属性用于规定iframe的高度和宽度

属性值的默认单位是像素，也可以用百分比来设定

```HTML
<iframe src="https://www.baidu.com/" width="200" height="200"></iframe>
```

---

## Iframe - 删除边框

frameborder属性规定是否显示iframe周围的边框

设置属性值为0就可以移除边框

```HTML
<iframe src="https://www.baidu.com/" frameborder="0"></frame>
```

---

## 使用iframe作为链接的目标

iframe可用作链接的目标\(target\)

链接的target属性必须引用iframe的name属性

```HTML
<iframe src="http://www.google.cn/" name="iframe_bai"></iframe>
<p><a href="https://www.baidu.com/">百度一下</p>
```

---

## HTML iframe 标签

| 标签 | 描述 |
| :--- | :--- |
| [&lt;iframe&gt;](http://www.w3school.com.cn/tags/tag_iframe.asp) | 定义内联的子窗口（框架） |




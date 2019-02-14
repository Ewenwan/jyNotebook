## HTML超链接\(链接\)

可以通过&lt;a&gt;标签在HTML中创建

* 通过使用href属性 - 创建指向另一个文档的链接\(非当前文档页面\)

* 通过使用name属性 - 创建文档内的书签

---

## HTML 链接语法

`<a href="url_path">angle</a>`

href属性定义链接的目标地址

---

## HTML链接 -target属性

使用Target属性，可以定义被链接的文档在何处显示

```HTML
<a href="https://www.bilibili.com/" target="_blank">哔哩哔哩</a>
```

---

## HTML链接 - name属性

name属性规定锚\(anchor\)的名称，可以使用name属性创建HTML页面中的书签

**命名锚的语法:**

```HTML
<a name="label">锚</a>
```

_tips:可以使用id属性来代替name属性_

实例:

* 对HTML文档中对锚进行命名即创建一个书签

```HTML
<a name="tips">angle</a>
```

* 在本页文档创建指向该锚的链接

```HTML
<a href="#tips">angle</a>
```

---

## HTML 链接标签

| 标签 | 描述 |
| :--- | :--- |
| [&lt;a&gt;](http://www.w3school.com.cn/tags/tag_a.asp) | 定义锚 |




## HTML 引用

---

## 引用（Quotation）

这是摘自 WWF 网站的引文：

> 五十年来，WWF 一直致力于保护自然界的未来。 世界领先的环保组织，WWF 工作于 100 个国家，并得到美国一百二十万会员及全球近五百万会员的支持。

---

## HTML 短引用

HTML&lt;q&gt;元素定义短的引用，浏览器通常为&lt;q&gt;元素包围引号

实例:

```HTML
<p>WWF 的目标是：<q>构建人与自然和谐共存的世界。</q></p>
```

---

## HTML 长引用

HTML&lt;blockquote&gt;元素定义被引用的节，浏览器通常会对&lt;blockquote&gt;元素进行缩进处理

实例:

```HTML
<p>以下内容引用自 WWF 的网站：</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>
```

---

## HTML 缩略词

HTML&lt;abbr&gt;元素定义缩写或首字母缩略语

实例:

```HTML
<p><abbr title="World Health Organizetion">WHO</abbr></p>
```

---

## HTML 定义

HTML &lt;dfn&gt;元素定义项目或缩写的定义

用法:

* 如果设置了&lt;dfn&gt;元素的title属性，则定义项目

```HTML
<p><dfn title="World Health Organization">WHO</dfn></p>
```

* 如果&lt;dfn&gt;元素中包含&lt;abbr&gt;元素，则&lt;abbr&gt;的title属性定义项目:

```
<p><dfn><abbr title="World Health Organization">WHO</abbr></dfn></p>
```

* &lt;dfn&gt;文本内容就是项目，并且父元素包含定义

```HTML
<p><dfn>WHO</dfn> World Health Organization 成立于 1948 年。</p>
```

提示:一般用第一种方式

---

## HTML 联系信息

HTML&lt;address&gt;元素定义文档或文章的联系信息。

实例:

```HTML
<address>
    author:angle<br />
    emial:xxxx@xx.xxx<br />
</address>
```

---

## HTML 著作标题

HTML&lt;cite&gt;元素定义著作的标题

实例:

```
<p><cite>angle</cite>she is a angle</p>
```

---

HTML 双向重写

HTML&lt;bdo&gt;元素定义双流向覆盖

&lt;bdo&gt;元素用于覆盖当前文本方向

实例:

```
<bdo dir="rtl">angle</bdo>
```

---

## HTML 引文、引用和定义元素

| 标签 | 描述 |
| :--- | :--- |
| &lt;abbr&gt; | 定义缩写或首字母缩略语。 |
| &lt;address&gt; | 定义文档作者或拥有者的联系信息。 |
| &lt;bdo&gt; | 定义文本方向。 |
| &lt;blockquote&gt; | 定义从其他来源引用的节。 |
| &lt;dfn&gt; | 定义项目或缩略词的定义。 |
| &lt;q&gt; | 定义短的行内引用。 |
| &lt;cite&gt; | 定义著作的标题。 |




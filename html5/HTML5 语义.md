## 什么是语义元素？

语义元素清楚地向浏览器和开发者描述其意义。

_非语义_元素的例子：&lt;div&gt; 和 &lt;span&gt; - 无法提供关于其内容的信息。

_语义_元素的例子：&lt;form&gt;、&lt;table&gt; 以及 &lt;img&gt; - 清晰地定义其内容。

---

## HTML&lt;section&gt;元素

&lt;section&gt;元素定义文档中的节。

```HTML
<section>
    <h1>angle</h1>
    <p>i love angle</p>
</section>
```

---

## HTML5&lt;article&gt;元素

&lt;article&gt;元素规定独立的自包含内容

```HTML
<article>
   <h1>What Does WWF Do?</h1>
   <p>WWF's mission is to stop the degradation of our planet's natural environment,
  and build a future in which humans live in harmony with nature.</p>
</article> 
```

---

## HTML5&lt;header&gt;元素

&lt;header&gt;元素为文档或节规定页眉

&lt;header&gt;元素应该被用作介绍内容的容器

```HTML
<header>
    <h1>anlge</h1>
</header>
```

---

## HTML5&lt;footer&gt;元素

&lt;footer&gt;元素为文档或节规定页脚

&lt;footer&gt;元素应该提供有关其包含元素的信息

页脚通常包含文档的作者、版权信息、使用条款链接、联系信息等。

实例:

```HTML
<footer>
    <p>
    Contact information:<a href="xx@xxx.com">xx@xxx.com</a>.
    </p>
</footer>
```

---

## HTML5&lt;nav&gt;元素

&lt;nav&gt;元素定义导航链接集合

&lt;nav&gt;元素旨在定义大型的导航链接块。不过，并非文档中所有链接应该位于&lt;nav&gt;元素中

```HTML
<nav>
    <a href="#">HTML</a>
    <a href="#">CSS</a>
</nav>
```

---

## HTML5 &lt;aside&gt; 元素

&lt;aside&gt;（在一边） 元素页面主内容之外的某些内容（比如侧栏）。

aside 内容应该与周围内容相关。

```HTML
<p>My family and I visited The Epcot center this summer.</p>

<aside>
   <h4>Epcot Center</h4>
   <p>The Epcot Center is a theme park in Disney World, Florida.</p>
</aside> 
```

---

## HTML5 &lt;figure&gt; 和 &lt;figcaption&gt; 元素

在书籍和报纸中，与图片搭配的标题很常见。

标题（caption）的作用是为图片添加可见的解释。

通过 HTML5，图片和标题能够被组合在_&lt;figure&gt;_元素中

```HTML
<figure>
   <img src="xx.jpg" alt="The Pulpit Rock" width="304" height="228">
   <figcaption>Fig1. - The Pulpit Pock, Norway.</figcaption>
</figure> 
```

---

## HTML5 中的语义元素

下面列出了以字母顺序排列的 HTML5 新语义元素。

这些链接指向完整的 HTML 参考手册。

| 标签 | 描述 |
| :--- | :--- |
| &lt;article&gt; | 定义文章。 |
| &lt;aside&gt; | 定义页面内容以外的内容。 |
| &lt;details&gt; | 定义用户能够查看或隐藏的额外细节。 |
| &lt;figcaption&gt; | 定义 &lt;figure&gt; 元素的标题。 |
| &lt;figure&gt; | 规定自包含内容，比如图示、图表、照片、代码清单等。 |
| &lt;footer&gt; | 定义文档或节的页脚。 |
| &lt;header&gt; | 规定文档或节的页眉。 |
| &lt;main&gt; | 规定文档的主内容。 |
| &lt;mark&gt; | 定义重要的或强调的文本。 |
| &lt;nav&gt; | 定义导航链接。 |
| &lt;section&gt; | 定义文档中的节。 |
| &lt;summary&gt; | 定义 &lt;details&gt; 元素的可见标题。 |
| &lt;time&gt; | 定义日期/时间。 |




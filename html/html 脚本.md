## HTML script元素

&lt;script&gt;标签用于定义客户端脚本，比如javascript

script元素即可包含脚本语句，也可通过src属性指向外部脚本文件

注意:必需的type属性规定脚本的MIME类型

_tips:javascript最常用于图片操作、表单验证以及内容动态更新_

```HTML
<script type="text/javascript">document.write("Hello world")</script>
```

---

## &lt;noscript&gt;标签

&lt;noscript&gt;标签提供无法使用脚本时的代替内容

```HTML
<script type="text/javascript">document.write("Hello world")</script>
<noscript>Your browser does not support JavaScript</noscript>
```

---



| 标签 | 描述 |
| :--- | :--- |
| [&lt;script&gt;](http://www.w3school.com.cn/tags/tag_script.asp) | 定义客户端脚本。 |
| [&lt;noscript&gt;](http://www.w3school.com.cn/tags/tag_noscript.asp) | 为不支持客户端脚本的浏览器定义替代内容。 |




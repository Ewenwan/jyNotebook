## HTML 基本文档

```HTML
<html>
    <head>
        <title>标题</title>
    </head>
    <body>
        身体
    </body>
<html>
```

---

## HTML 文本元素

```HTML
<p>一个段落</p>
<br /> 折行
<hr /> 水平线
<pre> 预定义 </pre>
```

---

## 逻辑风格

```HTML
<em>强调</em>
<strong>strong</strong>
<code> 计算机代码 </code>
```

---

## 物理风格

```HTML
<b>加粗</b>
<i>斜体</i>
```

---

## 链接，锚，图像标签

```HTML
<a href="http://www.baidu.com">这是一个百度链接</a>
<a href="http://www.baidu.com"><img src="url_path" alt="如果图像无法显示，我就来替换文本"/></a>
<a href="mailto:webmaster@example.com">Send e-mail</a>A named anchor:
<a name="tips">Useful Tips Section</a>
<a href="#tips">Jump to the Useful Tips Section</a>
```

---

## 无序列表

```
<ul>
    <li>angle</li>
    <li>miku</li>
</ul>
```

---

## 有序列表

```HTML
<ol>
    <li>angle</li>
    <li>miku</li>
</ol>
```

---

## 自定义列表

```HTML
<dl>
    <dt>定义项目</dt>
        <dd>定义</dd>
</dl>
```

---

## 表格

```HTML
<table border="">
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>1</td>
    </tr>
</table>
```

---

## 框架

```HTML
<frameset cols="25%,75%">
    <frame src="http://www.baidu.com">
    <frame src="http://www.google.cn/">
</frameset>
```

---

## 表单

```HTML
<form action="#" method="get|post">
    <input type="text" name="name" maxlength="30" size="10"/>
    <input type="password"/>
    <input type="radio" checked="checked"/>  
    <input type="checkbox" checked="checked"/> 
    <input type="submit"/> 
    <input type="reset"/> 
    <input type="hidden"/>
    <select>
        <option>angle</option>
        <option>miku</option>
    </select>
    <textarea name="textarea" rows="60" cols="60"></textarea>
</form>
```

---

## 实体

```HTML
&lt;小于
&gt;大于
&#169;©
```

---

## 其他元素

```HTML
<!-- This is a comment -->
<blockquote>
    Text quoted from some source.
</blockquote>
<address>
    Address 1<br />
    Address 2<br />
    City<br />
</address>
```




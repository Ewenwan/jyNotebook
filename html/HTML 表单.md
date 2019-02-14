## &lt;form&gt;元素

HTML表单用于收集用户输入

HTML表单由&lt;form&gt;元素定义

```HTML
<form>
……
</form>
```

---

## 表单元素

---

## &lt;input&gt;元素

## 属性

| type | button，checkbox，file，hidden，image，password，radio，reset，submit，text | 规定 input 元素的类型。 |
| :--- | :--- | :--- |
| value | value | 规定 input 元素的值。 |
| width | pixels% | 定义 input 字段的宽度。（适用于 type="image"） |

button 按钮、checkbox 复选框、radio 单选框、file 文件、hidden 隐藏、image 图像、password 密码

reset 重置、sumbit 提交、text 文本

---

## 文本输入

&lt;input type="text"&gt; 定义文本输入的单行输入字段

---

## 单选按钮输入

&lt;input type="text"&gt; 定义单选按钮

---

## 提交按钮

&lt;input type="submit"&gt; 定义提交表单的按钮

---

## form表单的action属性

action属性定义提交表单时执行的动作

```HTML
<form action="xxx.php">
```

表单提交到web服务器上的网页

---

## Method 属性

method 属性规定在提交表单时所用的 HTTP 方法（GET或POST）

---

## Name 属性

如果要正确地被提交，每个输入字段必须设置一个 name 属性。

---

## &lt;fieldset&gt;元素

&lt;fieldset&gt;\(字段集\)元素组合表单中的相关数据

&lt;legend&gt;元素为&lt;fieldset&gt;元素定义的标题

---

## HTML Form 属性

```HTML
<form action="action_page.php" method="GET" target="_blank" accept-charset="UTF-8"
ectype="application/x-www-form-urlencoded" autocomplete="off" novalidate>
 .
 form elements
 .
</form> 
```

**&lt;form&gt; 属性的列表：**

| 属性 | 描述 |
| :--- | :--- |
| accept-charset | 规定在被提交表单中使用的字符集（默认：页面字符集）。 |
| action | 规定向何处提交表单的地址（URL）（提交页面）。 |
| autocomplete | 规定浏览器应该自动完成表单（默认：开启）。 |
| enctype | 规定被提交数据的编码（默认：url-encoded）。 |
| method | 规定在提交表单时所用的 HTTP 方法（默认：GET）。 |
| name | 规定识别表单的名称（对于 DOM 使用：document.forms.name）。 |
| novalidate | 规定浏览器不验证表单。 |
| target | 规定 action 属性中地址的目标（默认：\_self）。 |




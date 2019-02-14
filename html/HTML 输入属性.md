## value 属性

_value_属性规定输入字段的初始值

### 实例

```HTML
<form action="">
  First name:<br>
  <input type="text" name="firstname" value="John">
 <br>
  Last name:<br>
 <input type="text" name="lastname">
</form> 
```

---

## readonly 属性

_readonly_属性规定输入字段为只读（不能修改）

---

## disabled 属性

_disabled_属性规定输入字段是禁用的。

---

## size 属性

_size_属性规定输入字段的尺寸（以字符计）

---

## maxlength 属性

_maxlength_属性规定输入字段允许的最大长度

---

## HTML5 属性

HTML5 为 &lt;input&gt; 增加了如下属性：

* autocomplete（自动完成）
* autofocus（自动聚焦）
* form
* formaction
* formenctype
* formmethod
* formnovalidate
* formtarget
* height 和 width
* list
* min 和 max
* multiple
* pattern \(regexp\)
* placeholder
* required
* step

并为 &lt;form&gt; 增加如需属性：

* autocomplete
* novalidate

---

## autocomplete 属性

autocomplete 属性规定表单或输入字段是否应该自动完成。

当自动完成开启，浏览器会基于用户之前的输入值自动填写值。

实例:

自动完成开启的HTML表单\(某个输入字段为off\)

```HTML
<form action="#" autocomplete="on">
   First name:<input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   E-mail: <input type="email" name="email" autocomplete="off"><br>
   <input type="submit">
</form> 
```

---

## novalidate 属性

novalidate 属性属于 &lt;form&gt; 属性。

如果设置，则 novalidate 规定在提交表单时不对表单数据进行验证。

```HTML
<form novalidate>
    E-mail:<input type="email" name="email"/>
</from>
```

---

## autofocus 属性

autofocus 属性是布尔属性。

如果设置，则规定当页面加载时 &lt;input&gt; 元素应该自动获得焦点。

### 实例

使 "First name" 输入字段在页面加载时自动获得焦点：

```HTML
First name:
<input type="text" name="fname" autofocus>
```

---

## form 属性

form 属性规定 &lt;input&gt; 元素所属的一个或多个表单。

提示：如需引用一个以上的表单，请使用空格分隔的表单 id 列表。

实例:

输入字段位于表单

```HTML
<form action="#" id="form1">
   First name: <input type="text" name="fname"><br>
   <input type="submit" value="Submit">
</form>

 Last name: <input type="text" name="lname" form="form1">
```

---

## formaction 属性

formaction 属性规定当提交表单时处理该输入控件的文件的 URL。

formaction 属性覆盖 &lt;form&gt; 元素的 action 属性。

formaction 属性适用于 type="submit" 以及 type="image"。

### 实例

拥有两个两个提交按钮并对于不同动作的 HTML 表单：

```HTML
<form action="#">
   First name: <input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   <input type="submit" value="Submit"><br>
   <input type="submit" formaction="#"
   value="Submit as admin">
</form> 
```

---

## formenctype 属性

formenctype 属性规定当把表单数据（form-data）提交至服务器时如何对其进行编码（仅针对 method="post" 的表单）。

formenctype 属性覆盖 &lt;form&gt; 元素的 enctype 属性。

formenctype 属性适用于 type="submit" 以及 type="image"。

### 实例

发送默认编码以及编码为 "multipart/form-data"（第二个提交按钮）的表单数据（form-data）：

```HTML
<form action="#" method="post">
   First name: <input type="text" name="fname"><br>
   <input type="submit" value="Submit">
   <input type="submit" formenctype="multipart/form-data"
   value="Submit as Multipart/form-data">
</form> 
```

---

## formmethod 属性

formmethod 属性定义用以向 action URL 发送表单数据（form-data）的 HTTP 方法。

formmethod 属性覆盖 &lt;form&gt; 元素的 method 属性。

formmethod 属性适用于 type="submit" 以及 type="image"。

### 实例

第二个提交按钮覆盖表单的 HTTP 方法：

```
<form action="#" method="get">
   First name: <input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   <input type="submit" value="Submit">
   <input type="submit" formmethod="post" formaction="#"
   value="Submit using POST">
</form> 
```

---

## formnovalidate 属性

novalidate 属性是布尔属性。

如果设置，则规定在提交表单时不对 &lt;input&gt; 元素进行验证。

formnovalidate 属性覆盖 &lt;form&gt; 元素的 novalidate 属性。

formnovalidate 属性可用于 type="submit"。

### 实例

拥有两个提交按钮的表单（验证和不验证）：

```
<form action="#">
   E-mail: <input type="email" name="userid"><br>
   <input type="submit" value="Submit"><br>
   <input type="submit" formnovalidate value="Submit without validation">
</form> 
```

---

## formtarget 属性

formtarget 属性规定的名称或关键词指示提交表单后在何处显示接收到的响应。

formtarget 属性会覆盖 &lt;form&gt; 元素的 target 属性。

formtarget 属性可与 type="submit" 和 type="image" 使用。

### 实例

这个表单有两个提交按钮，对应不同的目标窗口：

```
<form action="#">
   First name: <input type="text" name="fname"><br>
   Last name: <input type="text" name="lname"><br>
   <input type="submit" value="Submit as normal">
   <input type="submit" formtarget="_blank"
   value="Submit to a new window">
</form> 
```

---

## height 和 width 属性

height 和 width 属性规定 &lt;input&gt; 元素的高度和宽度。

height 和 width 属性仅用于 &lt;input type="image"&gt;。

注释：请始终规定图像的尺寸。如果浏览器不清楚图像尺寸，则页面会在图像加载时闪烁。

### 实例

把图像定义为提交按钮，并设置 height 和 width 属性：

```HTML
<input type="image" src="img_submit.gif" alt="Submit" width="48" height="48">
```

---

## list 属性

list 属性引用的 &lt;datalist&gt; 元素中包含了 &lt;input&gt; 元素的预定义选项。

### 实例

使用 &lt;datalist&gt; 设置预定义值的 &lt;input&gt; 元素：

```HTML
<input list="browsers">

<datalist id="browsers">
   <option value="Internet Explorer">
   <option value="Firefox">
   <option value="Chrome">
   <option value="Opera">
   <option value="Safari">
</datalist> 
```

---

## min 和 max 属性

min 和 max 属性规定 &lt;input&gt; 元素的最小值和最大值。

---

## multiple 属性

multiple 属性是布尔属性。

如果设置，则规定允许用户在 &lt;input&gt; 元素中输入一个以上的值。

---

## pattern 属性

pattern 属性规定用于检查 &lt;input&gt; 元素值的正则表达式。

---

## placeholder 属性

placeholder 属性规定用以描述输入字段预期值的提示（样本值或有关格式的简短描述）。

该提示会在用户输入值之前显示在输入字段中。

---

## required 属性

required 属性是布尔属性。

如果设置，则规定在提交表单之前必须填写输入字段。

---

## step 属性

step 属性规定 &lt;input&gt; 元素的合法数字间隔。

示例：如果 step="3"，则合法数字应该是 -3、0、3、6、等等。

提示：step 属性可与 max 以及 min 属性一同使用，来创建合法值的范围。




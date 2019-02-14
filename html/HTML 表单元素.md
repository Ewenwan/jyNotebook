## &lt;input&gt;元素

---

## &lt;select&gt;元素\(下拉列表\)

&lt;select&gt;元素定义下拉列表

```HTML
<select name="number">
    <option value="1">1</option>
    <option value="2">2</option>
</select>
```

&lt;option&gt;元素定义待选择的选项

列表通常会把首个想徐昂显示为被选选项

可以通过selected属性来定义预定义选项

```HTML
<option value="first" selected="selected">first</option>
```

---

## &lt;textarea&gt;元素

&lt;textarea&gt;元素定义多行输入字段\(文本域\)

实例:

```
<textarea name="message" rows="10" cols="10">angle</textarea>
```

---

## &lt;button&gt;元素

&lt;button&gt;元素定义可点击的按钮

```HTML
<button type="button" onclick="alert('Hello World')">Click Me</button>
```

---

## HTML5 表单元素

新增加元素:

* &lt;datalist&gt;
* &lt;keygen&gt;
* &lt;output&gt;

---

## HTML5 &lt;datalist&gt;元素

&lt;datalist&gt;元素为&lt;input&gt;元素规定预定义选项列表

```
<!DOCTYPE html>
<html>
  <body>
  <form action="/demo/demo_form.asp">
    <input list="browsers" name="browser">
      <datalist id="browsers">
        <option value="Internet Explorer">
        <option value="Firefox">
        <option value="Chrome">
        <option value="Opera">
        <option value="Safari">
      </datalist>
    <input type="submit">
  </form>
  </body>
</html>
```

输入一个相关的字符串，就会在输入框下方出现预选项


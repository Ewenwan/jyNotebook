## 表格

表格由&lt;table&gt;标签来定义。

每个表格均有若干行，每行由若干个单元格组成

行由&lt;tr&gt;标签定义

单元格由&lt;td&gt;标签定义

实例:

```HTML
<talbe border="1">
    <tr>
        <td>row 1,cell 1</td>
        <td>row 1,cell 2</td>
    </tr>
    <tr>
        <td>row 2,cell 1</td>
        <td>row 2,cell 2</td>
    </tr>
</table>
```

---

## 表格和边框属性

使用border属性定义边框

实例:

```
<talbe border="1">
    <tr>
        <td>row 1,cell 1</td>
        <td>row 1,cell 2</td>
    </tr>
</table>
```

---

## 表格的表头

表格的表头使用&lt;th&gt;标签来进行定义

```
<talbe border="1">
    <tr>
        <th>Heading</th>
        <th>Angle</th>
    </tr>
    <tr>
        <td>row 1,cell 1</td>
        <td>row 1,cell 2</td>
    </tr>
    <tr>
        <td>row 2,cell 1</td>
        <td>row 2,cell 2</td>
    </tr>
</table>
```

---

## 跨行跨列

colspan或rowspan属性设置跨越的列或行数

```HTML
<html>

<body>

<h4>横跨两列的单元格：</h4>
<table border="1">
<tr>
  <th>姓名</th>
  <th colspan="2">电话</th>
</tr>
<tr>
  <td>Bill Gates</td>
  <td>555 77 854</td>
  <td>555 77 855</td>
</tr>
</table>

<h4>横跨两行的单元格：</h4>
<table border="1">
<tr>
  <th>姓名</th>
  <td>Bill Gates</td>
</tr>
<tr>
  <th rowspan="2">电话</th>
  <td>555 77 854</td>
</tr>
<tr>
  <td>555 77 855</td>
</tr>
</table>

</body>
</html>

```

---

## 单元格的边距或间距

cellpadding属性

1.边距

```HTML
<html>

<body>

<h4>没有 cellpadding：</h4>
<table border="1">
<tr>
  <td>First</td>
  <td>Row</td>
</tr>   
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>

<h4>带有 cellpadding：</h4>
<table border="1" 
cellpadding="10">
<tr>
  <td>First</td>
  <td>Row</td>
</tr>   
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>

</body>
</html>
```

cellspacing属性

2.间距

```HTML
<html>

<body>

<h4>没有 cellspacing：</h4>
<table border="1">
<tr>
  <td>First</td>
  <td>Row</td>
</tr>   
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>

<h4>带有 cellspacing：</h4>
<table border="1" 
cellspacing="10">
<tr>
  <td>First</td>
  <td>Row</td>
</tr>   
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>

</body>
</html>

```



---

## 框架frame

* box\(盒\)
* above\(在上面\)
* below\(在下面\)

sides\(边\)

* hsides
* vsides

```HTML
<html>
<body>

<p><b>注释：</b>frame 属性无法在 Internet Explorer 中正确地显示。</p>

<p>Table with frame="box":</p>
<table frame="box">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>

<p>Table with frame="above":</p>
<table frame="above">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>

<p>Table with frame="below":</p>
<table frame="below">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>

<p>Table with frame="hsides":</p>
<table frame="hsides">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>

<p>Table with frame="vsides":</p>
<table frame="vsides">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>

</body>
</html>

```

---

##  表格标签

| 表格 | 描述 |
| :--- | :--- |
| [&lt;table&gt;](http://www.w3school.com.cn/tags/tag_table.asp) | 定义表格 |
| [&lt;caption&gt;](http://www.w3school.com.cn/tags/tag_caption.asp) | 定义表格标题。 |
| [&lt;th&gt;](http://www.w3school.com.cn/tags/tag_th.asp) | 定义表格的表头。 |
| [&lt;tr&gt;](http://www.w3school.com.cn/tags/tag_tr.asp) | 定义表格的行。 |
| [&lt;td&gt;](http://www.w3school.com.cn/tags/tag_td.asp) | 定义表格单元。 |
| [&lt;thead&gt;](http://www.w3school.com.cn/tags/tag_thead.asp) | 定义表格的页眉。 |
| [&lt;tbody&gt;](http://www.w3school.com.cn/tags/tag_tbody.asp) | 定义表格的主体。 |
| [&lt;tfoot&gt;](http://www.w3school.com.cn/tags/tag_tfoot.asp) | 定义表格的页脚。 |
| [&lt;col&gt;](http://www.w3school.com.cn/tags/tag_col.asp) | 定义用于表格列的属性。 |
| [&lt;colgroup&gt;](http://www.w3school.com.cn/tags/tag_colgroup.asp) | 定义表格列的组。 |




## css多列

* column-count
* column-gap
* column-rule

---

## CSS3 创建多列

column-count属性规定元素应该被分隔的列数

实例:把div元素中的文本分隔为三列

```
div{
    -moz-column-count:3;/*firefox*/
    -webkit-column-count:3;/*safari和chrome*/
    column-count:3;
}
```

---

## css3规定列之间的间隔

column-gap属性规定列之间的间隔

实例:规定列之间40像素的间隔

```
div{
    -moz-column-gap:40px;/*Firefox*/
    -webkit-column-gap:40px;/*safari和chrome*/
    column-gap:40px;
}
```

---

## css3列规则

column-rule属性设置列之间的宽度、样式和颜色规则

实例:规定列之间的宽度、样式和颜色规则

```
div{
    -moz-column-rule:3px outset red;
    -webkit-column-rule:3px outset red;
    column-rule:3px outset red;
}
```

## 新的多列属性

下面的表格列出了所有的转换属性：

| 属性 | 描述 | CSS |
| :--- | :--- | :--- |
| [column-count](http://www.w3school.com.cn/cssref/pr_column-count.asp) | 规定元素应该被分隔的列数。 | 3 |
| [column-fill](http://www.w3school.com.cn/cssref/pr_column-fill.asp) | 规定如何填充列。 | 3 |
| [column-gap](http://www.w3school.com.cn/cssref/pr_column-gap.asp) | 规定列之间的间隔。 | 3 |
| [column-rule](http://www.w3school.com.cn/cssref/pr_column-rule.asp) | 设置所有 column-rule-\* 属性的简写属性。 | 3 |
| [column-rule-color](http://www.w3school.com.cn/cssref/pr_column-rule-color.asp) | 规定列之间规则的颜色。 | 3 |
| [column-rule-style](http://www.w3school.com.cn/cssref/pr_column-rule-style.asp) | 规定列之间规则的样式。 | 3 |
| [column-rule-width](http://www.w3school.com.cn/cssref/pr_column-rule-width.asp) | 规定列之间规则的宽度。 | 3 |
| [column-width](http://www.w3school.com.cn/cssref/pr_column-width.asp) | 规定列的宽度。 | 3 |
| [columns](http://www.w3school.com.cn/cssref/pr_columns.asp) | 规定设置 column-width 和 column-count 的简写属性。 | 3 |






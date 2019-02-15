### 列表类型

list-style-type属性设置列表项标记的类型

可选值:

| 值 | 描述 |
| :--- | :--- |
| none | 无标记 |
| disc | 默认,标记是实心圆 |
| circle | 标记是空心圆 |
| square | 标记是实心方块 |
| decimal | 标记是数字 |
| decimal-leading-zero | 0开头的数字标记，例如:00,01…… |
| lower-roman | 小写罗马数字，例如:i,ii,iii,iv…… |
| upper-roman | 大写罗马数字，例如I，II，III,IV…… |
| lower-alpha | 小写英文字母 |

| hebrew | 传统的希伯来编号方式 |
| :--- | :--- |
| armenian | 传统的亚美尼亚编号方式 |
| georgian | 传统的乔治亚编号方式\(an, ban, gan, 等。\) |
| cjk-ideographic | 简单的表意数字 |
| hiragana | 标记是：a, i, u, e, o, ka, ki, 等。（日文片假名） |
| katakana | 标记是：A, I, U, E, O, KA, KI, 等。（日文片假名） |
| hiragana-iroha | 标记是：i, ro, ha, ni, ho, he, to, 等。（日文片假名） |
| katakana-iroha | 标记是：I, RO, HA, NI, HO, HE, TO, 等。（日文片假名） |

---

## 列表项图像

list-style-image属性使用图像来替换列表项的标记

可选值:

url:图像的路径

none:默认。无图像被显示

```HTML
li{
    list-style-image:url(xxx.gif);
}
```

---

## 列表标志位置

list-style-position属性设置在何处放置列表项标记

可选值:

inside:列表项目标记放置在文本以内，且环绕文本根据标记对齐

outside:默认值。保持标记位于文本的左侧。列表项目标记放置在文本以外，且环绕文本不根据标记对齐

---

## 简写列表样式

list-style简写属性在一个声明中设置所有的列表属性

可以按顺序设置如下属性：

* list-style-type
* list-style-position
* list-style-image

---

## CSS 列表属性\(list\)

| 属性 | 描述 |
| :--- | :--- |
| list-style | 简写属性。用于把所有用于列表的属性设置于一个声明中。 |
| [l](http://www.w3school.com.cn/cssref/pr_list-style-image.asp)list-style-image | 将图象设置为列表项标志。 |
| list-style-position | 设置列表中列表项标志的位置。 |
| list-style-type | 设置列表项标志的类型。 |
| marker-offset |  |




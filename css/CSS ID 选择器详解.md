## CSS ID 选择器

在某些方面，ID 选择器类似于类选择器，不过也有一些重要差别。

### 语法

首先，ID 选择器前面有一个 \# 号 - 也称为棋盘号或井号。

请看下面的规则：

```
*#intro {font-weight:bold;}
```

与类选择器一样，ID 选择器中可以忽略通配选择器。前面的例子也可以写作：

```
#intro {font-weight:bold;}
```

这个选择器的效果将是一样的。

第二个区别是 ID 选择器不引用 class 属性的值，毫无疑问，它要引用 id 属性中的值。

以下是一个实际 ID 选择器的例子：

```
<p id="intro">This is a paragraph of introduction.</p>
```

_tips:id只能在文档中使用一次_


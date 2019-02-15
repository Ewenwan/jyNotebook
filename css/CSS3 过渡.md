## CSS3 过渡

通过 CSS3，我们可以在不使用 Flash 动画或 JavaScript 的情况下，当元素从一种样式变换为另一种样式时为元素添加效果。

## 过渡属性

下面的表格列出了所有的转换属性：

| 属性 | 描述 |
| :--- | :--- |
| transition | 简写属性，用于在一个属性中设置四个过渡属性。 |
| transition-property | 规定应用过渡的 CSS 属性的名称。 |
| transition-duration | 定义过渡效果花费的时间。默认是 0。 |
| transition-timing-function | 规定过渡效果的时间曲线。默认是 "ease"。 |
| transition-delay | 规定过渡效果何时开始。默认是 0。 |

# transition-timing-function 属性

```
transition-timing-function: linear|ease|ease-in|ease-out|ease-in-out|cubic-
bezier(n,n,n,n);
```

| 值 | 描述 |
| :--- | :--- |
| linear | 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier\(0,0,1,1\)）。 |
| ease | 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier\(0.25,0.1,0.25,1\)）。 |
| ease-in | 规定以慢速开始的过渡效果（等于 cubic-bezier\(0.42,0,1,1\)）。 |
| ease-out | 规定以慢速结束的过渡效果（等于 cubic-bezier\(0,0,0.58,1\)）。 |
| ease-in-out | 规定以慢速开始和结束的过渡效果（等于 cubic-bezier\(0.42,0,0.58,1\)）。 |
| cubic-bezier\(n,n,n,n\) | 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。 |




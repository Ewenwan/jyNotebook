## :结构伪类

_简单说明:_

| 值 | 描述 |
| :--- | :--- |
| :first-child | 选择某个元素的第一个子元素 |
| :last-child | 选择某个元素的最后一个子元素 |
| :nth-child\(\) | 选择某个元素的一个或多个特定的子元素 |
| :nth-last-child\(\) | 选择某个元素的一个或多个特定的子元素，从这个元素的最后一个子元素开始计算 |
| :nth-of-type\(\) | 选择指定的元素 |
| :nth-last-of-type\(\) | 选择指定的元素，从元素的最后一个开始计算 |
| :first-of-type\(\) | 选择一个上级元素下的第一个同类子元素 |
| :last-of-type\(\) | 选择一个上级元素的最后一个同类子元素 |
| :only-child\(\) | 选择的元素是它的父元素的唯一一个子元素 |
| :only-of-type | 选择一个元素是它的上级元素的唯一一个相同类型的子元素 |
| :empty | 选择的元素里面是没有任何内容 |

_部分值解释:_

## :nth-child\(\)

```css
:nth-child(length);/*参数是具体数字*/
:nth-child(n);/*参数是n，n从0开始计算*/
:nth-child(n*length);/*n的倍数选择，n从0开始计算*/
:nth-child(n+length);/*选择大于length后面的元素*/
:nth-child(-n+length);/*选择大于length前面的元素*/
:nth-child(n*length+1);/*表示隔几选一*/
```

* :nth-child\(2n\)等价于:nth-child\(even\),选取偶数
* :nth-child\(2n-1\)等价于:nth-child\(odd\),选取奇数

---

## 否定伪类

:not\(\)表示否定选择器，即排除或者过滤掉特定元素。

……

## 锚伪类与其他伪类

| 属性 | 描述 |
| :--- | :--- |
| :active | 向被激活的元素添加样式。 |
| :focus | 向拥有键盘输入焦点的元素添加样式。 |
| :hover | 当鼠标悬浮在元素上方时，向元素添加样式。 |
| :link | 向未被访问的链接添加样式。 |
| :visited | 向已被访问的链接添加样式。 |




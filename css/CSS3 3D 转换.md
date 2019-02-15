## 3D转换

方法:

* rotateX\(\)
* rotateY\(\)

---

## rotateX\(\)方法

通过rotateX\(\)，元素围绕其x轴以给定的读书进行旋转

```
div{
    transform:rotateX(120deg);
    -webkit-transform:rotate(120deg);/*Safari和Chrome*/
    -moz-transform:rotateX(120deg);/*Firefox*/
}
```

---

## rotateY\(\)方法

通过rotateY\(\)方法,元素围绕其Y轴以给定的度数进行旋转

```
div{
    transform:rotateY(130deg);
    -webkit-transform:rotateY(130deg);/*Safari和Chrome*/
    -moz-transform:rotateY(130deg);/*Firefox*/
}
```

---

## 转换属性

下面的表格列出了所有的转换属性：

| 属性 | 描述 |
| :--- | :--- |
| transform | 向元素应用 2D 或 3D 转换。 |
| transform-origin | 允许你改变被转换元素的位置。 |
| transform-style | 规定被嵌套元素如何在 3D 空间中显示。 |
| perspective | 规定 3D 元素的透视效果。 |
| perspective-origin | 规定 3D 元素的底部位置。 |
| backface-visibility | 定义元素在不面对屏幕时是否可见。 |

## transform-origin属性

## 语法

```
transform-origin: x-axis y-axis z-axis
```

| 值 | 描述 |
| :--- | :--- |
| x-axis | 定义视图被置于 X 轴的何处。可能的值：leftcenterrightlength% |
| y-axis | 定义视图被置于 Y 轴的何处。可能的值：topcenterbottomlength% |
| z-axis | 定义视图被置于 Z 轴的何处。可能的值：length |

## transform-style属性

transform-style 属性规定如何在 3D 空间中呈现被嵌套的元素。

```
transform-style: flat|preserve-3d;
```

| 值 | 描述 |
| :--- | :--- |
| flat | 子元素将不保留其 3D 位置。 |
| preserve-3d | 子元素将保留其 3D 位置。 |

# perspective 属性

perspective 属性定义 3D 元素距视图的距离，以像素计。该属性允许您改变 3D 元素查看 3D 元素的视图。当为元素定义 perspective 属性时，其子元素会获得透视效果，而不是元素本身。

```
perspective: number|none;
```

| 值 | 描述 |
| :--- | :--- |
| number | 元素距离视图的距离，以像素计。 |
| none | 默认值。与 0 相同。不设置透视 |

# perspective-origin 属性

perspective-origin 属性定义 3D 元素所基于的 X 轴和 Y 轴。该属性允许您改变 3D 元素的底部位置。

当为元素定义 perspective-origin 属性时，其子元素会获得透视效果，而不是元素本身。

```
perspective-origin: x-axis y-axis;
```

| 值 | 描述 |
| :--- | :--- |
| x-axis | 定义该视图在 x 轴上的位置。默认值：50%。可能的值：leftcenterrightlength% |
| y-axis | 定义该视图在 y 轴上的位置。默认值：50%。可能的值：topcenterbottomlength% |

# backface-visibility 属性

backface-visibility 属性定义当元素不面向屏幕时是否可见。

如果在旋转元素不希望看到其背面时，该属性很有用。

```
backface-visibility: visible|hidden;
```

| 值 | 描述 |
| :--- | :--- |
| visible | 背面是可见的。 |
| hidden | 背面是不可见的。 |

## 2D Transform 方法

| 函数 | 描述 |
| :--- | :--- |
| matrix3d\(n,n,n,n,n,n, n,n,n,n,n,n,n,n,n,n\) | 定义 3D 转换，使用 16 个值的 4x4 矩阵。 |
| translate3d\(x,y,z\) | 定义 3D 转化。 |
| translateX\(x\) | 定义 3D 转化，仅使用用于 X 轴的值。 |
| translateY\(y\) | 定义 3D 转化，仅使用用于 Y 轴的值。 |
| translateZ\(z\) | 定义 3D 转化，仅使用用于 Z 轴的值。 |
| scale3d\(x,y,z\) | 定义 3D 缩放转换。 |
| scaleX\(x\) | 定义 3D 缩放转换，通过给定一个 X 轴的值。 |
| scaleY\(y\) | 定义 3D 缩放转换，通过给定一个 Y 轴的值。 |
| scaleZ\(z\) | 定义 3D 缩放转换，通过给定一个 Z 轴的值。 |
| rotate3d\(x,y,z,angle\) | 定义 3D 旋转。 |
| rotateX\(angle\) | 定义沿 X 轴的 3D 旋转。 |
| rotateY\(angle\) | 定义沿 Y 轴的 3D 旋转。 |
| rotateZ\(angle\) | 定义沿 Z 轴的 3D 旋转。 |
| perspective\(n\) | 定义 3D 转换元素的透视视图。 |




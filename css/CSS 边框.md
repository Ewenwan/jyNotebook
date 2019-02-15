1. _tips:元素的边框\(border\)是围绕元素内容和内边距的一条或多条线_

2. ## 边框样式

border-style属性用于设置元素所有边框的样式，或者单独地为各边设置边框样式

实例1:

```HTML
border-style:dotted solid double dashed
```

* 上边框是点状
* 右边框是实现
* 下边框是双线
* 左边框是虚线

实例2:

```HTML
border-style:dotted solid double;
```

* 上边框是点状
* 右边框和左边框是实线
* 下边框是双线

实例3:

```HTML
border-style:dotted solid;
```

* 上边框和下边框是点状
* 右边框和左边框是实线

实例4:

```
border-style:dotted;
```

* 所有4个边框都是点状

---

可选值:

| 值 | 描述 |
| :--- | :--- |
| none | 定义无边框 |
| hidden | hidden用于解决边冲突 |
| dotted | 定义点状边框 |
| dashed | 定义虚线 |
| solid | 定义实线 |
| double | 定义双线。双线的宽度等于border-width的值 |
| groove | 定义3D凹槽边框。其效果取决于border-color的值 |
| ridge | 定义3D垄状边框。其效果取决于border-color的值 |
| inset | 定义3Dinset边框。其效果取决于border-color的值 |
| outset | 定义3Doutset边框。其效果取决于border-color的值 |

---

## 定义单边样式

* border-top-style
* border-rigtht-style
* border-bottom-style
* border-left-style

---

## 边框的宽度

border-width简写属性为元素的所有边框设置宽度，或者单独地位各边边框设置宽度

_tips:只有当边框样式不是none时才起作用。如果边框样式是none，边框宽度实际上会重置为0_

实例1:

```
border-width:thin medium thick 10px;
```

* 上边框是细边框
* 右边框是中等边框
* 下边框是粗边框
* 左边框是10px宽的边框

实例2:

```
border-width:thin medium thick;
```

* 上边框是10px
* 右边框和左边框是中等边框
* 下边框是粗边框

实例3:

```
border-width:thin medium;
```

* 上边框和下边框是细边框
* 右边框和左边框是中等边框

实例4:

```
border-width:thin;
```

```
所有4个边框都是细边框
```

---

可选值:

| 值 | 描述 |
| :--- | :--- |
| thin | 定义细的边框 |
| medium | 默认。定义中等的边框 |
| thick | 定义粗的边框 |
| length | 允许自定义边框的宽度 |

---

## 定义单边宽度

* border-top-width
* border-right-width
* border-left-width
* border-bottom-width

---

## 边框的颜色

border-color属性设置四条边框的颜色

实例1:

```
border-color:red green blue pink;
```

* 上边框是红色
* 右边框是绿色
* 下边框是蓝色
* 左边框是粉色

实例2:

```
border-color:red green blue;
```

* 上边框是红色
* 右边框和左边框是绿色
* 下边框是蓝色

实例3:

```
border-color:red green;
```

* 上边框和下边框是红色
* 右边框和左边框是绿色

实例4:

```
border-color:red;
```

* 四个边框都是红色

---

可选值:

| 值 | 描述 |
| :--- | :--- |
| color\_name | 规定颜色值为颜色名称的边框颜色 |
| hex\_number | 规定颜色值为十六进制值得边框颜色 |
| rgb\_number | 规定颜色值为rgb代码的边框颜色 |
| transparent | 默认值。边框颜色为透明 |

---

## 定义单边颜色

* border-top-color
* border-right-color
* border-bottom-color
* border-left-color

---

## CSS 边框属性

| 属性 | 描述 |
| :--- | :--- |
| border | 简写属性，用于把针对四个边的属性设置在一个声明。 |
| border-style | 用于设置元素所有边框的样式，或者单独地为各边设置边框样式。 |
| border-width | 简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。 |
| border-color | 简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。 |
| border-bottom | 简写属性，用于把下边框的所有属性设置到一个声明中。 |
| border-bottom-color | 设置元素的下边框的颜色。 |
| border-bottom-style | 设置元素的下边框的样式。 |
| border-bottom-width | 设置元素的下边框的宽度。 |
| border-left | 简写属性，用于把左边框的所有属性设置到一个声明中。 |
| border-left-color | 设置元素的左边框的颜色。 |
| border-left-style | 设置元素的左边框的样式。 |
| border-left-width | 设置元素的左边框的宽度。 |
| border-right | 简写属性，用于把右边框的所有属性设置到一个声明中。 |
| border-right-color | 设置元素的右边框的颜色。 |
| border-right-style | 设置元素的右边框的样式。 |
| border-right-width | 设置元素的右边框的宽度。 |
| border-top | 简写属性，用于把上边框的所有属性设置到一个声明中。 |
| border-top-color | 设置元素的上边框的颜色。 |
| border-top-style | 设置元素的上边框的样式。 |
| border-top-width | 设置元素的上边框的宽度。 |




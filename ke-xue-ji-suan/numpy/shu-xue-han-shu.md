### 三角函数

| [`sin`](#)（x，/ \[，out，where，cast，order，...\]） | 三角正弦，元素。 |
| :--- | :--- |
| [`cos`](#)（x，/ \[，out，where，cast，order，...\]） | 余弦元素。 |
| [`tan`](#)（x，/ \[，out，where，cast，order，...\]） | 计算切线元素。 |
| [`arcsin`](#)（x，/ \[，out，where，cast，order，...\]） | 反正弦，元素。 |
| [`arccos`](#)（x，/ \[，out，where，cast，order，...\]） | 三角反余弦，元素方式。 |
| [`arctan`](#)（x，/ \[，out，where，cast，order，...\]） | 三角反正切，逐元素。 |
| [`hypot`](#)（x1，x2，/ \[，out，where，cast，...\]） | 给定直角三角形的“腿”，返回其斜边。 |
| [`arctan2`](#)（x1，x2，/ \[，out，where，cast，...\]） | `x1/x2`正确选择象限的逐元素反正切。 |
| [`degrees`](#)（x，/ \[，out，where，cast，order，...\]） | 将角度从弧度转换为度数。 |
| [`radians`](#)（x，/ \[，out，where，cast，order，...\]） | 将角度从度数转换为弧度。 |
| [`unwrap`](#)（p \[，discont，axis\]） | 通过将值之间的增量更改为2 \* pi补充来展开。 |
| [`deg2rad`](#)（x，/ \[，out，where，cast，order，...\]） | 将角度从度数转换为弧度。 |
| [`rad2deg`](#)（x，/ \[，out，where，cast，order，...\]） | 将角度从弧度转换为度数。 |

## 双曲函数

| [`sinh`](#)（x，/ \[，out，where，cast，order，...\]） | 双曲正弦，元素。 |
| :--- | :--- |
| [`cosh`](#)（x，/ \[，out，where，cast，order，...\]） | 双曲余弦，元素。 |
| [`tanh`](#)（x，/ \[，out，where，cast，order，...\]） | 计算双曲正切元素。 |
| [`arcsinh`](#)（x，/ \[，out，where，cast，order，...\]） | 逆双曲正弦元素。 |
| [`arccosh`](#)（x，/ \[，out，where，cast，order，...\]） | 反双曲余弦，元素。 |
| [`arctanh`](#)（x，/ \[，out，where，cast，order，...\]） | 逆双曲正切元素。 |

## Rounding

| [`around`](#)（a \[，小数，out\]） | 均匀舍入到给定的小数位数。 |
| :--- | :--- |
| [`round_`](#)（a \[，小数，out\]） | 将数组舍入到给定的小数位数。 |
| [`rint`](#)（x，/ \[，out，where，cast，order，...\]） | 将数组的元素舍入为最接近的整数。 |
| [`fix`](#)（x \[，out\]） | 向零舍入到最接近的整数。 |
| [`floor`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回输入的底限。 |
| [`ceil`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回输入的上限。 |
| [`trunc`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回输入的截断值。 |

## 总和，产品，差异

| [`prod`](#)（a \[，axis，dtype，out，keepdims，initial\]） | 返回给定轴上的数组元素的乘积。 |
| :--- | :--- |
| [`sum`](#)（a \[，axis，dtype，out，keepdims，initial\]） | 给定轴上的数组元素的总和。 |
| [`nanprod`](#)（a \[，axis，dtype，out，keepdims\]） | 返回给定轴上的数组元素的乘积，将非数字（NaN）视为1。 |
| [`nansum`](#)（a \[，axis，dtype，out，keepdims\]） | 返回给定轴上的数组元素的总和，将非数字（NaN）视为零。 |
| [`cumprod`](#)（a \[，轴，dtype，out\]） | 返回给定轴上元素的累积乘积。 |
| [`cumsum`](#)（a \[，轴，dtype，out\]） | 返回给定轴上元素的累积和。 |
| [`nancumprod`](#)（a \[，轴，dtype，out\]） | 返回给定轴上的数组元素的累积乘积，将非数字（NaN）视为一个。 |
| [`nancumsum`](#)（a \[，轴，dtype，out\]） | 返回给定轴上的数组元素的累积和，将非数字（NaN）视为零。 |
| [`diff`](#)（a \[，n，轴\]） | 计算沿给定轴的第n个离散差。 |
| [`ediff1d`](#)（ary \[，to\_end，to\_begin\]） | 数组的连续元素之间的差异。 |
| [`gradient`](#)（f，\* varargs，\*\* kwargs） | 返回N维数组的渐变。 |
| [`cross`](#)（A，B \[，Axisa，axisb，axisc，轴\]） | 返回两个（数组）向量的叉积。 |
| [`trapz`](#)（y \[，x，dx，轴\]） | 使用复合梯形法则沿给定轴积分。 |

## 指数和对数

| [`exp`](#)（x，/ \[，out，where，cast，order，...\]） | 计算输入数组中所有元素的指数。 |
| :--- | :--- |
| [`expm1`](#)（x，/ \[，out，where，cast，order，...\]） | 计算数组中的所有元素。`exp(x)-1` |
| [`exp2`](#)（x，/ \[，out，where，cast，order，...\]） | 计算输入数组中所有_p的2 \*\* p_。 |
| [`log`](#)（x，/ \[，out，where，cast，order，...\]） | 自然对数，元素方面。 |
| [`log10`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回输入数组的基数10对数。 |
| [`log2`](#)（x，/ \[，out，where，cast，order，...\]） | _x的_基数为2的对数。 |
| [`log1p`](#)（x，/ \[，out，where，cast，order，...\]） | 返回一个加上输入数组的自然对数，逐个元素。 |
| [`logaddexp`](#)（x1，x2，/ \[，out，where，cast，...\]） | 输入的取幂之和的对数。 |
| [`logaddexp2`](#)（x1，x2，/ \[，out，where，cast，...\]） | base-2中输入的取幂之和的对数。 |

## 其他特殊功能

| [`i0`](#)（X） | 修改了第一类贝塞尔函数，阶数为0。 |
| :--- | :--- |
| [`sinc`](#)（X） | 返回sinc函数。 |

## 浮点例程

| [`signbit`](#)（x，/ \[，out，where，cast，order，...\]） | 返回元素为True设置signbit（小于零）。 |
| :--- | :--- |
| [`copysign`](#)（x1，x2，/ \[，out，where，cast，...\]） | 将元素x1的符号更改为x2的符号。 |
| [`frexp`](#)（x \[，out1，out2\]，/ \[\[，out，where，...\]） | 将x的元素分解为尾数和二进制指数。 |
| [`ldexp`](#)（x1，x2，/ \[，out，where，cast，...\]） | 以元素方式返回x1 \* 2 \*\* x2。 |
| [`nextafter`](#)（x1，x2，/ \[，out，where，cast，...\]） | 将x1之后的下一个浮点值返回x2（元素方向）。 |
| [`spacing`](#)（x，/ \[，out，where，cast，order，...\]） | 返回x与最近的相邻数字之间的距离。 |

## 理性例程

| [`lcm`](#)（x1，x2，/ \[，out，where，cast，order，...\]） | 返回\` | x1 | `和的最小公倍数` | x2 | \` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [`gcd`](#)（x1，x2，/ \[，out，where，cast，order，...\]） | 返回\` | x1 | `和的最大公约数` | x2 | \` |

## 算术运算

| [`add`](#)（x1，x2，/ \[，out，where，cast，order，...\]） | 按元素添加参数。 |
| :--- | :--- |
| [`reciprocal`](#)（x，/ \[，out，where，cast，...\]） | 以元素为单位返回参数的倒数。 |
| [`positive`](#)（x，/ \[，out，where，cast，order，...\]） | 数字正面，元素方面。 |
| [`negative`](#)（x，/ \[，out，where，cast，order，...\]） | 数字否定，元素方面。 |
| [`multiply`](#)（x1，x2，/ \[，out，where，cast，...\]） | 元素相乘的论证。 |
| [`divide`](#)（x1，x2，/ \[，out，where，cast，...\]） | 以元素方式返回输入的真正除法。 |
| [`power`](#)（x1，x2，/ \[，out，where，cast，...\]） | 第一个数组元素从第二个数组提升到幂，逐个元素。 |
| [`subtract`](#)（x1，x2，/ \[，out，where，cast，...\]） | 从元素方面减去参数。 |
| [`true_divide`](#)（x1，x2，/ \[，out，where，...\]） | 以元素方式返回输入的真正除法。 |
| [`floor_divide`](#)（x1，x2，/ \[，out，where，...\]） | 返回小于或等于输入除法的最大整数。 |
| [`float_power`](#)（x1，x2，/ \[，out，where，...\]） | 第一个数组元素从第二个数组提升到幂，逐个元素。 |
| [`fmod`](#)（x1，x2，/ \[，out，where，cast，...\]） | 返回除法的元素余数。 |
| [`mod`](#)（x1，x2，/ \[，out，where，cast，order，...\]） | 返回除法元素的余数。 |
| [`modf`](#)（x \[，out1，out2\]，/ \[\[，out，where，...\]） | 以元素方式返回数组的分数和整数部分。 |
| [`remainder`](#)（x1，x2，/ \[，out，where，cast，...\]） | 返回除法元素的余数。 |
| [`divmod`](#)（x1，x2 \[，out1，out2\]，/ \[\[，out，...\]） | 同时返回逐元素的商和余数。 |

## 处理复数

| [`angle`](#)（z \[，deg\]） | 返回复杂参数的角度。 |
| :--- | :--- |
| [`real`](#)（小时） | 返回复杂参数的实部。 |
| [`imag`](#)（小时） | 返回复杂参数的虚部。 |
| [`conj`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回复共轭。 |

## Miscellaneous

| [`convolve`](#)（a，v \[，mode\] | 返回两个一维序列的离散线性卷积。 |
| :--- | :--- |
| [`clip`](#)（a，a\_min，a\_max \[，out\]） | 剪辑（限制）数组中的值。 |
| [`sqrt`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回数组的非负平方根。 |
| [`cbrt`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式返回数组的立方根。 |
| [`square`](#)（x，/ \[，out，where，cast，order，...\]） | 返回输入的元素方块。 |
| [`absolute`](#)（x，/ \[，out，where，cast，order，...\]） | 逐个元素地计算绝对值。 |
| [`fabs`](#)（x，/ \[，out，where，cast，order，...\]） | 以元素方式计算绝对值。 |
| [`sign`](#)（x，/ \[，out，where，cast，order，...\]） | 返回数字符号的元素指示。 |
| [`heaviside`](#)（x1，x2，/ \[，out，where，cast，...\]） | 计算Heaviside阶跃函数。 |
| [`maximum`](#)（x1，x2，/ \[，out，where，cast，...\]） | 元素最大数组元素。 |
| [`minimum`](#)（x1，x2，/ \[，out，where，cast，...\]） | 元素最小的数组元素。 |
| [`fmax`](#)（x1，x2，/ \[，out，where，cast，...\]） | 元素最大数组元素。 |
| [`fmin`](#)（x1，x2，/ \[，out，where，cast，...\]） | 元素最小的数组元素。 |
| [`nan_to_num`](#)（x \[，副本\]） | 用大有限数替换NaN为零和无穷大。 |
| [`real_if_close`](#)（来自\[，tol\]） | 如果复杂输入返回真实数组，如果复杂零件接近于零。 |
| [`interp`](#)（x，xp，fp \[，left，right，period\]） | 一维线性插值 |




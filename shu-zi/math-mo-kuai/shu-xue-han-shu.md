现在看下数学函数的用法

| 函数 | 返回值 \( 描述 \) |
| :--- | :--- |
| abs\(x\) | 返回数字的绝对值，如abs\(-10\) 返回 10，注意这个是内置函数，不需要使用math模块 |
| ceil\(x\) | 返回数字的上入整数，如math.ceil\(4.1\) 返回 5 |
| copysign\(x,y\) | 返回一个浮点数，其大小\(绝对值\)为x，但符号为y，如math.copysign\(2.0,-3.0\) 返回 -2.0 |
| cmp\(x, y\) | 如果 x &lt; y 返回 -1, 如果 x == y 返回 0, 如果 x &gt; y 返回 1。**Python 3 已废弃**。使用**使用 \(x&gt;y\)-\(x&lt;y\)**替换。 |
| exp\(x\) | 返回e的x次幂\(ex\),如math.exp\(1\) 返回2.718281828459045 |
| fabs\(x\) | 返回数字的绝对值，如math.fabs\(-10\) 返回10.0 |
| factorial\(x\) | 返回x的阶乘。如果x不是整数或者为负，则引发ValueError |
| floor\(x\) | 返回数字的下舍整数，如math.floor\(4.9\)返回 4 |
| fmod\(x,y\) | 返回浮点数之间模运算，比如math.fmod\(2.0,3.0\) 返回2.0 |
| fsum\(\[x1,x2...\]\) | 返回迭代中的精确浮点值，比如math.fsum\(\[.1,.2,.3\]\)返回值为0.6，如果使用sum\(\)计算，返回值为0.6000000000000001 |
| gcd\(a,b\) | 返回a和b之间的最大公约数，比如math.gcd\(36,54\)，返回值为18 |
| isfinite\(x\) | 如果x既不是无穷大也不是Nan，则返回 |
| isinf\(x\) | 如果x是正或负无穷大，则返回True，否者返回False |
| isnan\(x\) | 如果x是NaN\(不是数字\)，则返回True，否则返回False |
| ldexp\(x,i\) | 返回x\*\(2\*\*\(i+1\)\),是函数frexp\(\)的反函数,比如math.ldexp\(4,3\) 返回值为32 |
| log\(x\) | 如math.log\(math.e\)返回1.0,math.log\(100,10\)返回2.0 |
| log2\(x\) | 返回以2为底的对数 |
| log1p\(x\) | 返回以1+x为基数的x的对数 |
| log10\(x\) | 返回以10为基数的x的对数，如math.log10\(100\)返回 2.0 |
| max\(x1, x2,...\) | 返回给定参数的最大值，参数可以为序列。 |
| min\(x1, x2,...\) | 返回给定参数的最小值，参数可以为序列。 |
| modf\(x\) | 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。 |
| pow\(x, y\) | x\*\*y 运算后的值。 |
| round\(x \[,n\]\) | 返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数。 |
| sqrt\(x\) | 返回数字x的平方根。 |
| trunc\(x\) | 返回实数的整数部分 |
| 特殊功能 |  |
| erf\(x\) | 返回[标准正太分布](https://en.wikipedia.org/wiki/Normal_distribution#Cumulative_distribution_function)值 |
| erfc\(x\) | 返回1.0-erf\(x\) |
| gamma\(x\) | 在x处返回[Gamma函数](https://en.wikipedia.org/wiki/Gamma_function) |
| lgamma\(x\) | 在返回Gamma函数的绝对值的自然对数x |




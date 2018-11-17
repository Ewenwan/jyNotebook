* random模块为各种分布实现伪随机数生成器

| 整数函数 | 描述 |
| :--- | :--- |
| random.randrange\(stop\) | 从0-end\(但不包括end\)的序列中随机抽取一个数 |
| random.randrange\(start，stop\[，step\] \) | 从中返回随机选择的元素。这相当于，但实际上并不构建范围对象。range\(start, stop, step\),choice\(range\(start, stop, step\)\) |
| random.randint\(a，b \) | 返回一个随机整数N,范围为a&lt;=x&lt;=b |
| random.getrandbits\(k\) |  |
| 序列函数 |  |
| random.choice\(seq\) | 从非空序列seq返回一个随机元素。如果seq为空，则报IndexError |
| random.shuffle\(x\[, random\]\) | 打乱序列中元素的顺序，比如:a=\[1,2,3,4,\],然后使用random.shuffle\(a\),这样就可以将a序列打乱了 |
| random.sample\(population, k\) | 随机从population序列中提取k个不同元素的样本 |
| 分布函数 |  |
| random.random\(\) |  |
| random.uniform\(a，b \) | 返回随机浮点数N,a &lt;= N &lt;= b |
| random.triangular\(低，高，模式\) | 返回一个随机浮点数N，以便在这些边界之间使用指定的模式。该低和高界默认的0和1。所述模式参数默认为边界之间的中点，给人一种对称分布。low &lt;= N &lt;= high |
| random.betavariate\(alpha，beta \) | Beta分布。参数的条件是和 。返回值的范围介于0和1之间。alpha &gt; 0beta &gt; 0 |
| random.expovariate（lambd ） | 指数分布。 lambd是1.0除以所需的平均值。它应该是非零的。（该参数将被称为“拉姆达”，但是这是在Python保留字。）返回值的范围从0到正无穷大如果lambd为正，且从负无穷大到0，如果lambd为负 |
| random.gammavariate\(alpha，beta\) | Gamma分布,参数的条件是和。alpha &gt; 0beta &gt; 0 |
| random.gauss\(mu, sigma\) | 高斯分布。 mu是平均值，sigma是标准偏差。比normalvariate\(\)函数稍快 |
| random.lognormvariate\(mu, sigma\) | 记录正态分布 |
| random.normalvariate\(mu, sigma\) | 正态分布。 mu是平均值，sigma是标准偏差 |
| random.vonmisesvariate\(mu, kappa\) | mu是平均角度，以弧度表示，介于0和2 \* pi之间，kappa 是浓度参数，必须大于或等于零。如果 kappa等于零，则该分布在0到2 \* pi的范围内减小到均匀的随机角度 |
| random.paretovariate\(alpha\) | 帕累托分布。 alpha是形状参数 |
| random.weibullvariate\(alpha, beta\) | 威布尔分布。 alpha是scale参数，beta是shape参数。 |

```
>>> random()                             # Random float:  0.0 <= x < 1.0
0.37444887175646646

>>> uniform(2.5, 10.0)                   # Random float:  2.5 <= x < 10.0
3.1800146073117523

>>> expovariate(1 / 5)                   # Interval between arrivals averaging 5 seconds
5.148957571865031

>>> randrange(10)                        # Integer from 0 to 9 inclusive
7

>>> randrange(0, 101, 2)                 # Even integer from 0 to 100 inclusive
26

>>> choice(['win', 'lose', 'draw'])      # Single random element from a sequence
'draw'

>>> deck = 'ace two three four'.split()
>>> shuffle(deck)                        # Shuffle a list
>>> deck
['four', 'two', 'ace', 'three']

>>> sample([10, 20, 30, 40, 50], k=4)    # Four samples without replacement
[40, 10, 50, 30]
```




归一化的方法

优缺点：

![](/assets/jq-2.1.3-1.png)

preprocessing.MinMaxScaler

![](/assets/jq-2.1.3-2.png)

preprocessing.StandardScaler

preprocessing.robust\_scale

链接:

http://blog.csdn.net/zbc1090549839/article/details/44103801

---

```
sklearn.preprocessing.MinMaxScaler(feature_range=(0, 1), copy=True)


参数:    
feature_range : tuple (min, max), default=(0, 1)
期望的转换数据范围

copy : boolean, optional, default True
设置为False以执行就地行规范化并避免复制（如果输入已经是一个numpy数组）

属性:    
min_ : ndarray, shape (n_features,)
每个功能调整最小

scale_ : ndarray, shape (n_features,)
每个功能相对缩放数据

New in version 0.17: scale_ attribute.

data_min_ : ndarray, shape (n_features,)
每个功能在数据中看到的最小值


data_max_ : ndarray, shape (n_features,)
每个功能在数据中看到的最大值


data_range_ : ndarray, shape (n_features,)
每个功能范围在数据中看到(data_max_ - data_min_)
```

样例:

```
>>> 从 sklearn.preprocessing  进口 MinMaxScaler 
>>> 
>>> 数据 =  [[ - 1 ， 2 ]， [ - 0.5 ， 6 ]， [ 0 ， 10 ]， [ 1 ， 18 ]] 
>>> 缩放器 =  MinMaxScaler （）
>>> 打印（定标器。拟合（数据））
MinMaxScaler（拷贝=真，feature_range =（0，1））
>>> 打印（定标器。data_max_ ）
[1。18.] 
>>> 打印（定标器。变换（数据））
 [[0。0.] 
[0.25 0.25] 
[0.5 0.5] 
[1。1。]] 
>>> 打印（定标器。变换（[[ 2 ， 2 ]]））
 [[1.5 0.]]
```

方法:

```
fit（X [，y]）    计算用于以后缩放的最小值和最大值。
fit_transform（X [，y]）    适合数据，然后转换它。
get_params（[深]）    获取此估算工具的参数。
inverse_transform（X）    根据feature_range撤消X的缩放。
partial_fit（X [，y]）    在线计算X上的最小值和最大值以便以后缩放。
set_params（** PARAMS）    设置此估算器的参数。
transform（X）    根据feature_range缩放X的特征。
```

---

```
sklearn.preprocessing.robust_scale(X, axis=0, with_centering=True, 
                                with_scaling=True, quantile_range=(25.0, 75.0), copy=True)


Parameters:    
X : array-like
要集中和扩展的数据

axis : int (0 by default)
用于计算中位数和IQR的轴。如果为0，则独立缩放每个特征，否则（如果1）缩放每个样本

with_centering : boolean, True by default
如果为True，则在缩放之前将数据居中

with_scaling : boolean, True by default
如果为True，则将数据缩放为单位方差（或等效地，单位标准差).

quantile_range : tuple (q_min, q_max), 0.0 < q_min < q_max < 100.0
默认值：（25.0,75.0）=（第1个分位数，第3个分位数）= IQR用于计算的分位数范围scale_

copy : boolean, optional, default is True
设置为False以执行就地行规范化并避免复制（如果输入已经是numpy数组或scipy.sparse CSR矩阵且轴是1）
```

---

```
sklearn.preprocessing.StandardScaler(copy=True, with_mean=True, with_std=True)


参数:    
copy : boolean, optional, default True
如果为False，请尝试避免复制并改为进行缩放。这并不能保证始终在原地工作; 例如，如果数据不是NumPy数组或
scipy.sparse CSR矩阵，则仍可返回副本

with_mean : boolean, True by default
如果为True，则在缩放之前将数据居中。当在稀疏矩阵上尝试时，这不起作用（并且会引发异常），因为它们的居中
需要构建一个密集矩阵，在常见的情况下，该矩阵可能太大而不适合存储器

with_std : boolean, True by default
如果为True，则将数据缩放为单位方差（或等效地，单位标准差）

属性:    
scale_ : ndarray or None, shape (n_features,)
每个功能相对缩放数据。等于None什么时候 with_std=False

mean_ : ndarray or None, shape (n_features,)
训练集中每个要素的平均值。等于None什么时候with_mean=False

var_ : ndarray or None, shape (n_features,)
训练集中每个要素的方差。用于计算 scale_。等于None什么时候with_std=False

n_samples_seen_ : int or array, shape (n_features,)
估算器为每个要素处理的样本数。如果没有丢失样本，n_samples_seen则将是整数，否则它将是一个数组。将在新
呼叫重置以适应，但在partial_fit呼叫之间递增
```

```
>>> from sklearn.preprocessing import StandardScaler
>>> data = [[0, 0], [0, 0], [1, 1], [1, 1]]
>>> scaler = StandardScaler()
>>> print(scaler.fit(data))
StandardScaler(copy=True, with_mean=True, with_std=True)
>>> print(scaler.mean_)
[0.5 0.5]
>>> print(scaler.transform(data))
[[-1. -1.]
 [-1. -1.]
 [ 1.  1.]
 [ 1.  1.]]
>>> print(scaler.transform([[2, 2]]))
[[3. 3.]]
```

方法

| `fit`（X \[，y\]） | 计算用于以后缩放的mean和std。 |
| :--- | :--- |
| `fit_transform`（X \[，y\]） | 适合数据，然后转换它。 |
| `get_params`（\[深\]） | 获取此估算工具的参数。 |
| `inverse_transform`（X \[，复制\]） | 将数据缩减为原始表示 |
| `partial_fit`（X \[，y\]） | 在线计算X上的mean和std以便以后缩放。 |
| `set_params`（\*\* PARAMS） | 设置此估算器的参数。 |
| `transform`（X \[，y，copy\]） | 通过居中和缩放执行标准化 |

* \_\_init\_\_（copy = True，with\_mean = True，with\_std = True ）
* fit（X，y =无）

计算用于以后缩放的mean和std。

| 参数： | **X**：{array-like，sparse matrix}，shape \[n\_samples，n\_features\]用于计算平均值和标准偏差的数据，用于稍后沿特征轴缩放。**和**忽视 |
| :--- | :--- |


* fit\_transform（X，y =无，\*\* fit\_params ）

适合数据，然后转换它。

使用可选参数fit\_params使变换器适合X和y，并返回X的变换版本。

| 参数： | **X**：numpy数组形状\[n\_samples，n\_features\]训练集。**y**：numpy数组形状\[n\_samples\]目标值。 |
| :--- | :--- |
| 返回： | **X\_new**：numpy形状数组\[n\_samples，n\_features\_new\]变形阵列。 |

* get\_params\(deep=True\)

获取此估算工具的参数。

| 参数： | **deep**：布尔值，可选如果为True，将返回此估计器的参数并包含作为估算器的子对象。 |
| :--- | :--- |
| 返回： | **params**：将字符串映射到任意字符串映射到其值的参数名称。 |

* inverse\_transform（X，copy = None ）

将数据缩减为原始表示

| 参数： | **X**：类似数组，形状\[n\_samples，n\_features\]用于沿要素轴缩放的数据。**copy**：bool，optional（默认值：None）是否复制输入X. |
| :--- | :--- |
| 返回： | **X\_tr**：类似数组，形状\[n\_samples，n\_features\]变形阵列。 |

* partial\_fit（X，y =无）

在线计算X上的mean和std以便以后缩放。所有X都作为单个批次处理。这适用于由于n\_samples数量非常大而无法拟合的情况，或者因为从连续流中读取X.

增量平均值和标准差的算法在Chan，Tony F.，Gene H.Golub和Randall J.LeVeque的公式1.5a，b中给出。“计算样本方差的算法：分析和建议。”美国统计学家37.3（1983）：242-247：

| 参数： | **X**：{array-like，sparse matrix}，shape \[n\_samples，n\_features\]用于计算平均值和标准偏差的数据，用于稍后沿特征轴缩放。**和**忽视 |
| :--- | :--- |


set\_params（\*\* params ）

设置此估算器的参数。

该方法适用于简单估计器以及嵌套对象（例如管道）。后者具有表单的参数，`<component>__<parameter>`以便可以更新嵌套对象的每个组件。

return:self

* transform\(X, y=’deprecated’, copy=None\)\[source\]

通过居中和缩放执行标准化

| 参数： | **X**：类似数组，形状\[n\_samples，n\_features\]用于沿要素轴缩放的数据。**并且**:\(忽略）自版本0.19后不推荐使用：此参数将在0.21中删除。**copy**：bool，optional（默认值：None）是否复制输入X. |
| :--- | :--- |





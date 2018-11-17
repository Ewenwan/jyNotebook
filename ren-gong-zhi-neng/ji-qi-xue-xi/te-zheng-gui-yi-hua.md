# 特征归一化方法

## 线性归一化

优点:  
    适用于数值比较集中的情况

缺点:  
    当有新数据加入时，可能导致max和min的变化，需要重新定义

## 零均值归一化

优点:  
    适用于属性A的最大值和最小值未知  
    简单容易计算  
    能够应用于数值型的数据，并且不受数据量级的影响

缺点:  
    消除了数据具有的实际意义

# 标准化：去均值，方差规模化

Standardization标准化:将特征数据的分布调整成标准正太分布，也叫高斯分布，也就是使得数据的均值维0，方差为1

标准化的过程为两步：去均值的中心化（均值变为0）；方差的规模化（方差变为1）z-score标准化：y=\(x-μ\)/σ  
小数定标标准化y=x/10^j  （j确保max\(\|y\|\)&lt;1）  
对数Logistic模式:y=1/\(1+e^\(-x\)\)

```python
from sklearn import preprocessing
import numpy as np

# 创建一组特征数据，每一行表示一个样本，每一列表示一个特征
x = np.array([
    [2,1,-3],
    [1,3,-1],
    [-1,0,2]
])

# 将每一列特征标准化为标准正太分为，注意，标准化是针对每一列而言
x_scale = preprocessing.scale(x)
x_scale
```

```
array([[ 1.06904497, -0.26726124, -1.13554995],
       [ 0.26726124,  1.33630621, -0.16222142],
       [-1.33630621, -1.06904497,  1.29777137]])
```

```python
# 特征缩放
mu = x.mean(axis=0)
sigma = x.std(axis=0)
x_o = (x-mu)/sigma
x_o
```

```
array([[ 1.06904497, -0.26726124, -1.13554995],
       [ 0.26726124,  1.33630621, -0.16222142],
       [-1.33630621, -1.06904497,  1.29777137]])
```

```python
mu
sigma
```

```
array([1.24721913, 1.24721913, 2.05480467])
```

```python
x_scale == x_o
```

```
array([[ True,  True,  True],
       [ True,  True,  True],
       [ True,  True,  True]])
```

```python
# 标准化后的均值和方差
x_scale_mean = x_scale.mean(axis=0)
x_scale_std = x_scale.std(axis=0)
print(x_scale_mean)
print(x_scale_std)

# axis=0:对列进行操作
# axis=1:对行进行操作
```

```
[ 1.48029737e-16  7.40148683e-17 -7.40148683e-17]
[1. 1. 1.]
```

StandarScaler类,可以在训练数据集上做了标准转换操作之后，把相同的转换应用到测试训练集中

可以对训练数据，测试数据应用相同的转换，以后有新的数据进来也可以直接调用，不用再重新把数据放在一起再计算一次了

```python
# 调用fit方法，根据已有的训练数据创建一个标准化的转换器
scaler = preprocessing.StandardScaler().fit(x)
scaler
```

```
E:\Anaconda3\lib\site-packages\sklearn\utils\validation.py:475: DataConversionWarning: Data with input dtype int32 was converted to float64 by StandardScaler.
  warnings.warn(msg, DataConversionWarning)





StandardScaler(copy=True, with_mean=True, with_std=True)
```

```python
# 训练数据x，调用transformfangfa
scaler.transform(x)
```

```
E:\Anaconda3\lib\site-packages\sklearn\utils\validation.py:475: DataConversionWarning: Data with input dtype int32 was converted to float64 by StandardScaler.
  warnings.warn(msg, DataConversionWarning)





array([[ 1.06904497, -0.26726124, -1.13554995],
       [ 0.26726124,  1.33630621, -0.16222142],
       [-1.33630621, -1.06904497,  1.29777137]])
```

```python
# 训练新数据
new_x = [
    [-1,2,-0]
]

scaler.transform(new_x)
```

```
array([[-1.33630621,  0.53452248,  0.32444284]])
```

StandardScaler\(\)中可以传入两个参数：with\_mean,with\_std.这两个都是布尔型的参数，默认情况下都是true,但也可以自定义成false.即不要均值中心化或者不要方差规模化为1

# 归一化

也就是使得特征的分布是在一个给定最小值和最大值的范围内的。一般情况下是在\[0,1\]之间，或者是特征中绝对值最大的那个数为1，其他数以此维标准分布在\[\[-1，1\]之间

## MinMaxScaler

数据规与\[0,1\]之间

公式:

x\_scaled = \(x-x.min\) / \(x.max-x.min\)

```python
min_max_scaler = preprocessing.MinMaxScaler()
x_minmax = min_max_scaler.fit_transform(x)
x_minmax
```

```
E:\Anaconda3\lib\site-packages\sklearn\utils\validation.py:475: DataConversionWarning: Data with input dtype int32 was converted to float64 by MinMaxScaler.
  warnings.warn(msg, DataConversionWarning)





array([[1.        , 0.33333333, 0.        ],
       [0.66666667, 1.        , 0.4       ],
       [0.        , 0.        , 1.        ]])
```

```python
x_scaled = (x-x.min(axis=0)) / (x.max(axis=0)-x.min(axis=0)) 
print(x_scaled)
```

```
[[1.         0.33333333 0.        ]
 [0.66666667 1.         0.4       ]
 [0.         0.         1.        ]]
```

```python
x_test = np.array([
    [-1,2,-0]
])
x_test_minmax = min_max_scaler.transform(x_test)
x_test_minmax
```

```
array([[0.        , 0.66666667, 0.6       ]])
```

## MaxAbsScaler

数据会被规模化到\[-1,1\]之间

```python
max_abs_scaler = preprocessing.MaxAbsScaler()
x_train_maxabs = max_abs_scaler.fit_transform(x)
x_train_maxabs
```

```
array([[ 1.        ,  0.33333333, -1.        ],
       [ 0.5       ,  1.        , -0.33333333],
       [-0.5       ,  0.        ,  0.66666667]])
```

```python
x_test = np.array([
    [-1,2,-0]
])
x_train_maxabs = max_abs_scaler.transform(x_test)
x_train_maxabs
```

```
array([[-0.5       ,  0.66666667,  0.        ]])
```

# 规模化有异常值的数据

# 正则化Normalization

正则化是将样本在向量空间模型上的一个转换，经常被使用在分类与聚类中

```python
x_normalized1 = preprocessing.normalize(x,norm='l1')
x_normalized2 = preprocessing.normalize(x,norm='l2')
print(x)
print(x_normalized1)
print(x_normalized2)

x_normalized = x_normalized2
```

```
[[ 2  1 -3]
 [ 1  3 -1]
 [-1  0  2]]
[[ 0.33333333  0.16666667 -0.5       ]
 [ 0.2         0.6        -0.2       ]
 [-0.33333333  0.          0.66666667]]
[[ 0.53452248  0.26726124 -0.80178373]
 [ 0.30151134  0.90453403 -0.30151134]
 [-0.4472136   0.          0.89442719]]
```

```python
# 训练
normlizer = preprocessing.Normalizer().fit(x)
normlizer
```

```
Normalizer(copy=True, norm='l2')
```

```python
# 对数据进行正则化
normlizer.transform(x)
```

```
array([[ 0.53452248,  0.26726124, -0.80178373],
       [ 0.30151134,  0.90453403, -0.30151134],
       [-0.4472136 ,  0.        ,  0.89442719]])
```

```python
# 新数据训练
new_x = [
    [1,-1,2]
]
normlizer.transform(new_x)
```

```
array([[ 0.40824829, -0.40824829,  0.81649658]])
```

## 二值化-特征值得二值化

特征的二值化是指将数值型的特征数据转换成布尔类型的值。可以使用实用类Binarizer

```python
# 创建一组特征数据，每一行表示一个样本，每一列表示一个特征

binarizer = preprocessing.Binarizer().fit(x)
binarizer.transform(x)
```

```
array([[1, 1, 0],
       [1, 1, 0],
       [0, 0, 1]])
```

默认是根据0来二值化的，大于0的都标记为1，小于等于0的都标记为0

可以设置这个阀值，只需传出参数threshold

```python
binarizer = preprocessing.Binarizer(threshold=-0.5)
binarizer.transform(x)
```

```
array([[1, 1, 0],
       [1, 1, 0],
       [0, 1, 1]])
```

# 类别特征编码

要想使得类别型的变量能最终被模型直接使用，可以使用one-of-k编码或者one-hot编码。这些都可以通过OneHotEncoder实现，它可以将有n种值的一个特征变成n个二元的特征

# enc = preprocessing.OneHotEncoder\(\)

enc.fit\(\[\[0, 0, 3\], \[1, 1, 0\], \[0, 2, 1\], \[1, 0, 2\]\]\)  
enc.transform\(\[\[1,1,3\]\]\).toarray\(\)

```python
# 某些特征中可能对一些值有缺失
# 可以向OneHotEncoder传如参数n_values，用来指明每个特征中的值的总个数

enc = preprocessing.OneHotEncoder(n_values=[4,5,6])
enc.fit([
    [0, 0, 3],
    [1, 1, 0], 
    [0, 2, 5]
])
enc.transform([[1,1,5]]).toarray()
```

```
array([[0., 1., 0., 0., 0., 1., 0., 0., 0., 0., 0., 0., 0., 0., 1.]])
```

# 弥补缺失数据

```python
from sklearn.preprocessing import Imputer

imp = Imputer(missing_values="NaN",strategy="mean",axis=0)
x = [
    [1,6,3],
    [np.nan,3,4],
    [7,8,3]
]
imp.fit(x)

x_test = [[np.nan, 2,1], [6, np.nan,3], [7, 6,6]]
imp.transform(x_test)
```

```
array([[4.        , 2.        , 1.        ],
       [6.        , 5.66666667, 3.        ],
       [7.        , 6.        , 6.        ]])
```

# 创建多项式特征

```python
import numpy as np
from sklearn.preprocessing import PolynomialFeatures

# 自建一组3*2的样本
x = np.arange(6).reshape(3, 2)

# 创建2次方的多项式
# poly = PolynomialFeatures(2,interaction_only=True)
poly = PolynomialFeatures(2)

poly.fit_transform(x)
```

```
array([[ 1.,  0.,  1.,  0.,  0.,  1.],
       [ 1.,  2.,  3.,  4.,  6.,  9.],
       [ 1.,  4.,  5., 16., 20., 25.]])
```

# 自定义特征的转换函数

## FunctionTransformer

```python
# 将特征数据做log转换

from sklearn.preprocessing import FunctionTransformer
import numpy as np

transformer = FunctionTransformer(np.log1p)
x= np.array([
    [0.,1],
    [np.e-1,3]
])
transformer.transform(x)
```

```
array([[0.        , 0.69314718],
       [1.        , 1.38629436]])
```

首先要明确有多少特征，哪些是连续的，哪些是类别的。

检查有没有缺失值，对确实的特征选择恰当方式进行弥补，使数据完整。

对连续的数值型特征进行标准化，使得均值为0，方差为1。

对类别型的特征进行one-hot编码。

将需要转换成类别型数据的连续型数据进行二值化。

为防止过拟合或者其他原因，选择是否要将数据进行正则化。

在对数据进行初探之后发现效果不佳，可以尝试使用多项式方法，寻找非线性的关系。

根据实际问题分析是否需要对特征进行相应的函数转换


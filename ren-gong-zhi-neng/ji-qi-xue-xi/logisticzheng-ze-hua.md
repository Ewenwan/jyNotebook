### 机器学习中防止过拟合的处理方法

* 参考答案[https://blog.csdn.net/heyongluoyao8/article/details/49429629](https://blog.csdn.net/heyongluoyao8/article/details/49429629)

* （1）什么是过拟合（over-fitting）:

  * 过拟合表现于模型的泛化能力弱。训练集上效果好；在测试集上效果差。

* （2）过拟合影响：拟合模型是用来预测未知的结果，过拟合会导致预测结果不准确无法达到预定的目标。

* （3）防止过拟合的方式：

  * a.增大训练样本，使模型接触更多样化的数据来调增本身以达到更好的结果
  * b.正则化方法：在进行目标函数或代价函数优化时，在目标函数或代价函数后面加上一个正则项
    *     L1正则：L1正则是基于L1范数，即在目标函数后面加上参数的L1范数和项（即参数绝对值和与参数的积项）
      * 目的：为了使得部分参数为零，减少参数，从而降低模型的复杂度，防止过拟合，提高模型的泛化能力
    * L2正则:L2正则是基于L2范数，即在目标函数后面加上参数的L2范数和项（参数的平方和与参数的积项）
      * 目的：为了使参数值更小，降低模型的复杂度，防止过拟合，提高模型的泛化能力
  * c.    Dropout：是通过修改神经网络本身来实现的，它是在训练网络时用的一种技巧。

使用逻辑回归\(Logistic Regression\)对鸢尾花数据（多分类问题）进行预测，可以直接使用sklearn中的LR方法，并尝试使用不同的参数，包括正则化的方法，正则项系数，求解优化器，以及将二分类模型转化为多分类模型的方法。

```
import numpy as np
import pandas as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report

# 获取鸢尾花数据的方法：
X,y = load_iris(return_X_y=True)
```

```
lr = LogisticRegression()
lr.fit(X,y)
lr_pre = lr.predict(X)
lr.score(X,y)
```

0.96

```
print(classification_report(y,lr_pre))
```

```
         precision    recall  f1-score   support

      0       1.00      1.00      1.00        50

      1       0.98      0.90      0.94        50

      2       0.91      0.98      0.94        50
```

avg / total       0.96      0.96      0.96       150

```
y = g(z)=g(h(θ)) = 1/(+e^(-z)) sigmoid函数
```

```
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号

def sigmoid(z):
    return 1.0/(1.0+np.exp(-z))

x = np.arange(-10,10,0.1)
h = sigmoid(x)
plt.plot(x,h)
plt.axvline(0.0,color='k')
plt.axhline(y=0.5,ls='dotted',color='k')
plt.yticks([0.0,0.5,1.0])
plt.title(r"Sigmoid函数曲线",fontsize=15)
plt.text(5,0.8,r'$y=\frac{1}{1+e^{z}}$',fontsize=18)
```

![](/assets/jq-2.1.4-6.png)

```
from sklearn.model_selection import train_test_split
from sklearn.datasets import load_iris

X,y = load_iris(return_X_y=True)


x_train,x_test,y_train,y_test = train_test_split(X,y,test_size=0.35,random_state=0)
# x_train.shape,y_train.shape,x_test.shape,y_test.shape
```

```
# 画出训练数据点
import plotly.graph_objs as go
from plotly.offline import init_notebook_mode, iplot
init_notebook_mode(connected = True)
trace = go.Scatter(x = X[:,0], y = X[:,1], mode = 'markers', 
                    marker = dict(color = np.random.randn(150),size = 10, colorscale='Viridis',showscale=False))
layout = go.Layout(title = '训练点', xaxis=dict(title='花萼长度 Sepal length', showgrid=False),
                    yaxis=dict(title='花萼宽度 Sepal width',showgrid=False),
                    width = 700, height = 380)
fig = go.Figure(data=[trace], layout=layout)

iplot(fig)
```

![](/assets/jq-2.1.4-7.png)

```
X1 = [i[0] for i in X]
Y1 = [i[1] for i in X]
plt.scatter(X1,Y1,color='red',marker='o',label='setosa')
plt.legend()
```

![](/assets/jq-2.1.4-8.png)

```
from sklearn.linear_model import LogisticRegression

lr = LogisticRegression(penalty='l2',solver='newton-cg',multi_class='multinomial')
lr.fit(x_train,y_train)


print("训练集准确率:{}".format(lr.score(x_train,y_train)))
print("测试集准确率:{}".format(lr.score(x_test,y_test)))
```

训练集准确率:0.979381443298969

测试集准确率:0.9811320754716981

```
# 分类器正确率分析
from sklearn import metrics
pre = lr.predict(x_test)
accuracy = metrics.accuracy_score(y_test,pre)
print("模型准确率:{}".format(accuracy))
```

模型准确率:0.9811320754716981

```
print(metrics.classification_report(y_test,pre))
```

```
         precision    recall  f1-score   support

      0       1.00      1.00      1.00        16

      1       1.00      0.95      0.98        21

      2       0.94      1.00      0.97        16
```

avg / total       0.98      0.98      0.98        53

```
x1_min, x1_max = X[:, 0].min()-0.5, X[:, 0].max()+0.5  # 第0列的范围
x2_min, x2_max = X[:, 1].min()-0.5, X[:, 1].max()+0.5  # 第1列的范围
x1,y1 = np.meshgrid(np.arange(x1_min,x1_max,0.2),np.arange(x2_min,x2_max,0.2))

#pcolormesh函数将xx,yy两个网格矩阵和对应的预测结果Z绘制在图片上
# np.c_:获取矩阵
# np.ravel():调用ravel()函数将x和y的两个矩阵转变成一维数组
z = lr.predict(np.c_[x1.ravel(),y1.ravel()])
z = z.reshape(x1.shape)
plt.figure(1,figsize=(10,6))
# 调用pcolormesh()函数将xx、yy两个网格矩阵和对应的预测结果Z绘制在图片上
# cmap=plt.cm.Paired表示绘图样式选择Paired主题
plt.pcolormesh(x1,y1,z,cmap=plt.cm.Paired)

plt.scatter(X1,Y1,color="blue",marker='x')
plt.xlim(x1.min(),x1.max())
plt.ylim(y1.min(),y1.max())
plt.xticks()
plt.yticks()
```

![](/assets/jq-2.1.4-9.png)

```
import numpy as np

def sigmoid(z):
    return 1.0/(1.0+np.exp(-z))

def costReg(theta,X,y,learningRate):
    theta = np.matrix(theta)
    X = np.matrix(X)
    y = np.matrix(y)
    first = np.multiply(-y,np.log(sigmoid(X*theta.T)))
    second = np.multiply((1-y),np.log(1-sigmoid(X*theta.T)))
    reg = learningRate / (2*len(X))*np.sum(np.power(theta[:,1:theta.shape[1]],2))
    return np.sum(first-second) / len(X)+reg

theta = np.ones((X.shape[0],X.shape[1]))
learningRate = 0.1
costReg(theta,X,y,learningRate)
```

0.15276123962660298




```
# 直方图
x = np.random.rand(100)
plt.hist(x,30)
plt.show()
```

![](/assets/k-m-3.3.4-1.png)

```
# 标题、标签、图例

#coding:utf-8
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
#有中文出现的情况，需要u'内容'

x = np.linspace(0,2*np.pi,50)

plt.plot(x,np.sin(x),'r-x',label="sin(x)")
plt.plot(x,np.cos(x),'g-^',label="cos(x)")
plt.legend()

# x标签
plt.xlabel("Rads测试")
# y标签
plt.ylabel("Amplitude")
# 标题
plt.title("Sin and Cos")
plt.show()
```

![](/assets/k-m-3.3.4-2.png)

```
# 折线图
x = np.linspace(0,10,10,dtype=int)
y = np.linspace(0,10,10,dtype=int)
plt.plot(x,y)
plt.show()
```

![](/assets/k-m-3.3.4-3.png)

```
# 盒图
fig = plt.figure()
ax = plt.subplot()
# 设置最大值不超过95分位点；最小值不小于5%分位点
ax.boxplot([range(5),range(10)],whis=[5,95])
plt.show()
```

![](/assets/k-m3.3.4-3.png)

```
# 热度图
import seaborn as sns
import pandas as pd
y = np.random.randint(1,100,40)
y = y.reshape((5,8))
df = pd.DataFrame(y,columns=[x for x in 'abcdefgh'])
sns.heatmap(df,annot=True)
plt.show()
```

![](/assets/k-m3.3.4-6.png)

```
# 颜色表
dir(plt.cm)
```

```
# 中文
#coding:utf-8
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
#有中文出现的情况，需要u'内容'
```




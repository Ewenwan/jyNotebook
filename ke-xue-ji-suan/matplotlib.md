```
import matplotlib.pyplot as plt
import numpy as np
```

```
# 简单的绘图
x = np.linspace(0,2*np.pi,50)
# 如果没有第一个参数，则x坐标默认为数组的索引
plt.plot(x,np.sin(x))
plt.show()
```

![](/assets/k-m-3.3.3-1.png)

```
x = np.linspace(0,2*np.pi,50)
plt.plot(
    x,np.sin(x),
    x,np.sin(2*x)
)
plt.show()
```

![](/assets/k-m-3.3.3-2.png)

```
# 自定义图形外观
x = np.linspace(0,2*np.pi,50)
plt.plot(
    x,np.sin(x),'b-.',
    x,np.cos(x),'g--'
)
plt.show()
```

![](/assets/k-m-3.3.3-3.png)

蓝色 - 'b' 绿色 - 'g' 红色 - 'r' 青色 - 'c' 品红 - 'm' 黄色 - 'y' 黑色 - 'k' （'b'代表蓝色，所以这里用黑色的最后一个字母） 白色 - 'w' 线： 直线 - '-' 虚线 - '--' 点线 - ':' 点划线 - '-.' 常用点标记 点 - '.' 像素 - ',' 圆 - 'o' 方形 - 's' 三角形 - '^'

In \[9\]:

```
# 使用子图
x = np.linspace(0,2*np.pi,50)
plt.subplot(2,1,1)
plt.plot(x,np.sin(x),'r')
plt.subplot(2,1,2)
plt.plot(x,np.cos(x),'g')
plt.show()


# subplot(parm1,parm2,parm3):
# parm1:代表子图的总行数
# param2:代表子图的总列数
# param3:代表活跃区域
```

![](/assets/k-m-3.3.3-4.png)

```
# 散点图
x = np.linspace(0,2*np.pi,50)
y = np.sin(x)
plt.scatter(x,y)
plt.show()
```

![](/assets/k-m-3.3.3-5.png)

```
#彩色映射散点图
x = np.random.rand(1000)
y = np.random.rand(1000)
size = np.random.rand(1000)*50
colour = np.random.rand(1000)
plt.scatter(x,y,size,colour)
# 颜色表
plt.colorbar()
plt.show()




import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

N = 100
genders= ['Female', 'Male']
df = pd.DataFrame({
    'Height': np.random.uniform(low=130, high=200, size=N),
    'Weight': np.random.uniform(low=40, high=100, size=N),
    'Gender': np.random.choice(genders, size=N)
})

fg = sns.FacetGrid(data=df, hue='Gender', hue_order=genders)
fg.map(plt.scatter, 'Weight', 'Height').add_legend()
plt.show()
```

![](/assets/k-m-3.3.3-6.png)

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




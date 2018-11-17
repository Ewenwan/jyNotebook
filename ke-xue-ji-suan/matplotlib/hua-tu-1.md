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
```

![](/assets/k-m-3.3.3-6.png)


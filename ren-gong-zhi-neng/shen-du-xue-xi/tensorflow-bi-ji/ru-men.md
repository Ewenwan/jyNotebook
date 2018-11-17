了解和运行 TensorFlow!

使用 Python API 撰写的 TensorFlow 示例代码:生成一些三维数据, 然后用一个平面拟合数据.

```
#!/usr/bin/env python
# coding: utf-8

# In[1]:


import tensorflow as tf
import numpy as np

# 使用Nummpy生成假数据(phony data),共100个点
x_data = np.float32(np.random.rand(2,100)) # 随机输入
y_data = np.dot([0.100,0.200],x_data) + 0.300


# In[2]:


x_data


# In[3]:


y_data


# In[4]:


# 构造一个线性模型

b = tf.Variable(tf.zeros([1]))
W = tf.Variable(tf.random_uniform([1,2],-1.0,1.0))
y = tf.matmul(W,x_data) + b


# In[5]:


b


# In[6]:


W


# In[7]:


y


# In[9]:


# 最小化方差

loss = tf.reduce_mean(tf.square(y-y_data))
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(loss)


# In[8]:


# 初始化变量
init = tf.global_variables_initializer()


# In[10]:


# 启动图(graph)
sess = tf.Session()
sess.run(init)


# In[13]:


# 拟合平面
for step in range(0,201):
    sess.run(train)
    if step % 20 ==0:
        print(step,sess.run(W),sess.run(b))


# In[ ]:





```

为了进一步激发你的学习欲望, 我们想让你先看一下 TensorFlow 是如何解决一个经典的机器 学习问题的. 在神经网络领域, 最为经典的问题莫过于 MNIST 手写数字分类问题. 我们准备了 两篇不同的教程, 分别面向机器学习领域的初学者和专家. 如果你已经使用其它软件训练过许多 MNIST 模型, 请阅读高级教程 \(红色药丸链接\). 如果你以前从未听说过 MNIST, 请阅读初级教程 \(蓝色药丸链接\). 如果你的水平介于这两类人之间, 我们建议你先快速浏览初级教程, 然后再阅读高级教程.

[![](http://www.tensorfly.cn/tfdoc/images/blue_pill.png "面向机器学习初学者的 MNIST 初级教程")](http://www.tensorfly.cn/tfdoc/tutorials/mnist_beginners.html)

[![](http://www.tensorfly.cn/tfdoc/images/red_pill.png "面向机器学习专家的 MNIST 高级教程")](http://www.tensorfly.cn/tfdoc/tutorials/mnist_pros.html)

图片由 CC BY-SA 4.0 授权; 原作者 W. Carter


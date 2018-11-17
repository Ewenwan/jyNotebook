> 什么是Jupyter?

```
Jupyter Notebook（此前被称为IPython notebook）是一个交互式笔记本，支持运行40 多种编程语言。 
Jupyter Notebook 的本质是一个Web 应用程序，便于创建和共享文学化程序文档，支持实时代码，数学方程，可视化和markdown
```

### 安装Jupyter

```
python3 -m pip install --upgrade pip
python3 -m pip install jupyter
```

或者直接

```
pip install jupyter
```

### 运行

安装完成后，运行Jupyter notebook，在命令框下，输入如下命令即可:

```
jupyter notebook
```

在浏览器中输入 localhost:8888 会出现如下界面

![](/assets/1.2.3.1-1.png)

> 温馨提示:
>
> jupyrt notebook 应该需要创建一个文件夹，然后在当前文件夹目录下运行命令

### jupyter notebook常用命令

* #### 帮助

```
jupyter notebook --help 或者 jupyter notebook -h
```

* #### 启动

##### 默认端口启动

```
jupyter notebook
```

> 之后在Jupyter Notebook的所有操作，都请保持终端不要关闭，因为一旦关闭终端，就会断开与本地服务器的链接，将无法在Jupyter Notebook中进行其他操作

#### **指定端口启动**

```
jupyter notebook --port <port_number>

例如:jupyter notebook --port 8889
```

#### 启动服务器但不打开浏览器

```
jupyter-notebook --no-browser
```

#### 以root身份启动

```
jupyter notebook --ip=127.0.0.1 --port 8000 --allow-root
```

#### 生成jupyter的配置文件

```
jupyter notebook --generate-config
```

#### 修改jupyter的配置文件

```
vim ~/.jupyter/jupyter_notebook_config.py
```

将293行 \#c.NotebookApp.token = '&lt;generated&gt;'修改为c.NotebookApp.token = 'password'，则密码就改为password

#### 修改密码

```
启动jupyter后，新建一个python

输入第一行
from notebook.auth import passwd
alt + enter 来执行这个命令并进入下一行；在下一行里面输入：
passwd()
```

### Markdown用法

![](/assets/jy-4.1.4.1-2.png)

### 常用魔法函数

![](/assets/jy-4.1.4.1-3.png)


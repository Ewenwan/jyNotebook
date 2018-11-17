### 在Windows下安装Python

安装python有两种方式:

* 一种通过Python安装包安装
* 另一种通过anaconda安装

---

接下来介绍如何安装两种方式的安装方法:

#### Python安装包安装

* 官方网站:[https://www.python.org/](https://www.python.org/)

首先进入官网

![](/assets/1.2.1.1-1.png)

然后点击Downloads &gt; Windows,会出现如何界面

![](/assets/1.2.1.1-2.png)然后点击 [Latest Python 3 Release - Python 3.7.0](https://www.python.org/downloads/release/python-370/)，往下滑动，出现以下界面

![](/assets/1.2.1.1-3.png)这里有很多版本的，在windows中安装可以选择[Windows x86-64 executable installer](https://www.python.org/ftp/python/3.7.0/python-3.7.0-amd64.exe)和[Windows x86 executable installer](https://www.python.org/ftp/python/3.7.0/python-3.7.0.exe) 分别是对应64位的windows和32位的windows，选择适合的版本进行下载，下载完后，双击安装python.exe,出现以下界面

![](/assets/1.2.1.1-4.png)

第一个是默认安装，第二个是用户自定义安装，最下方的复选框，勾选后，表示python路径自动添加到环境变量中

本文选择用户自定义安装

![](/assets/1.2.1.1-5.png)

![](/assets/1.2.1.1-6.png)然后点击安装，安装完后，出现successful，就表示安装成功了

现在测试，是否安装成功了，按下win+r,并输入cmd，进入控制平台，在命令框下输入python

![](/assets/1.2.1.1-8.png)

出现以上类似内容，就证明安装成功了

如果出现以下提示

![](/assets/1.2.1.1-10.png)

代表环境路径，没有配置好，需要将python.exe所在的python路径添加到环境变量中，

![](/assets/1.2.1.1-11.png)

首先右键点击此电脑，选中属性，出现如下界面

![](/assets/1.2.1.1-12.png)

选中高级系统设置，然后可以看到有环境变量的选项，点击进去，出现如下视图

![](/assets/1.2.1.1-13.png)

选中系统变量下的Path选项，然后，点击编辑，然后找到python.exe的所在路径

![](/assets/1.2.1.1-14.png)

粘贴复制到刚才编辑变量处，点击新建

![](/assets/1.1.2.1-15.png)

然后点击确定，就可以了

有可能自己的电脑下装了很多不同版本的python，为了区别开来，可以在python目录，将python.exe，复制粘贴并命名为新的名字，作为原来的python.exe的代替

![](/assets/1.2.1.1-7.png)

测试一下，在命令框中输入python36

![](/assets/1.2.1.1-9.png)

另外还需要将python下的Scripts目录添加到环境变量中

![](/assets/1.2.1.1-17.png)

### Anaconda安装

* 官方网站:https://www.anaconda.com/download/

首先进入官网

![](/assets/1.2.1.1-16.png)

电脑是64位的，安装[64-Bit Graphical Installer \(631 MB\)](https://repo.anaconda.com/archive/Anaconda3-5.2.0-Windows-x86_64.exe)

电脑是32位的，安装[32-Bit Graphical Installer \(506 MB\)](https://repo.anaconda.com/archive/Anaconda3-5.2.0-Windows-x86.exe)

---

> 温馨提示
>
> 建议使用anaconda






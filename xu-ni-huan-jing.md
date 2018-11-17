> 首先来讲下为什么要安装搭建虚拟环境?

* 搭建独立的python运行环境，防止与其他版本的python产生冲突

* 有助于包管理和避免版本的冲突

* 卸载方便

> 接下来开始安装虚拟环境

### 安装virtualenv

```
pip install virtualenv
```

### 创建项目文件

```
# 创建文件
F:\py_virtualenv>mkdir app

# 切换目录
F:\py_virtualenv>cd app

F:\py_virtualenv\app>
```

### 指定版本创建

```
mkvirtualenv --python=D:\py\python2.7\python.exe app
```

### 安装虚拟环境

在自定义的目录下安装虚拟环境，输入 virtualenv 虚拟环境名

```
F:\py_virtualenv\app>virtualenv django
Using base prefix 'e:\\anaconda3'
New python executable in F:\py_virtualenv\app\django\Scripts\python.exe
Installing setuptools, pip, wheel...done.
```

会在当前目录创建一个django 文件，切换到当前目录下Scripts

```
F:\py_virtualenv\app>cd django

F:\py_virtualenv\app\django>cd Scripts

F:\py_virtualenv\app\django\Scripts>
```

![](/assets/1.2.1.4-4.png)

### 启动虚拟环境

输入如下命令进行启动

```
activate
```

如:

```
F:\py_virtualenv\app\django\Scripts>activate

(django) F:\py_virtualenv\app\django\Scripts>
```

在前面会出现，自定义的虚拟环境的名字

### 退出虚拟环境

输入如下命令

```
deactivate
```

如:

```
(django) F:\py_virtualenv\app\django\Scripts>deactivate
F:\py_virtualenv\app\django\Scripts>
```

---

### 安装virtualenvwrapper

为了更方便使用virtualenv，借助 virtualenvwrapper 来安装虚拟环境

##### 定义默认的安装路径

通过 计算机 &gt; 属性 &gt; 高级系统设置 &gt; 环境变量

然后在系统变量中新建"变量名":WORKON\_HOME，变量值:"自定义的路径"

##### ![](/assets/1.2.1.4-1.png)

##### 创建环境变量命令:

```
mkvirtualenv venv
```

如:

```
C:\Users\tokimeki>mkvirtualenv venv
Using base prefix 'e:\\anaconda3'
New python executable in F:\py_virtualenv\venv\Scripts\python.exe
Installing setuptools, pip, wheel...done.
```

##### 列出所有虚拟环境命令:

```
lsvirtualenv
```

如:

```
(venv) C:\Users\tokimeki>lsvirtualenv

dir /b /ad "F:\py_virtualenv"
==============================================================================
app
venv
```

##### 激活虚拟环境命令:

```
workon venv
```

如:

```
C:\Users\tokimeki>workon venv
(venv) C:\Users\tokimeki>
```

##### 进入虚拟环境目录命令:

```
cdsitepackages
```

如:

```
(venv) C:\Users\tokimeki>cdsitepackages
(venv) F:\py_virtualenv\venv\Lib\site-packages>
```

##### 列出site-packages目录的所有软件包 命令

```
lssitepackages
```

如:

```
(venv) F:\py_virtualenv\venv\Lib\site-packages>lssitepackages

dir /b "F:\py_virtualenv\venv\Lib\site-packages"
==============================================================================
easy_install.py
pip
pip-18.0.dist-info
pkg_resources
setuptools
setuptools-40.4.2.dist-info
wheel
wheel-0.31.1.dist-info
__pycache__
```

##### 退出虚拟环境命令:

```
deactivate
```

如:

```
(venv) F:\py_virtualenv\venv\Lib\site-packages>deactivate

F:\py_virtualenv\venv\Lib\site-packages>
```

##### 删除虚拟环境命令:

```
rmvirtualenv 虚拟环境名字
```

如:

```
F:\py_virtualenv\venv\Lib\site-packages>rmvirtualenv app

    Deleted F:\py_virtualenv\app
```

---

### 重建Python环境

#### 冻结环境

所谓 冻结\(freeze\) 环境，就是将当前环境的软件包等固定下来:

```
# 安装包列表保存到文件packages.txt中
pip freeze > requirements.txt
```

#### 重建环境

重建\(rebuild\) 环境就是在部署的时候，在生产环境安装好对应版本的软件包，不要出现版本兼容等问题:

```
pip install -r requirements.txt
```




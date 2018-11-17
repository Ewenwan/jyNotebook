# 下载与安装 {#下载与安装-}

你可以使用我们提供的二进制包, 或者使用源代码, 安装 TensorFlow.

## 二进制安装 {#二进制安装-}

TensorFlow Python API 依赖 Python 2.7 版本.

在 Linux 和 Mac 下最简单的安装方式, 是使用[pip](https://pypi.python.org/pypi/pip)安装.

如果在安装过程中遇到错误, 请查阅[常见问题](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html#common_install_problems). 为了简化安装步骤, 建议使用 virtualenv, 教程见[这里](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html#virtualenv_install).

### Ubuntu/Linux {#ubuntulinux-}

```
# 仅使用 CPU 的版本
$ pip install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.5.0-cp27-none-linux_x86_64.whl

# 开启 GPU 支持的版本 (安装该版本的前提是已经安装了 CUDA sdk)
$ pip install https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.5.0-cp27-none-linux_x86_64.whl
```

### Mac OS X {#mac-os-x-}

在 OS X 系统上, 我们推荐先安装[homebrew](http://brew.sh/), 然后执行`brew install python`, 以便能够使用 homebrew 中的 Python 安装 TensorFlow. 另外一种推荐的方式是在[virtualenv](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html#virtualenv_install)中安装 TensorFlow.

```
# 当前版本只支持 CPU
$ pip install https://storage.googleapis.com/tensorflow/mac/tensorflow-0.5.0-py2-none-any.whl
```

## 基于 Docker 的安装 {#基于-docker-的安装-}

我们也支持通过[Docker](http://docker.com/)运行 TensorFlow. 该方式的优点是不用操心软件依赖问题.

首先,[安装 Docker](http://docs.docker.com/engine/installation/). 一旦 Docker 已经启动运行, 可以通过命令启动一个容器:

```
$ docker run -it b.gcr.io/tensorflow/tensorflow

```

该命令将启动一个已经安装好 TensorFlow 及相关依赖的容器.

### 其它镜像 {#其它镜像-}

默认的 Docker 镜像只包含启动和运行 TensorFlow 所需依赖库的一个最小集. 我们额外提供了 下面的容器, 该容器同样可以通过上述`docker run`命令安装:

* `b.gcr.io/tensorflow/tensorflow-full`
  : 镜像中的 TensorFlow 是从源代码完整安装的, 包含了编译和运行 TensorFlow 所需的全部工具. 在该镜像上, 可以直接使用源代码进行实验, 而不需要再安装上述的任何依赖.

## 基于 VirtualEnv 的安装 {#基于-virtualenv-的安装-}

我们推荐使用[virtualenv](https://pypi.python.org/pypi/virtualenv)创建一个隔离的容器, 来安装 TensorFlow. 这是可选的, 但是这样做能使排查安装问题变得更容易.

首先, 安装所有必备工具:

```
# 在 Linux 上:

$ sudo apt-get install python-pip python-dev python-virtualenv


# 在 Mac 上:

$ sudo easy_install pip  
# 如果还没有安装 pip

$ sudo pip install --upgrade virtualenv

```

接下来, 建立一个全新的 virtualenv 环境. 为了将环境建在`~/tensorflow`目录下, 执行:

```
$ virtualenv --system-site-packages ~/tensorflow
$ cd ~/tensorflow
```

然后, 激活 virtualenv:

```
$ source bin/activate  # 如果使用 bash
$ source bin/activate.csh  # 如果使用 csh
(tensorflow)$  # 终端提示符应该发生变化
```

在 virtualenv 内, 安装 TensorFlow:

```
(tensorflow)$ pip install --upgrade <$url_to_binary.whl>
```

接下来, 使用类似命令运行 TensorFlow 程序:

```
(tensorflow)$ cd tensorflow/models/image/mnist
(tensorflow)$ python convolutional.py

# 当使用完 TensorFlow
(tensorflow)$ deactivate  # 停用 virtualenv

$  # 你的命令提示符会恢复原样
```

## 尝试你的第一个 TensorFlow 程序 {#尝试你的第一个-tensorflow-程序-}

### \(可选\) 启用 GPU 支持 {#可选-启用-gpu-支持-}

如果你使用 pip 二进制包安装了开启 GPU 支持的 TensorFlow, 你必须确保 系统里安装了正确的 CUDA sdk 和 CUDNN 版本. 请参间[CUDA 安装教程](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html#install_cuda)

你还需要设置`LD_LIBRARY_PATH`和`CUDA_HOME`环境变量. 可以考虑将下面的命令 添加到`~/.bash_profile`文件中, 这样每次登陆后自动生效. 注意, 下面的命令 假定 CUDA 安装目录为`/usr/local/cuda`:

```
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64"
export CUDA_HOME=/usr/local/cuda
```

### 运行 TensorFlow {#运行-tensorflow-}

打开一个 python 终端:

```
$ python

>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print sess.run(hello)
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print sess.run(a+b)
42
>>>
```

## 从源码安装 {#从源码安装-}

### 克隆 TensorFlow 仓库 {#克隆-tensorflow-仓库-}

```
$ git clone --recurse-submodules https://github.com/tensorflow/tensorflow
```

`--recurse-submodules`参数是必须得, 用于获取 TesorFlow 依赖的 protobuf 库.

### Linux 安装 {#linux-安装-}

#### 安装 Bazel {#安装-bazel-}

首先依照[教程](http://bazel.io/docs/install.html)安装 Bazel 的依赖. 然后使用下列命令下载和编译 Bazel 的源码:

```
$ git clone https://github.com/bazelbuild/bazel.git
$ cd bazel
$ git checkout tags/0.1.0
$ ./compile.sh
```

上面命令中拉取的代码标签为`0.1.0`, 兼容 Tensorflow 目前版本. bazel 的`HEAD`版本 \(即最新版本\) 在这里可能不稳定.

将执行路径`output/bazel`添加到`$PATH`环境变量中.

#### 安装其他依赖 {#安装其他依赖-}

```
$ sudo apt-get install python-numpy swig python-dev

```

#### 可选: 安装 CUDA \(在 Linux 上开启 GPU 支持\) {#可选-安装-cuda-在-linux-上开启-gpu-支持-}

为了编译并运行能够使用 GPU 的 TensorFlow, 需要先安装 NVIDIA 提供的 Cuda Toolkit 7.0 和 CUDNN 6.5 V2.

TensorFlow 的 GPU 特性只支持 NVidia Compute Capability &gt;= 3.5 的显卡. 被支持的显卡 包括但不限于:

* NVidia Titan
* NVidia Titan X
* NVidia K20
* NVidia K40

##### 下载并安装 Cuda Toolkit 7.0 {#下载并安装-cuda-toolkit-70-}

[下载地址](https://developer.nvidia.com/cuda-toolkit-70)

将工具安装到诸如`/usr/local/cuda`之类的路径.

##### 下载并安装 CUDNN Toolkit 6.5 {#下载并安装-cudnn-toolkit-65-}

[下载地址](https://developer.nvidia.com/rdp/cudnn-archive)

解压并拷贝 CUDNN 文件到 Cuda Toolkit 7.0 安装路径下. 假设 Cuda Toolkit 7.0 安装 在`/usr/local/cuda`, 执行以下命令:

```
tar xvzf cudnn-6.5-linux-x64-v2.tgz
sudo cp cudnn-6.5-linux-x64-v2/cudnn.h /usr/local/cuda/include
sudo cp cudnn-6.5-linux-x64-v2/libcudnn* /usr/local/cuda/lib64
```

##### 配置 TensorFlow 的 Cuba 选项 {#配置-tensorflow-的-cuba-选项-}

从源码树的根路径执行:

```
$ ./configure
Do you wish to bulid TensorFlow with GPU support? [y/n] y
GPU support will be enabled for TensorFlow

Please specify the location where CUDA 7.0 toolkit is installed. Refer to
README.md for more details. [default is: /usr/local/cuda]: /usr/local/cuda

Please specify the location where CUDNN 6.5 V2 library is installed. Refer to
README.md for more details. [default is: /usr/local/cuda]: /usr/local/cuda

Setting up Cuda include
Setting up Cuda lib64
Setting up Cuda bin
Setting up Cuda nvvm
Configuration finished
```

这些配置将建立到系统 Cuda 库的符号链接. 每当 Cuda 库的路径发生变更时, 必须重新执行上述 步骤, 否则无法调用 bazel 编译命令.

##### 编译目标程序, 开启 GPU 支持 {#编译目标程序-开启-gpu-支持-}

从源码树的根路径执行:

```
$ bazel build -c opt --config=cuda //tensorflow/cc:tutorials_example_trainer

$ bazel-bin/tensorflow/cc/tutorials_example_trainer --use_gpu
# 大量的输出信息. 这个例子用 GPU 迭代计算一个 2x2 矩阵的主特征值 (major eigenvalue).
# 最后几行输出和下面的信息类似.
000009/000005 lambda = 2.000000 x = [0.894427 -0.447214] y = [1.788854 -0.894427]
000006/000001 lambda = 2.000000 x = [0.894427 -0.447214] y = [1.788854 -0.894427]
000009/000009 lambda = 2.000000 x = [0.894427 -0.447214] y = [1.788854 -0.894427]
```

注意, GPU 支持需通过编译选项 "--config=cuda" 开启.

##### 已知问题 {#已知问题-}

* 尽管可以在同一个源码树下编译开启 Cuda 支持和禁用 Cuda 支持的版本, 我们还是推荐在 在切换这两种不同的编译配置时, 使用 "bazel clean" 清理环境.

* 在执行 bazel 编译前必须先运行 configure, 否则编译会失败并提示错误信息. 未来, 我们可能考虑将 configure 步骤包含在编译过程中, 以简化整个过程, 前提是 bazel 能够提供新的特性支持这样.

### Mac OS X 安装 {#mac-os-x-安装-}

Mac 和 Linux 需要的软件依赖完全一样, 但是安装过程区别很大. 以下链接用于帮助你 在 Mac OS X 上安装这些依赖:

#### Bazel {#bazel-}

参见[本网页](http://bazel.io/docs/install.html)的 Mac OS X 安装指南.

#### SWIG {#swig-}

[Mac OS X 安装教程](http://www.swig.org/Doc3.0/Preface.html#Preface_osx_installation).

注意: 你需要安装[PCRE](ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/), 而_不是_PCRE2.

#### Numpy {#numpy-}

参见[安装教程](http://docs.scipy.org/doc/numpy/user/install.html).

### 创建 pip 包并安装 {#创建-pip-包并安装-}

```
$ bazel build -c opt //tensorflow/tools/pip_package:build_pip_package

$ bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg

# .whl 文件的实际名字与你所使用的平台有关
$ pip install /tmp/tensorflow_pkg/tensorflow-0.5.0-cp27-none-linux_x86_64.whl
```

## 训练你的第一个 TensorFlow 神经网络模型 {#训练你的第一个-tensorflow-神经网络模型-}

从源代码树的根路径执行:

```
$ cd tensorflow/models/image/mnist
$ python convolutional.py
Succesfully downloaded train-images-idx3-ubyte.gz 9912422 bytes.
Succesfully downloaded train-labels-idx1-ubyte.gz 28881 bytes.
Succesfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes.
Succesfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes.
Extracting data/train-images-idx3-ubyte.gz
Extracting data/train-labels-idx1-ubyte.gz
Extracting data/t10k-images-idx3-ubyte.gz
Extracting data/t10k-labels-idx1-ubyte.gz
Initialized!
Epoch 0.00
Minibatch loss: 12.054, learning rate: 0.010000
Minibatch error: 90.6%
Validation error: 84.6%
Epoch 0.12
Minibatch loss: 3.285, learning rate: 0.010000
Minibatch error: 6.2%
Validation error: 7.0%
...
...
```

## 常见问题 {#常见问题-}

### GPU 相关问题 {#gpu-相关问题-}

如果在尝试运行一个 TensorFlow 程序时出现以下错误:

```
ImportError: libcudart.so.7.0: cannot open shared object file: No such file or directory

```

请确认你正确安装了 GPU 支持, 参见[相关章节](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html#install_cuda).

### 在 Linux 上 {#在-linux-上-}

如果出现错误:

```
...
 "__add__", "__radd__",
             ^
SyntaxError: invalid syntax
```

解决方案: 确认正在使用的 Python 版本为 Python 2.7.

### 在 Mac OS X 上 {#在-mac-os-x-上-}

如果出现错误:

```
import six.moves.copyreg as copyreg

ImportError: No module named copyreg
```

解决方案: TensorFlow 使用的 protobuf 依赖`six-1.10.0`. 但是, Apple 的默认 python 环境 已经安装了`six-1.4.1`, 该版本可能很难升级. 这里提供几种方法来解决该问题:

1. 升级全系统的`six`:

   ```
    sudo easy_install -U six

   ```

2. 通过 homebrew 安装一个隔离的 python 副本:

   ```
    brew install python

   ```

3. 在[`virtualenv`](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html#virtualenv_install)内编译或使用 TensorFlow.

如果出现错误:

```
>>> import tensorflow as tf
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/lib/python2.7/site-packages/tensorflow/__init__.py", line 4, in <module>
    from tensorflow.python import *
  File "/usr/local/lib/python2.7/site-packages/tensorflow/python/__init__.py", line 13, in <module>
    from tensorflow.core.framework.graph_pb2 import *
...
  File "/usr/local/lib/python2.7/site-packages/tensorflow/core/framework/tensor_shape_pb2.py", line 22, in <module>
    serialized_pb=_b('\n,tensorflow/core/framework/tensor_shape.proto\x12\ntensorflow\"d\n\x10TensorShapeProto\x12-\n\x03\x64im\x18\x02 \x03(\x0b\x32 .tensorflow.TensorShapeProto.Dim\x1a!\n\x03\x44im\x12\x0c\n\x04size\x18\x01 \x01(\x03\x12\x0c\n\x04name\x18\x02 \x01(\tb\x06proto3')
TypeError: __init__() got an unexpected keyword argument 'syntax'
```

这是由于安装了冲突的 protobuf 版本引起的, TensorFlow 需要的是 protobuf 3.0.0. 当前 最好的解决方案是确保没有安装旧版本的 protobuf, 可以使用以下命令重新安装 protobuf 来解决 冲突:

```
brew reinstall --devel protobuf
```




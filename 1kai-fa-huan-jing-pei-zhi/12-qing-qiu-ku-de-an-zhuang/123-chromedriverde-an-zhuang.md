# 1.2.3 ChromeDriver的安装

selenium对chrome浏览器操作，需要进行以下配置

## 1.相关链接

* 下载地址：[https://chromedriver.storage.googleapis.com/index.html](https://sites.google.com/a/chromium.org/chromedriver/downloads)

## 2.查看Chrome版本

在chrome菜单中，点击帮助&gt;关于Chrome，可以查看chrome的版本号

## 3.下载ChromeDriver

打开官网可以查看，目前最新版本，其支持的chrome浏览器版本号

![](../../.gitbook/assets/1.2.3-1.png)



找到对应版本号后，下载对应的安装包:[https://chromedriver.storage.googleapis.com/index.html](https://chromedriver.storage.googleapis.com/index.html)

## 4.环境变量配置

下载完成后将ChromeDriver可执行文件配置到环境变量中

在windows平台下，直接把可执行文件拖入python的Scripts目录下，这样就配置到环境变量中了

在 Linux、Mac 下，需要将可执行文件配置到环境变量或将文件移动到属于环境变量的目录里。

例如移动文件到 /usr/bin 目录，首先命令行进入其所在路径，然后将其移动到 /usr/bin：

```text
sudo mv chromedriver /usr/bin
```

当然也可以将 ChromeDriver 配置到 $PATH，首先可以将可执行文件放到某一目录，目录可以任意选择，例如将当前可执行文件放在 /usr/local/chromedriver 目录下，接下来可以修改 ~/.profile 文件，命令如下：

```text
export PATH="$PATH:/usr/local/chromedriver"
```

保存然后执行：

```text
source ~/.profile
```

## 5.验证安装

在命令行下输入chrome driver命令进行验证![](../../.gitbook/assets/2.1.3-2.png)有类似结果输出就代表配置环境成功

然后在程序中测试

```text
from selenium import webdriver

browser = webdriver.Chrome()
```

如果有chrome浏览器自动打开，就代表配置成功


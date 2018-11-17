> 工欲善其事，必先利其器

### 安装Pycharm

官网:[https://www.jetbrains.com/pycharm/download/\#section=windows](https://www.jetbrains.com/pycharm/download/#section=windows)

进入官网

![](/assets/1.2.1.2-1.png)

有两个版本，professional是专业版，需要进行收费，community是社区版，是免费的

为了自己更好的进行学习，选用professional版本的

下载过程~

> 注意安装路径尽量不使用带有**中文或空格**的目录，这样在之后的使用过程中减少一些莫名的错误

安装完成后，不要着急打开，首先需要进行破解，不然无法使用

![](/assets/1.2.1.2-2.png)

这里采用补丁进行破解

IntelliJ IDEA注册码网站:[http://idea.lanyus.com/](http://idea.lanyus.com/)

![](/assets/1.2.1.2-3.png)

选择 破解补丁无需使用注册码，下载地址：[http://idea.lanyus.com/jar/JetbrainsCrack-3.1-release-enc.jar](http://idea.lanyus.com/jar/JetbrainsCrack-3.1-release-enc.jar) ，然后下载补丁，下载完后，将其放到 Pycharm 目录下 bin 目录中

如:E:\JetBrains\PyCharm 2018.2.3\bin

![](/assets/1.2.1.2-4.png)

在同目录下，有 pycharm.exe.vmoptions 和 pycharm64.exe.vmoptions 两个文件，分别对应32位的 和 64位的

在打开文件之前，需要下载[sublime ](https://www.sublimetext.com/3)或者 [notepad++](https://www.sublimetext.com/3) 两个软件，对文件进行打开

打开文件

![](/assets/1.2.1.2-5.png)

分别在32位和64位的文件末尾添加

```
-javaagent:E:\JetBrains\PyCharm 2018.2.3\bin\JetbrainsCrack-3.1-release-enc.jar
```

然后保存，便破解成功，打开软件，如果还出现如下图

![](/assets/1.2.1.2-2.png)

耐心等待，过一会儿，便破解成功了，只需点击ok即可

![](/assets/1.2.1.2-6.png)

现在安装好了pycharm，到后面就可以使用pycharm编写程序了


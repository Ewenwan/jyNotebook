解决方法一如下:

* 将之前的证书删除
  * 按下win + r 然后输入certmgr.msc 回车，出现管理器，找到之前生成的证书杀出即可

  ![](/assets/pro-15.17.5-1.png)
* 用一个叫”FiddlerCertMaker.exe“的工具重新打了一个证书，可以上网去找

* 重新打开fiddler即可

* 使用ios远程连接fiddler的代理地址，在线安装证书成功后，使用第三方浏览器访问，fiddler成功抓取到https的数据

* 访问地址，在右上角有个online，鼠标以上去，下面会显示出可用的本机ip地址，然后在第三方浏览器输入ip地址:8888\(端口号\)\(我的是192.168.99.1:8888\)即可，然后点击如第二张图所示的第二行，进行下载证书，然后进行安装即可，注意小米的可能会麻烦一点

![](/assets/pro-15.17.5-2.png)



![](/assets/pro-15.17-5-2.png)

### 说明

将做好的笔记上传到github里，并且与gitbook进行绑定，这样就能在网页上浏览自己的笔记了

* **README.md 和 SUMMARY.md 是两个必须文件**
  * README.md 是对书籍的简单介绍
  * SUMMARY.md 是书籍的目录结构

### 如何下载在github里的笔记

#### 安装git

官网:[https://gitforwindows.org/](https://gitforwindows.org/)

如果下载速度慢，或者访问速度慢，也可以在电脑管家里的软件里下载

#### 下载笔记

```
git clone path
```

![](/assets/g-2.2-1.png)

该[网页](https://github.com/CoderAngle/163spider)可以看到文本框里的地址，粘贴复制，进行下载

```
git clone https://github.com/CoderAngle/163spider.git
```

#### 上传笔记

* ##### 需要在github里注册一个账号
* 新建一个仓库

![](/assets/g-2.2-2.png)



![](/assets/g-2.2-3.png)

新建好后，可以看到一些教你如何上传的方法

##### 上传

```
git init 初始化文件目录

git add * 添加所有目录文件

git commit -m "提交的相关说明"

git remote add origin https://github.com/CoderAngle/machine-learing-code.git  提交到哪里

git push origin master -u 推送/上传内容

git pull origin master -u 拉取该文件内容

-f 强行推送
```




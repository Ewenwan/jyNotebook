# 1.4.2 MongoDB的安装

MongoDB 是由 C++ 语言编写的非关系型数据库，是一个基于分布式文件存储的开源数据库系统，其内容存储形式类似 Json 对象，它的字段值可以包含其他文档，数组及文档数组，非常灵活。

MongoDB 支持多种平台，包括 Windows、Linux、Mac OS、Solaris 等，在其官方网站均可找到对应的安装包，[https://www.mongodb.com/download-center](https://www.mongodb.com/download-center)

本节我们来看下它的安装过程。

## 1. 相关链接 {#1-相关链接}

* 官方网站：[https://www.mongodb.com](https://www.mongodb.com/)
* 官方文档：[https://docs.mongodb.com](https://docs.mongodb.com/)
* GitHub：[https://github.com/mongodb](https://github.com/mongodb)
* 中文教程：[http://www.runoob.com/mongodb/mongodb-tutorial.html](http://www.runoob.com/mongodb/mongodb-tutorial.html)

## 2. Windows下的安装 {#2-windows下的安装}

目前最新版本的MongoDB，不用这么麻烦的配置服务和日志了

直接在官网下载安装包即可，链接为：[https://www.mongodb.com/download-center\#community](https://www.mongodb.com/download-center#community)

![](/assets/11.2.4.2-1.png)

直接点击 Download 下载 msi 安装包即可。

下载完成之后双击开始安装，指定 MongoDB 的安装路径，例如在此处我指定安装路径为 C:\MongoDB\Server\3.4，当然路径可以自行选择

![](/assets/11.2.4.2-2.png)

点击下一步执行安装即可。

安装成功之后，进入 MongoDB 的安装目录，在此处所在路径是 C:\MongoDB\Server\3.4，在 bin 目录下新建同级目录 data

![](/assets/11.2.4.2-3.png)

然后进入 data 文件夹新建子文件夹 db，作为数据目录存储的文件夹，之后打开命令行，进入 MongoDB 安装目录的 bin 目录下，运行 MongoDB 服务：

```text
mongod --dbpath "C:\MongoDB\Server\3.4\data\db"
```

请记得将此处的路径替换成你的主机 MongoDB 安装路径。

如果想一直使用 MongoDB 就不能关闭此命令行，如果意外关闭或重启 MongoDB 服务就不能使用了，这显然不是我们想要的，所以接下来我们还需将 MongoDB 配置成系统服务。

首先我们要以管理员模式运行命令行，注意此处一定要是管理员模式运行，否则可能配置失败，如图 1-34 所示：



图 1-34 管理员模式

开始菜单搜索 cmd，找到命令行，然后右键以管理员身份运行即可。

随后新建一个日志文件，在 bin 目录同级目录新建 logs 文件夹，进入之后新建一个 mongodb.log 文件，用于保存 MongoDB 运行的日志，如图 1-35 所示。

![](/assets/11.2.4.2-4.png)

图 1-35 新建 mongodb.log 结果

在命令行下输入如下内容：

```text
mongod --bind_ip 0.0.0.0 --logpath "C:\MongoDB\Server\3.4\logs\mongodb.log" --logappend --dbpath "C:\MongoDB\Server\3.4\data\db" --port 27017 --serviceName "MongoDB" --serviceDisplayName "MongoDB" --install
```

这里的意思是绑定 IP 为 0.0.0.0，即任意 IP 均可访问，指定日志路径、数据库路径、端口，指定服务名称，注意这里依然需要把路径替换成你的 MongoDB 安装路径，运行此命令后即可安装服务。

如果没有出现错误提示，则证明 MongoDB 服务已经安装成功。

可以设置它的开机启动方式，如自动启动或手动启动等。这样我们就可以非常方便地管理 MongoDB 服务了。

启动服务之后我们在命令行下就可以利用 mongo 命令进入 MongoDB 命令交互环境了

这样 Windows 下 MongoDB 配置就完成了。

## 3. Linux下的安装 {#3-linux下的安装}

在这里以 MongoDB 3.4 为例说明 MongoDB 的安装过程。

### Ubuntu {#ubuntu}

首先导入 MongoDB 的 GPG Key：

```text
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```

随后创建 apt-get 源列表，各个系统版本对应的命令如下：

* Ubuntu 12.04

```text
echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

* Ubuntu 14.04

```text
echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

* Ubuntu 16.04

```text
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

随后更新 apt-get 源：

```text
sudo apt-get update
```

之后安装 MongoDB 即可：

```text
sudo apt-get install -y mongodb-org
```

安装完成之后运行 MongoDB，命令如下：

```text
mongod --port 27017 --dbpath /data/db
```

运行命令之后 MongoDB 就在 27017 端口上运行了，数据文件会保存在 /data/db 路径下。

一般我们在 Linux 上配置 MongoDB 都是为了远程连接使用的，所以在这里还需要配置一下 MongoDB 的远程连接和用户名密码：

接着我们进入到 MongoDB 命令行：

```text
mongo --port 27017
```

现在我们就已经进入到 MongoDB 的命令行交互模式下了，在此模式下运行如下命令：

```text
>use admin
switched to db admin

>db.createUser({user: 'admin', pwd: 'admin123', roles: [{role: 'root', db: 'admin'}]})
Successfully added user: {
        "user" : "admin",
        "roles" : [
                {
                        "role" : "root",
                        "db" : "admin"
                }
        ]
}
```

这样我们就创建了一个用户名为 admin，密码为 admin123 的用户，赋予最高权限。

随后需要修改 MongoDB 的配置文件，

执行如下命令：

```text
sudo vi /etc/mongod.conf
```

修改 net 部分为：

```text
net:
  port: 27017
  bindIp: 0.0.0.0
```

这样配置后 MongoDB 可被远程访问。

另外还需要添加如下权限认证配置，直接添加如下内容到配置文件：

```text
security:
 authorization: enabled
```

配置完成之后我们需要重新启动 MongoDB 服务，命令如下：

```text
sudo service mongod restart
```

这样远程连接和权限认证就配置完成了。

### CentOS、RedHat {#centos、redhat}

首先添加 MongoDB 源：

```text
sudo vi /etc/yum.repos.d/mongodb-org.repo
```

修改为如下内容保存：

```text
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

然后执行 yum 命令安装：

```text
sudo yum install mongodb-org
```

启动 MongoDB 服务：

```text
sudo systemctl start mongod
```

停止和重新加载 MongoDB 服务：

```text
sudo systemctl stop mongod
sudo systemctl reload mongod
```

有关远程连接和认证配置可以参考上文，方式是相同的。

更多 Linux 发行版的 MongoDB 安装方式可以参考官方文档：[https://docs.mongodb.com/manual/administration/install-on-linux/](https://docs.mongodb.com/manual/administration/install-on-linux/)。

## 4. Mac下的安装 {#4-mac下的安装}

推荐使用 Homebrew 安装，执行 brew 命令即可：

```text
brew install mongodb
```

然后创建一个新文件夹 /data/db，用于存放 MongoDB 数据。

启动 MongoDB 服务：

```text
brew services start mongodb
sudo mongod
```

这样就启动了 MongoDB 服务。

停止、重启 MongoDB 服务的命令：

```text
brew services stop mongodb
brew services restart mongodb
```

## 5.使用docker安装 {#5-可视化工具}

1.查找docker中的mongo

```text
sudo docker search mongo
```

2.拉取镜像

```text
sudo docker pull mongo:3.6
```

3.查看是否已经下载下来

```text
sudo docker images
```

4.运行mongo镜像

```text
sudo docker run -p 27917:27017 -e $PWD/db:/data/db -d mongo:3.6
```

5.查看容器启动情况

```text
sudo docker ps
```

## 6. 可视化工具 {#5-可视化工具}

RoboMongo/Robo 3T，官方网站：[https://robomongo.org/](https://robomongo.org/)，下载链接：[https://robomongo.org/download](https://robomongo.org/download)。

Studio 3T，官方网站：[https://studio3t.com](https://studio3t.com/)，下载链接：[https://studio3t.com/download/](https://studio3t.com/download/)。


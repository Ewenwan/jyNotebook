# 115 Redis的安装以及客户端连接

## redis在Ubuntu系统中的安装与启动

1.安装

```text
sudo apt-get install redis-server
```

2.卸载

```text
sudo apt-get purge --auto-remove redis-server
```

3.启动:

```text
查看是否启动
ps aux|grep redis

手动启动
sudo service redis-server start
```

4.停止

```text
sudo service redis-server stop
```

## Windows下安装redis

redis官网:[https://redis.io/](https://redis.io/)

GitHub:[https://github.com/MicrosoftArchive/redis/releases](https://github.com/MicrosoftArchive/redis/releases)

解压后bin目录下的文件

```text
redis-benchmark.exe         #基准测试
redis-check-aof.exe         # aof
redis-check-dump.exe        # dump
redis-cli.exe               # 客户端
redis-server.exe            # 服务器
redis.windows.conf          # 配置文件
```

用cd命令切换redis的目录并运行**redis-server.exe redis.windows.conf**

## 启动redis:

```text
ubuntu:sudo service redis-server
windows:net start redis
```

## 连接redis

```text
redis-cli -h [ip] -p[端口](默认端口为6379)
```

## Redis中文问题

```text
如果要在redis-cli中使用中文时，必须打开--raw选项，才能正常地显示中文
redis-cli --raw
```


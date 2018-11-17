打开配置文件,windows下的配置文件为"redis.windows-service.conf"，Ubuntu下的配置文件为"redis.conf"

* Ubuntu
  * cd /etc/redis,vim redis.conf
* windows
  * 找到配置文件，使用notepad记事本打开
* 找到bind,进行修改绑定本机地址

```text
bind 127.0.0.1 本机地址
```

打开配置文件,windows下的配置文件为"redis.windows-service.conf"，Ubuntu下的配置文件为"redis.conf"

* Ubuntu
  * cd /etc/redis,vim redis.conf
* windows
  * 找到配置文件，使用notepad记事本打开
* 找到bind,进行修改绑定本机地址

```text
bind 127.0.0.1 本机地址
```

### ![](/assets/1.4.4.1.10-1.png)

### redis问题

-MISCONF Redis is configured to save RDB snapshots, but is currently not able to persist on disk. Commands that may modify the data set are disabled. Please check Redis logs for details about the error.

出现如上错误，输入以下命令即可解决

```
config set stop-writes-on-bgsave-error no
```

### redis问题

-MISCONF Redis is configured to save RDB snapshots, but is currently not able to persist on disk. Commands that may modify the data set are disabled. Please check Redis logs for details about the error.

出现如上错误，输入以下命令即可解决

```
config set stop-writes-on-bgsave-error no
```




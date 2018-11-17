# 110 memcached的安装和参数详解

1. windows:
   * 安装:memcached -d install

     ```text
     32位系统 1.4.4版本：http://static.runoob.com/download/memcached-win32-1.4.4-14.zip
     64位系统 1.4.4版本：http://static.runoob.com/download/memcached-win64-1.4.4-14.zip
     32位系统 1.4.5版本：http://static.runoob.com/download/memcached-1.4.5-x86.zip
     64位系统 1.4.5版本：http://static.runoob.com/download/memcached-1.4.5-amd64.zip
     ```

   * 启动:memcached -d start
   * 停止:memcached.exe -d stop
   * 卸载:memcached.exe -d uninstall
   * memcached版本&gt;=1.45

     * 安装

     ```text
     schtasks /create /sc onstart /tn memcached /tr "'F:\software\memcached>memcached.exe' -m 512"

     注意：-m 512 意思是设置 memcached 最大的缓存配置为512M。我们可以通过使用
      "memcached.exe -h" 命令查看更多的参数配置。
     ```
2. linux\(ubuntu\):
   * 安装:sudo apt-get install memcached
   * 启动:sudo service memcached start
   * 查看是否启动成功

     ```text
     查看当前所有端口
     ps aux|grep memcached
     ```

   * 建议使用windows自带的linux子系统
   * 注意:ufw allow 11211
3. 可能出现的问题:
   * 提示没有权限:使用管理员权限
   * 不要放在含有中文的路径下面
   * 提示缺少pthreadGC2.dll文件；将缺少文件拷贝到windows/System32中

```text
/usr/bin/memcached -u memcache start

# 后台运行
/usr/bin/memcached -u memcache -d start

# 杀掉所有memcached进程
sudo killall memcached
```

4.启动memcached:

```text
注意:指定用户
```

* -d:这个参数是让memcached在后台运行
* -m:指定占用多少内存，以n为单位，默认为64M
* -p:指定占用的端口。默认的端口是11211
* -l:别的机器可以通过哪个ip地址链接到这台服务器。想要别的机器链接，就必须配置'-l 0.0.0.0'

```text
 /usr/bin/memcached -u memcache -l 0.0.0.0 -d start
```


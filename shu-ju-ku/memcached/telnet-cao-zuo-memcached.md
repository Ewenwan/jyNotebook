windows下可能没有启动telnet，需要手动启动telnet服务

### 启动Telnet

首先win+R，在弹出框中输入control并点击打开，打开后，点击程序，可以看见如下图所示

![](/assets/1.4.2.1-1.png)

然后点击启用或关闭Windows功能

![](/assets/1.4.2.1-2.png)

打开后，勾选telnet客户端选项，然后点击确定，便可以安装telent了，安装完成后，重启后，便可以正式使用了。

> 接下来开始学习telnet操作memcached的方法

---

### telnet 登录memcached

命令格式:

```
telnet ip 地址 端口号
```

示例:

```
telnet 127.0.0.1 11211
```

> 温馨提示:memcached 存储数据是以键值对的方式存储的

#### 添加数据

* set 命令（设置）

  * 语法格式
    ```
    set key 0(否)(是否压缩) timeout(过期时间) value_length(字符串的长度)
    ```
  * 示例

    ```
    set name 0 60 5
    angle
    STORED
    ```

* add 命令（添加）

  * 语法格式

    ```
    add key 0 timeout value_length
    ```

  * 示例

    ```
    add name 0 60 2
    ab
    STORED
    ```

> 温馨提示:
>
> set 和 add 的区别:add是只负责添加数据，不会去修改数据。如果添加的数据的key已经存在了，则添加失败，如果是添加的key不存在，则添加成功。而set不同，如果memcached中不存在相同的key，则进行添加，如果存在，则替换。

#### 获取数据

* get 命令
  * 语法格式
    ```
    get key
    ```
  * 示例
    ```
    get name
    angle
    ```

#### 删除数据

* delete 命令

  * 语法格式
    ```
    delete key
    ```
  * 示例
    ```
    delete name
    ```

* flush\_all 命令

  * 语法格式

    ```
    flush_all
    ```

  * 删除memcached中的所有键值对

#### 查看memcached的当前状态

* status 命令
  ```
  'get_hists':get命令命中了多少次
  'get_misses':get命令get空了几次
  'curr_items':当前'memcached'中的键值对的个数
  'total_connections':从'memcached'开启到现在总共的连接数
  'curr_connections':当前'memcached'的连接数
  ‘memcached’默认醉的连接数是1024
  ```

#### 增加

```
set age 0 120 2  > 20
incr age 2 > 22
注意:必须都是数值类型，不然会报错
```

#### 减少

```
decr age 2  > 20
```




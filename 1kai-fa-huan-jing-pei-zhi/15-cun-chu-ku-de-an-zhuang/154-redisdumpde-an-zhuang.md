# 1.5.4 RedisDump的安装

## 1.说明

RedisDump是一个用于Redis数据导入导出的工具，是基于Ruby实现的，所以要安装RedisDump需要安装Ruby

## 2. 相关链接 {#1-相关链接}

* GitHub：[https://github.com/delano/redis-dump](https://github.com/delano/redis-dump)
* 官方文档：[http://delanotes.com/redis-dump](http://delanotes.com/redis-dump)

## 3.安装Ruby

官网:[http://www.ruby-lang.org/zh\_cn/documentation/installation](http://www.ruby-lang.org/zh_cn/documentation/installation)

windows-下载地址:[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)

![](../../.gitbook/assets/1.5.4-1.png)msys2:[http://repo.msys2.org/distrib/x86\_64/msys2-x86\_64-20180531.exe](http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20180531.exe)

## 3.Gem安装

打开Start Command Prompt with Ruby

![](../../.gitbook/assets/15.4-4.png)![](../../.gitbook/assets/1.5.4-6.png)如果出现上面类似情况，需要更换源

```text
$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
或者 
添加淘宝镜像：gem source -a http://ruby.taobao.org/ --remove https://rubygems.org/

# 查看源
$ gem sources -l
*** CURRENT SOURCES ***

https://gems.ruby-china.org
```

利用gem命令安装

```text
gem install redis-dump
```

下面是报错：

```text
Temporarily enhancing PATH for MSYS/MINGW...
Building native extensions. This could take a while...
ERROR:  Error installing jekyll:
        ERROR: Failed to build gem native extension.

    current directory: C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
C:/Ruby25-x64/bin/ruby.exe -r ./siteconf20180308-3672-ueo7ea.rb extconf.rb
creating Makefile

current directory: C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
make "DESTDIR=" clean
'make' 不是内部或外部命令，也不是可运行的程序或批处理文件。

current directory: C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
make "DESTDIR="
'make' 不是内部或外部命令，也不是可运行的程序或批处理文件。

make failed, exit code 1

Gem files will remain installed in C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/http_p
arser.rb-0.6.0 for inspection.
Results logged to C:/Ruby25-x64/lib/ruby/gems/2.5.0/extensions/x64-mingw32/2.5.0
/http_parser.rb-0.6.0/gem_make.out
```

如果出现如上类似错误

原来是没有make指令，需要安装

```text
ridk install
```

![](../../.gitbook/assets/1.5.4-7.png)等待安装完毕，期间网速可能会很慢

安装完后，重新安装redis-dump

需要安装证书,可以在这里下载:[https://www.digicert.com/digicert-root-certificates.htm](https://www.digicert.com/digicert-root-certificates.htm)

## 4.验证安装

安装成功后就可以执行如下两个命令：

```text
redis-dump
redis-load
```

#### 使用redis-dump导出数据

导出指令如下：

```text
redis-dump -u :mypassword@localhost:6379 -d database_name >test.json
```

-u 后边跟redis数据库的信息，如果没有密码可以不写

```text
redis-dump -u localhost:6379 -d database_name  >test.json
```

如果直接导出本机端口为6379的可以把 -u 的部分给省去

```text
redis-dump >test.json
```

-d 指定导出哪个数据库的数据，如果不写则导出所有的，一定要注意数据库名字（这里是 database\_name ）前后必须要加空格。![](../../.gitbook/assets/1.5.4-8.png)如果导出数据时，出现以上错误，应该如下解决

```text
首先打开dump.rb文件进行编辑，这里推荐使用notepad记事本
如下:
C:\Ruby25-x64\lib\ruby\gems\2.5.0\gems\redis-dump-0.4.0\lib\redis\dump.rb

然后在文本中的第32行，用#进行注释
如下:
#        `ps -o rss= -p #{Process.pid}`.to_i # in kb
```

#### 使用**redis-load还原数据**

导入指令如下:

```text
< test.json redis-load //导入数据 


#导入
cat redis.json | redis-load -u :password@localhost
```

### redis-dump命令

```text
    -u, --uri=S                      Redis URI (e.g. redis://hostname[:port])
    -d, --database=S                 Redis database (e.g. -d 15)
    -a, --password=S                 Redis password (e.g. -a 'my@pass/word')
    -s, --sleep=S                    Sleep for S seconds after dumping (for debugging)
    -c, --count=S                    Chunk size (default: 10000)
    -f, --filter=S                   Filter selected keys (passed directly to redis' KEYS command)
    -b, --base64                     Encode key values as base64 (useful for binary values)
    -O, --without_optimizations      Disable run time optimizations
    -V, --version                    Display version
    -D, --debug
        --nosafe
```


# 3.1.4 分析Robots协议

## 1.说明

利用 Urllib 的 robotparser 模块我们可以实现网站 Robots 协议的分析

## 2. Robots协议 {#1-robots协议}

Robots 协议也被称作爬虫协议、机器人协议，它的全名叫做网络爬虫排除标准（Robots Exclusion Protocol），用来告诉爬虫和搜索引擎哪些页面可以抓取，哪些不可以抓取。它通常是一个叫做 robots.txt 的文本文件，放在网站的根目录下。

当搜索爬虫访问一个站点时，它首先会检查下这个站点根目录下是否存在 robots.txt 文件，如果存在，搜索爬虫会根据其中定义的爬取范围来爬取。如果没有找到这个文件，那么搜索爬虫便会访问所有可直接访问的页面。

例如:

```text
https://blog.csdn.net/robots.txt
```

robots.txt内容:

```text
User-agent: *
Disallow: /css/
Disallow: /images/
Disallow: /content/
Disallow: /ui/
Disallow: /js/

Sitemap: https://blog.csdn.net/s/sitemap/pcsitemapindex.xml
```

User-agent 描述了搜索爬虫的名称，在这里将值设置为 \*，则代表该协议对任何的爬取爬虫有效

Disallow 指定了不允许抓取的目录，比如上述例子中设置为/则代表不允许抓取所有页面。

Allow 一般和 Disallow 一起使用，一般不会单独使用，用来排除某些限制，现在我们设置为 /public/ ，起到的作用是所有页面不允许抓取，但是 public 目录是可以抓取的

## 3. 爬虫名称 {#2-爬虫名称}

大家可能会疑惑，爬虫名是哪儿来的？为什么就叫这个名？其实它是有固定名字的了，比如百度的就叫做 BaiduSpider，下面的表格列出了一些常见的搜索爬虫的名称及对应的网站：

| 爬虫名称 | 名称 | 网站 |
| :--- | :--- | :--- |
| BaiduSpider | 百度 | www.baidu.com |
| Googlebot | 谷歌 | www.google.com |
| 360Spider | 360搜索 | www.so.com |
| YodaoBot | 有道 | www.youdao.com |
| ia\_archiver | Alexa | www.alexa.cn |
| Scooter | altavista | www.altavista.com |

## 4. robotparser {#3-robotparser}

了解了什么是 Robots 协议之后，我们就可以使用 robotparser 模块来解析 robots.txt 了。

robotparser 模块提供了一个类，叫做 RobotFileParser。它可以根据某网站的 robots.txt 文件来判断一个爬取爬虫是否有权限来爬取这个网页。

语法声明:

```text
urllib.robotparser.RobotFileParser(url='')
```

使用这个类的时候非常简单，只需要在构造方法里传入 robots.txt的链接即可。当然也可以声明时不传入，默认为空，再使用 set\_url\(\) 方法设置一下也可以。

有常用的几个方法分别介绍一下：

* set\_url\(\)，用来设置 robots.txt 文件的链接。如果已经在创建 RobotFileParser 对象时传入了链接，那就不需要再使用这个方法设置了。
* read\(\)，读取 robots.txt 文件并进行分析，注意这个函数是执行一个读取和分析操作，如果不调用这个方法，接下来的判断都会为 False，所以一定记得调用这个方法，这个方法不会返回任何内容，但是执行了读取操作。
* parse\(\)，用来解析 robots.txt 文件，传入的参数是 robots.txt 某些行的内容，它会按照 robots.txt 的语法规则来分析这些内容。
* can\_fetch\(\)，方法传入两个参数，第一个是 User-agent，第二个是要抓取的 URL，返回的内容是该搜索引擎是否可以抓取这个 URL，返回结果是 True 或 False。
* mtime\(\)，返回的是上次抓取和分析 robots.txt 的时间，这个对于长时间分析和抓取的搜索爬虫是很有必要的，你可能需要定期检查来抓取最新的 robots.txt。
* modified\(\)，同样的对于长时间分析和抓取的搜索爬虫很有帮助，将当前时间设置为上次抓取和分析 robots.txt 的时间。

实例:

```text
from urllib.robotparser import  RobotFileParser

rp = RobotFileParser()
rp.set_url('http://www.jianshu.com/robots.txt')
rp.read()
print(rp.can_fetch('*', 'http://www.jianshu.com/p/b67554025d7d'))
print(rp.can_fetch('*', "http://www.jianshu.com/search?q=python&page=1&type=collections"))
```

以简书为例，我们首先创建 RobotFileParser 对象，然后通过 set\_url\(\) 方法来设置了 robots.txt 的链接。当然不用这个方法的话，可以在声明时直接用如下方法设置：

```text
rp = RobotFileParser('http://www.jianshu.com/robots.txt')
```

利用 can\_fetch\(\) 方法来判断了网页是否可以被抓取

运行结果:

```text
False
False
```

可以使用 parser\(\) 方法执行读取和分析

实例:

```text
from urllib.robotparser import RobotFileParser
from urllib.request import urlopen

rp = RobotFileParser()
rp.parse(urlopen('https://blog.csdn.net/robots.txt').read().decode('utf-8').split('\n'))
print(rp.can_fetch('*', 's://blog.csdn.net/Linear_Luo/article/details/52231550'))
```

运行结果:

```text
True
```

tips:一般都不会用这个


# 1.9.4 ScrapydAPI的安装

## 1.说明

安装好了 Scrapyd 之后，我们可以直接请求它提供的 API 即可获取当前主机的 Scrapy 任务运行状况。

如某台主机的 IP 为 192.168.1.1，则可以直接运行如下命令获取当前主机的所有 Scrapy 项目：

```text
C:\Users\miku>curl http://localhost:6800/listprojects.json
{"node_name": "overload", "status": "ok", "projects": []}
```

返回结果是 Json 字符串，通过解析这个字符串我们便可以得到当前主机所有项目。

curl下载地址:[https://curl.haxx.se/download.html](https://curl.haxx.se/download.html)

## 2. 相关链接 {#1-相关链接}

* GitHub：[https://pypi.python.org/pypi/python-scrapyd-api/](https://pypi.python.org/pypi/python-scrapyd-api/)
* PyPi：[https://pypi.python.org/pypi/python-scrapyd-api](https://pypi.python.org/pypi/python-scrapyd-api)
* 官方文档：[http://python-scrapyd-api.readthedocs.io/en/latest/usage.html](http://python-scrapyd-api.readthedocs.io/en/latest/usage.html)

## 3. 安装 {#2-pip安装}

```text
pip install python-scrapyd-api
```

## 3. 验证安装 {#3-验证安装}

安装完成之后便可以使用 Python 来获取主机状态了，所以如上的操作便可以用 Python 代码实现：

```text
from scrapyd_api import ScrapydAPI
scrapyd = ScrapydAPI("http://127.0.0.1:6800")
print(scrapyd.list_projects())
```

运行结果：

```text
[]
```

这样我们便可以用 Python 直接来获取各个主机上 Scrapy 任务的运行状态了。


# 3.1 使用urllib

## 1.相关链接

官方文档:[https://docs.python.org/3/library/urllib.html](https://docs.python.org/3/library/urllib.html)

测试网站:httpbin.org

## 2.内容

Urllib 库，是 Python 内置的 HTTP 请求库，包含四个模块：

* urllib.request:用于请求URL
* urllib.error:异常处理模块，如果出现请求错误，我们可以捕获这些异常，然后进行重试或其他操作保证程序不会意外终止
* urllib.parse:用于解析URL
* urllib.robotparser:用于解析robots.txt文件


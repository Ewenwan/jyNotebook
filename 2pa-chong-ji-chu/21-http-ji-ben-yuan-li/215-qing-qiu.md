# 2.1.5 请求

## Request

Request，即请求，由客户端向服务端发出。

Request 有四部分内容：

* Request Method\(请求方式\)
* Request URL\(请求链接\)
* Request Headers\(请求头\)
* Request Body\(请求体\)

## Request Method

请求方式中有两种常见的类型:GET和POST

_GET:_从指定的资源请求数据。比如在谷歌中直接搜索花，这便发起了一个get请求，请求的参数会直接包含到url中，如:[https://www.google.com.hk/search?q=花&oq=花&aqs=chrome..69i57j69i60l4.5466j0j7&sourceid=chrome&ie=UTF-8，url中包含了请求的参数信息，这里的参数q就是搜索的关键字](https://www.google.com.hk/search?q=花&oq=花&aqs=chrome..69i57j69i60l4.5466j0j7&sourceid=chrome&ie=UTF-8，url中包含了请求的参数信息，这里的参数q就是搜索的关键字)

_POST:_向指定的资源提交要被处理的数据。POST 请求大多为表单提交发起，如一个登录表单，输入用户名密码，点击登录按钮，这通常会发起一个 POST 请求，其数据通常以 Form Data 即表单的形式传输，不会体现在 URL 中。

GET 和 POST 请求方法有如下区别：

* GET 方式请求中参数是包含在 URL 里面的，数据可以在 URL 中看到，而 POST 请求的 URL 不会包含这些数据，数据都是通过表单的形式传输，会包含在 Request Body 中。
* GET 方式请求提交的数据最多只有 1024 字节，而 POST 方式没有限制。

请求方式以及描述

| 方法 |
| :--- |


|  | 描述 |
| :--- | :--- |
| GET | 请求指定的页面信息，并返回实体主体。 |
| HEAD | 类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头。 |
| POST | 向指定资源提交数据进行处理请求，数据被包含在请求体中。 |
| PUT | 从客户端向服务器传送的数据取代指定的文档的内容。 |
| DELETE | 请求服务器删除指定的页面。 |
| CONNECT | HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。 |
| OPTIONS | 允许客户端查看服务器的性能。 |
| TRACE | 回显服务器收到的请求，主要用于测试或诊断。 |

本表参考：[http://www.runoob.com/http/http-methods.html](http://www.runoob.com/http/http-methods.html)

### Request URL {#request-url}

请求的网址，即统一资源定位符，用 URL 可以唯一确定我们想请求的资源。

### Request Headers {#request-headers}

请求头，用来说明服务器要使用的附加信息，比较重要的信息有 Cookie、Referer、User-Agent 等，下面将一些常用的头信息说明如下：

* Accept，请求报头域，用于指定客户端可接受哪些类型的信息。
* Accept-Language，指定客户端可接受的语言类型。
* Accept-Encoding，指定客户端可接受的内容编码。
* Host，用于指定请求资源的主机 IP 和端口号，其内容为请求 URL 的原始服务器或网关的位置。从 HTTP 1.1 版本开始，Request 必须包含此内容。
* Cookie，也常用复数形式 Cookies，是网站为了辨别用户进行 Session 跟踪而储存在用户本地的数据。Cookies 的主要功能就是维持当前访问会话。
* Referer，此内容用来标识这个请求是从哪个页面发过来的，服务器可以拿到这一信息并做相应的处理，如做来源统计、做防盗链处理等。
* User-Agent，简称 UA，它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版本、浏览器及版本等信息。在做爬虫时加上此信息可以伪装为浏览器，如果不加很可能会被识别出为爬虫。
* Content-Type，即 Internet Media Type，互联网媒体类型，也叫做 MIME 类型，在 HTTP 协议消息头中，使用它来表示具体请求中的媒体类型信息。例如 text/html 代表 HTML 格式，image/gif 代表 GIF 图片，application/json 代表 Json 类型，更多对应关系可以查看此对照表：[http://tool.oschina.net/commons](http://tool.oschina.net/commons)。

Request Headers 是 Request 等重要组成部分，在写爬虫的时候大部分情况都需要设定 Request Headers。

### Request Body {#request-body}

即请求体，一般承载的内容是 POST 请求中的 Form Data，即表单数据，而对于 GET 请求 Request Body 则为空。

下面列出了 Content-Type 和 POST 提交数据方式的关系：

| Content-Type | 提交数据方式 |
| :--- | :--- |
| application/x-www-form-urlencoded | Form 表单提交 |
| multipart/form-data | 表单文件上传提交 |
| application/json | 序列化 Json 数据提交 |
| text/xml | XML 数据提交 |

在爬虫中如果我们要构造 POST 请求需要注意这几种 Content-Type，了解各种请求库的各个参数设置时使用的是哪种 Content-Type，不然可能会导致 POST 提交后得不到正常的 Response。


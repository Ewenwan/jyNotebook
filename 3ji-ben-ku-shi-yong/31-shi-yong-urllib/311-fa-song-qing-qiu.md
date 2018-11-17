# 3.1.1 发送请求

## 1.相关链接

* 官方文档
  * [https://docs.python.org/3/library/urllib.request.html](https://docs.python.org/3/library/urllib.request.html)
  * [https://docs.python.org/3/library/urllib.request.html\#basehandler-objects](https://docs.python.org/3/library/urllib.request.html#basehandler-objects)

测试网站:[http://httpbin.org/post](http://httpbin.org/post)

## 2. urlopen\(\) {#1-urlopen}

urllib.request 模块提供了最基本的构造 HTTP 请求的方法，利用它可以模拟浏览器的一个请求发起过程，同时它还带有处理authenticaton（授权验证），redirections（重定向\)，cookies（浏览器Cookies）以及其它内容。

例子:抓取百度首页

```text
import urllib.request

response = urllib.request.urlopen("http://www.baidu.com")
print(response.read().decode('utf-8'))
print(type(response))
```

运行结果:

![](../../.gitbook/assets/3.1.1-1.png)

输出的类型:

```text
<class 'http.client.HTTPResponse'>
```

通过输出结果可以发现它是一个 HTTPResposne 类型的对象，主要包含的方法有 read\(\)、readinto\(\)、getheader\(name\)、getheaders\(\)、fileno\(\) 等方法和 msg、version、status、reason、debuglevel、closed 等属性。

可以利用response对象调用这些属性，例子:

```text
import urllib.request

response = urllib.request.urlopen("http://www.baidu.com")
print(response.status) # 状态码
print(response.getheaders()) # 响应头信息
print(response.getheader('Server')) # headers中server的值
```

输出结果为:

```text
200
[('Bdpagetype', '1'), ('Bdqid', '0xef591dd800056531'), ('Cache-Control', 'private'), ('Content-Type', 'text/html'), ('Cxy_all', 'baidu+16f7eb85af21b1161c1ef2120b208c5a'), ('Date', 'Mon, 30 Jul 2018 06:01:58 GMT'), ('Expires', 'Mon, 30 Jul 2018 06:01:28 GMT'), ('P3p', 'CP=" OTI DSP COR IVA OUR IND COM "'), ('Server', 'BWS/1.1'), ('Set-Cookie', 'BAIDUID=ADA3E646B4E0A6AE8F0BA17B395B76A3:FG=1; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com'), ('Set-Cookie', 'BIDUPSID=ADA3E646B4E0A6AE8F0BA17B395B76A3; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com'), ('Set-Cookie', 'PSTM=1532930518; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com'), ('Set-Cookie', 'delPer=0; expires=Wed, 22-Jul-2048 06:01:28 GMT'), ('Set-Cookie', 'BDSVRTM=0; path=/'), ('Set-Cookie', 'BD_HOME=0; path=/'), ('Set-Cookie', 'H_PS_PSSID=1441_25810_26458_21121_18559_26350_26920_22160; path=/; domain=.baidu.com'), ('Vary', 'Accept-Encoding'), ('X-Ua-Compatible', 'IE=Edge,chrome=1'), ('Connection', 'close'), ('Transfer-Encoding', 'chunked')]
BWS/1.1
```

urlopen\(\)函数的API:

`urllib.request.urlopen（url，data = None，[ timeout，] *，cafile = None，capath = None，cadefault = False，context = None ）`

## data参数

data 参数是可选的，如果要添加 data，它要是字节流编码格式的内容，即 bytes 类型，通过 bytes\(\) 方法可以进行转化，另外如果传递了这个 data 参数，它的请求方式就不再是 GET 方式请求，而是 POST。

模拟一个post请求:

```text
import urllib.parse
import urllib.request

data = bytes(urllib.parse.urlencode({"name":"angle"}),encoding="utf-8")
response = urllib.request.urlopen("http://httpbin.org/post",data=data)
print(response.read().decode('utf-8'))
```

运行结果如下:

```text
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "angle"
  }, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Connection": "close", 
    "Content-Length": "10", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Python-urllib/3.6"
  }, 
  "json": null, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/post"
}
```

## timeout参数

timeout 参数可以设置超时时间，单位为秒，意思就是如果请求超出了设置的这个时间还没有得到响应，就会抛出异常，如果不指定，就会使用全局默认时间。它支持 HTTP、HTTPS、FTP 请求。

实例:

```text
import urllib.request

response = urllib.request.urlopen("http://httpbin.org/get",timeout=0.1)
print(response.read().decode("utf-8"))
```

运行结果如下:

```text
....

During handling of the above exception, another exception occurred:

....
  File "E:\Python36\lib\urllib\request.py", line 1320, in do_open
    raise URLError(err)
urllib.error.URLError: <urlopen error timed out>
```

设置超时时间为0.1秒，程序超过0.1秒没有响应，就会抛出URLError异常，属于urllib.error模块，错误的原因是超时

可以利用try/except语句来跳过长时间未响应的页面

```text
import urllib.request
import urllib.error
import socket

try:
    response = urllib.request.urlopen("http://httpbin.org/get",timeout=0.1)
except urllib.error.URLError as e:
    if isinstance(e.reason,socket.timeout):
        print("TIME OUT")
```

运行结果:

```text
TIME OUT
```

## 其他参数

还有 context 参数，它必须是 ssl.SSLContext 类型，用来指定 SSL 设置。

cafile 和 capath 两个参数是指定 CA 证书和它的路径，这个在请求 HTTPS 链接时会有用。

cadefault 参数现在已经弃用了，默认为 False。

## 2.Request

例子:

```text
import urllib.request

request = urllib.request.Request("https://python.org")
response = urllib.request.urlopen(request)
print(response.read().decode('utf-8'))
```

urlopen\(\) 方法的参数不再是一个 URL，而是一个 Request 类型的对象，通过构造这个这个数据结构，一方面我们可以将请求独立成一个对象，另一方面可配置参数更加丰富和灵活

Request函数API:

```text
class urllib.request.Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None)
```

* url 参数是请求 URL，这个是必传参数，其他的都是可选参数。
* data 参数如果要传必须传 bytes（字节流）类型的，如果是一个字典，可以先用 urllib.parse 模块里的 urlencode\(\) 编码。
* headers 参数是一个字典，这个就是 Request Headers ，可以在构造 Request 时通过 headers 参数直接构造，也可以通过调用 Request 实例的 add\_header\(\) 方法来添加。

添加 Request Headers 最常用的用法就是通过修改 User-Agent 来伪装浏览器，默认的 User-Agent 是 Python-urllib，我们可以通过修改它来伪装浏览器，比如要伪装火狐浏览器，你可以把它设置为：

```text
Mozilla/5.0 (X11; U; Linux i686) Gecko/20071127 Firefox/2.0.0.11
```

* origin\_req\_host 参数指的是请求方的 host 名称或者 IP 地址。
* unverifiable 参数指的是这个请求是否是无法验证的，默认是False。意思就是说用户没有足够权限来选择接收这个请求的结果。例如我们请求一个 HTML 文档中的图片，但是我们没有自动抓取图像的权限，这时 unverifiable 的值就是 True。
* method 参数是一个字符串，它用来指示请求使用的方法，比如GET，POST，PUT等等。

实例:

```text
from urllib import request,parse

url = 'http://httpbin.org/post'
# 伪造请求头
headers = {
    'User-Agent': 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)',
    'Host': 'httpbin.org'
}
# 构造参数
dict = {
    'name':"angle",
}
# 转换为字节流
data = bytes(parse.urlencode(dict),encoding='utf-8')
req = request.Request(url=url,data=data,headers=headers,method='POST')
response = request.urlopen(req)
print(response.read().decode('utf-8'))
```

运行结果:

```text
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "angle"
  }, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Connection": "close", 
    "Content-Length": "10", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)"
  }, 
  "json": null, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/post"
}
```

通过四个参数构造了一个 Request，url 即请求 URL，在headers 中指定了 User-Agent 和 Host，传递的参数 data 用了 urlencode\(\) 和 bytes\(\) 方法来转成字节流，并指定了请求方式为 POST。

另外一种添加headers的方法：

利用add\_header\(\)方法来添加headers

```text
req = request.Request(url=url,data=data,method='POST')
req.add_header('User-Agent','Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)')
```

注意add\_header\(\):add\_header\(key,value\)

## 3. 高级用法 {#3-高级用法}

利用Handler 处理Cookies 处理，代理设置等操作

urllib.request 模块里的 BaseHandler类，是所有其他 Handler 的父类，提供了最基本的 Handler 的方法，例如 default\_open\(\)、protocol\_request\(\) 方法等。

接下来就有各种 Handler 子类继承这个 BaseHandler 类，举例几个如下：

* HTTPDefaultErrorHandler 用于处理 HTTP 响应错误，错误都会抛出 HTTPError 类型的异常。
* HTTPRedirectHandler 用于处理重定向。
* HTTPCookieProcessor 用于处理 Cookies。
* ProxyHandler 用于设置代理，默认代理为空。
* HTTPPasswordMgr 用于管理密码，它维护了用户名密码的表。
* HTTPBasicAuthHandler 用于管理认证，如果一个链接打开时需要认证，那么可以用它来解决认证问题。
* 另外还有其他的 Handler 类，在这不一一列举了，详情可以参考官方文档：

  [https://docs.python.org/3/library/urllib.request.html\#urllib.request.BaseHandler](https://docs.python.org/3/library/urllib.request.html#urllib.request.BaseHandler)

另外一个比较重要的类就是 OpenerDirector，可以称之为 Opener，之前用过 urlopen\(\) 这个方法，实际上它就是 Urllib提供的一个 Opener。

那么为什么要引入 Opener ？因为需要实现更高级的功能，之前使用的 Request、urlopen\(\) 相当于类库封装好了极其常用的请求方法，利用它们两个就可以完成基本的请求，但是现在不一样了，需要实现更高级的功能，所以需要深入一层进行配置，使用更底层的实例来完成我们的操作。

所以，在这里就用到了比调用 urlopen\(\) 的对象的更普遍的对象，也就是 Opener。

Opener 可以使用 open\(\) 方法，返回的类型和 urlopen\(\) 如出一辙。那么它和 Handler 有什么关系？简而言之，就是利用 Handler 来构建 Opener。

### 认证 {#认证}

有些网站在打开时它就弹出了一个框，直接提示输入用户名和密码，认证成功之后才能查看页面：

![](../../.gitbook/assets/3.1.1-3.png)

请求这样的页面需要借助于 HTTPBasicAuthHandler 就可以完成

实例:

```text
from urllib.request import HTTPPasswordMgrWithDefaultRealm,HTTPBasicAuthHandler,build_opener
from urllib.error import  URLError

username = 'username'
password = 'password'
url = 'http://localhost:5000/'

# 实例化HTTPPasswordMgrWithDefaultRealm 对象
p = HTTPPasswordMgrWithDefaultRealm()
# 利用HTTPPasswordMgrWithDefaultRealm 对象添加相关信息，这样就建立了认证的Handler
p.add_password(None,url,username,password)
auth_handler = HTTPBasicAuthHandler(p)
# 构建一个opener，在发送请求时就认证成功了
opener = build_opener(auth_handler)

try:
    # 打开网址
    result = opener.open(url)
    # 源码
    html = result.read().decode('utf-8')
    print(html)
except URLError as e:
    print(e.reason)
```

首先实例化了一个 HTTPBasicAuthHandler 对象，参数是 HTTPPasswordMgrWithDefaultRealm 对象，它利用 add\_password\(\) 添加进去用户名和密码，这样我们就建立了一个处理认证的 Handler。

接下来利用 build\_opener\(\) 方法来利用这个 Handler 构建一个 Opener，那么这个 Opener 在发送请求的时候就相当于已经认证成功了。

接下来利用 Opener 的 open\(\) 方法打开链接，就可以完成认证了，在这里获取到的结果就是认证后的页面源码内容。

### 代理 {#代理}

添加代理

```text
from urllib.error import URLError
from urllib.request import ProxyHandler,build_opener

# 建立代理池
proxy_handler = ProxyHandler({
    'http': 'http://127.0.0.1:5000',
    'https': 'https://127.0.0.1:5000'
})

opener = build_opener(proxy_handler)

try:
    response = opener.open('https://www.baidu.com')
    print(response.read().decode('utf-8'))
except URLError as e:
    print(e.reason)
```

在本地搭建一个代理，运行在9743端口上

使用了 ProxyHandler，ProxyHandler 的参数是一个字典\(协议类型:代理ip\)，，可以添加多个代理。

然后利用 build\_opener\(\) 方法利用这个 Handler 构造一个 Opener，然后发送请求即可。

## Cookies

获取相关网站的cookies

```text
import http.cookiejar,urllib.request

# 声明一个CookieJar对象
cookie = http.cookiejar.CookieJar()
# 构建一个handler
handler = urllib.request.HTTPCookieProcessor(cookie)
# 构建一个opener
opener = urllib.request.build_opener(handler)
# 打开网站
response = opener.open('http://www.baidu.com')
for item in cookie:
    print(item.name+"="+item.value)
```

运行结果如下:

```text
BAIDUID=6579690C07419CE00E162042A638AEAE:FG=1
BIDUPSID=6579690C07419CE00E162042A638AEAE
H_PS_PSSID=26524_1436_26909_21078_26925_20928
PSTM=1532934005
BDSVRTM=0
BD_HOME=0
delPer=0
```

将cookies存储为文本格式

实例:

```text
import urllib.request,http.cookiejar

filename = "cookies.txt"
# 如果存储为文本格式，需要用到MozillaCookieJar
cookies = http.cookiejar.MozillaCookieJar(filename)
# 构建一个handler
handler = urllib.request.HTTPCookieProcessor(cookies)
# 构建一个opener
opener = urllib.request.build_opener(handler)
response = opener.open("http://www.baidu.com")
cookies.save(ignore_discard=True,ignore_expires=True)
```

CookieJar需要换成 MozillaCookieJar，生成文件时需要用到它，它是 CookieJar 的子类，可以用来处理 Cookies 和文件相关的事件，读取和保存 Cookies，它可以将 Cookies 保存成 Mozilla 型浏览器的 Cookies 的格式。

运行之后会有一个cookies.txt文件生成，内容如下:

```text
# Netscape HTTP Cookie File
# http://curl.haxx.se/rfc/cookie_spec.html
# This is a generated file!  Do not edit.

.baidu.com    TRUE    /    FALSE    3680417901    BAIDUID    2DD475CE73FF8C93B7B1F0798D7A5426:FG=1
.baidu.com    TRUE    /    FALSE    3680417901    BIDUPSID    2DD475CE73FF8C93B7B1F0798D7A5426
.baidu.com    TRUE    /    FALSE        H_PS_PSSID    1420_21101_26350_26923_26809
.baidu.com    TRUE    /    FALSE    3680417901    PSTM    1532934257
www.baidu.com    FALSE    /    FALSE        BDSVRTM    0
www.baidu.com    FALSE    /    FALSE        BD_HOME    0
www.baidu.com    FALSE    /    FALSE    2479014200    delPer    0
```

另外还有一个 LWPCookieJar，同样可以读取和保存 Cookies，但是保存的格式和 MozillaCookieJar 的不一样，它会保存成与 libwww-perl\(LWP\) 的 Cookies 文件格式。

要保存成 LWP 格式的 Cookies 文件，可以在声明时就改为：

```text
cookie = http.cookiejar.LWPCookieJar(filename)
```

运行结果如下:

```text
#LWP-Cookies-2.0
Set-Cookie3: BAIDUID="16458736324AC0E3ECA4EECD48D8DC8C:FG=1"; path="/"; domain=".baidu.com"; path_spec; domain_dot; expires="2086-08-17 10:20:34Z"; version=0
Set-Cookie3: BIDUPSID=16458736324AC0E3ECA4EECD48D8DC8C; path="/"; domain=".baidu.com"; path_spec; domain_dot; expires="2086-08-17 10:20:34Z"; version=0
Set-Cookie3: H_PS_PSSID=1432_26458_21099_20930; path="/"; domain=".baidu.com"; path_spec; domain_dot; discard; version=0
Set-Cookie3: PSTM=1532934390; path="/"; domain=".baidu.com"; path_spec; domain_dot; expires="2086-08-17 10:20:34Z"; version=0
Set-Cookie3: BDSVRTM=0; path="/"; domain="www.baidu.com"; path_spec; discard; version=0
Set-Cookie3: BD_HOME=0; path="/"; domain="www.baidu.com"; path_spec; discard; version=0
Set-Cookie3: delPer=0; path="/"; domain="www.baidu.com"; expires="2048-07-22 07:05:45Z"; version=0
```

从cookies.txt读取存储的cookies

以LWPCookieJar为例:

```text
import urllib.request,http.cookiejar

cookies = http.cookiejar.LWPCookieJar()
cookies.load(filename='cookies.txt',ignore_expires=True,ignore_discard=True)
handler = urllib.request.HTTPCookieProcessor(cookies)
opener = urllib.request.build_opener(handler)
response = opener.open('http://www.baidu.com')
# print(response.read().decode('utf-8'))
for cookie in cookies:
    print(cookie)
```

利用load\(\)方法读取本地Cookies文件，获取到了cookies的内容

运行结果如下:

```text
<Cookie BAIDUID=16458736324AC0E3ECA4EECD48D8DC8C:FG=1 for .baidu.com/>
<Cookie BIDUPSID=16458736324AC0E3ECA4EECD48D8DC8C for .baidu.com/>
<Cookie H_PS_PSSID=1432_26458_21099_20930 for .baidu.com/>
<Cookie PSTM=1532934390 for .baidu.com/>
<Cookie BDSVRTM=0 for www.baidu.com/>
<Cookie BD_HOME=0 for www.baidu.com/>
<Cookie delPer=0 for www.baidu.com/>
```


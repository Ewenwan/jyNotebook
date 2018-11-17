# 2.4 会话和Cookies

Cookie:[https://xintiaohuiyi.gitbook.io/flask-note/5flaskzhi-shi-dian-bu-chong/flask-cookie](https://xintiaohuiyi.gitbook.io/flask-note/5flaskzhi-shi-dian-bu-chong/flask-cookie)

Session:[https://xintiaohuiyi.gitbook.io/flask-note/5flaskzhi-shi-dian-bu-chong/flask-session](https://xintiaohuiyi.gitbook.io/flask-note/5flaskzhi-shi-dian-bu-chong/flask-session)

cookie属性：

* Name，即该 Cookie 的名称。
* Value，即该 Cookie 的值。如果值为 Unicode 字符，需要为字符编码。如果值为二进制数据，则需要使用 BASE64 编码。
* Max Age，即该 Cookie 失效的时间，单位秒，也常和 Expires 一起使用，通过它可以计算出其有效时间。Max Age 如果为正数，则该Cookie 在 Max Age 秒之后失效。如果为负数，则关闭浏览器时Cookie 即失效，浏览器也不会以任何形式保存该 Cookie。
* Path，即该 Cookie 的使用路径。如果设置为 /path/，则只有路径为 /path/ 的页面可以访问该 Cookie。如果设置为 /，则本域名下的所有页面都可以访问该 Cookie。
* Domain，即可以访问该 Cookie 的域名。例如如果设置为 .zhihu.com，则所有以 zhihu.com，结尾的域名都可以访问该Cookie。
* Size字段，即此 Cookie 的大小。
* Http字段，即 Cookie 的 httponly 属性。若此属性为 true，则只有在 HTTP Headers 中会带有此 Cookie 的信息，而不能通过 document.cookie 来访问此 Cookie。
* Secure，即该 Cookie 是否仅被使用安全协议传输。安全协议。安全协议有 HTTPS，SSL 等，在网络上传输数据之前先将数据加密。默认为 false。


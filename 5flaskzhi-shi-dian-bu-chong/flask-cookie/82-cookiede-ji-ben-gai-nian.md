# 82 cookie的基本概念

## 什么是cookie?

cookie:在网站中，HTTP请求是无状态的。也就是第一次和服务器连接后并且登录成功后，第二次请求服务器依然不能知道请求的是哪个用户。cookie的出现是为了解决这个问题，第一次登录后服务器返回一些数据\(cookie\)给浏览器，然后浏览器保存在本地，当该用户发送第二次请求的时候，就会自动的把上次请求存储的cookie数据自动的携带给服务器，服务器通过浏览器携带的数据就能判断当前用户是哪个了。cookie存储的数据量有限，不同的浏览器有不同的存储大小，但一般不超过4kb，因此使用cookie只能存储一些小量的数据

* cookie有有效期，服务器可以设置cookie的有效期，以后浏览器会自动的清除过期的cookie
* cookie有域名的概念:只有访问同一个域名，才会把之前相同域名返回的cookie携带给服务器，也就是说，访问谷歌的时候，不会把百度的cookie发送给谷歌

```text
# secure设置为True只能在HTTPS协议下使用
# httponly设置为Truecookie只能被浏览器读取，不能被js读取
# expires无效日期
# max_age:以秒为单位，距离现在多久过期
set_cookie(self, key, value='',max_age=None, expires=None,path='/', domain=None,
secure=False, httponly=False,samesite=None)
```


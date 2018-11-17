# 2.4.3 常见误区

在谈论 Session 机制的时候，常常听到这样一种误解“只要关闭浏览器，Session 就消失了”，这种理解是错误的，可以想象一下会员卡的例子，除非顾客主动对店家提出销卡，否则店家绝对不会轻易删除顾客的资料。对 Session 来说也是一样的，除非程序通知服务器删除一个 Session，否则服务器会一直保留，比如程序一般都是在我们做注销操作的时候才去删除 Session。

但是当我们关闭浏览器时，浏览器不会主动在关闭之前通知服务器它将要关闭，所以服务器根本不会有机会知道浏览器已经关闭，之所以会有这种错觉，是大部分 Session 机制都使用会话 Cookie 来保存 Session ID 信息，而关闭浏览器后 Cookies 就消失了，再次连接服务器时也就无法找到原来的 Session。如果服务器设置的 Cookies 被保存到硬盘上，或者使用某种手段改写浏览器发出的 HTTP 请求头，把原来的 Cookies 发送给服务器，则再次打开浏览器仍然能够找到原来的 Session ID，依旧还是可以保持登录状态的。

而且恰恰是由于关闭浏览器不会导致 Session 被删除，这就需要服务器为 Seesion 设置一个失效时间，当距离客户端上一次使用 Session 的时间超过这个失效时间时，服务器就可以认为客户端已经停止了活动，才会把 Session 删除以节省存储空间。

## 参考资料 {#5-参考资料}

* Session 百度百科：[https://baike.baidu.com/item/session/479100](https://baike.baidu.com/item/session/479100)
* Cookie 百度百科：[https://baike.baidu.com/item/cookie/1119](https://baike.baidu.com/item/cookie/1119)
* HTTP Cookie 维基百科：[https://en.wikipedia.org/wiki/HTTP\_cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
* Session和几种状态保持方案理解：[http://www.mamicode.com/info-detail-46545.html](http://www.mamicode.com/info-detail-46545.html)
* 静觅:[https://germey.gitbooks.io/python3webspider/content/2.4-Session和Cookies.html](https://germey.gitbooks.io/python3webspider/content/2.4-Session和Cookies.html)


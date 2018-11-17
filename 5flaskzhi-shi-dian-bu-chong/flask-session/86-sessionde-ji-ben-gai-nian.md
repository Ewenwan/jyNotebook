# 86 session的基本概念

## 什么是session?

session:session和cookie的作用类似，都是为了存储用户相关的信息，不同的是，cookie是存储在本地浏览器，session是一个思路/概念，一个服务器存储授权信息的解决方案，不同的服务器，不同的框架，不同的语言有不同的实现，虽然实现不一样，但是他们的目的都是服务器为了方便存储数据的。session的出现，是为了解决cookie存储数据不安全的问题的

## cookie和session结合使用

由于随着web的开发，发展至今，一般有两种存储方式:

* 存储在服务端_**:**_通过cookie存储一个session\_id，然后具体的数据则是保存在session中。如果用户已经登录，则服务器会在cookie中保存一个session\_id，下次再次请求的时候，会把session\_id携带上来，服务器根据session\_id在session库中获取用户的session数据，就能知道该用户到底是谁，以及之前保存的一些状态信息。这种专业术语叫做server side session。存储在服务器的数据会更加的安全，不容易被窃取。但存储在服务器也有一定的弊端，就是会占用服务器的资源，但现在服务器以及发展至今，一些session信息还是可以存储的
* 将session数据加密，然后存储在cookie中。这种专业术语叫做client side session。flask采用的就是这种方式，但是也可以替换成其他形式


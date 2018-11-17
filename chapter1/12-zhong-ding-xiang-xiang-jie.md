## 关于响应

### 视图函数的返回值会被自动转换为一个响应对象，flask的转换逻辑如下:

* 如果返回的是一个合法的响应对象，则直接返回

* 如果返回的是一个字符串，那么Flask会重新创建一个werkzeug.wrappers.Response对象，Response将该字符串作为主体，状态码是200，MIME类型为text/html，然后返回该Response对象

* .如果返回的是一个元祖，元祖中的数据类型是\(reponse.status.headers。status值会覆盖默认的200状态码，headers可以是一个列表或者字典，作为额外的消息头

* 如果以上条件都不满足，Flask会假设返回值是一个合法的wsgi 应用程序，并通过Response.force\_type\(rv,request.environ\)转换为一个请求对象

### 自定义响应。自定义响应必须满足三个条件:

* 必须继承自Response类

* 必须实现类方法force\_type\(cls,rv,environ=None\)

* 必须制定app.response\_class为你自定义的Response

## response笔记

### 视图函数中可以返回那些值

1.可以返回字符串:返回的字符串其实是底层将这个字符串包装成了一个'Response'对象

2.可以返回元组：元组的形式是\(响应体，状态码，头部信息，返回的元组在底层包装成了一个'Response'对象\)

3.可以返回'Response'及其子类。

### 实现一个自定义的Response对象:

1.继承'Response'类

2.实现方法'force\_type\(cls,rv,envison=None\)'

3.指定'app.reponse\_class'为你自定义的'Response'对象

4.如果视图返回的数据，不是字符串，也不是元组，也不是Response，那么就会将返回值传给'focre\_type'，然后'force\_type'的返回值返回给前端


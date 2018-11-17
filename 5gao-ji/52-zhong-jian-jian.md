## 中间件

* 是一个轻量级、底层的插件系统，可以介入Django的请求和响应处理过程，修改Django的输入或输出
* 激活:添加到django配置文件中的MIDDLEWARE\_CLASSES元祖中
* 每个中间件组件是一个独立的python类，可以定义下面方法中的一个或多个
  * \_\__int_\_\_:无序任何参数，服务器响应第一个请求的时候调用一次，用于确定是否启用当前中间件
  * process\_request\(request\):执行视图之前被调用，每个请求上调用，返回None或HttpResponse对象
  * process\__view\(request,view_func,view_args,views_kwargs\):调用视图之前被调用，在每个请求上调用，返回None或HttpResponse对象
  * process\__template\_response\(request,response\):_在视图刚好执行完毕之后被调用，在每个请求上调用，返回实现了render方法的响应对象
  * process\_response\(request,response\):所有响应返回浏览器之前被调用，在每个请求上调用，返回HttpResponse对象
  * process\_exception\(request,respone,exception\):当视图抛出异常时调用，在每个请求上调用，返回一个HttpResponse对象
* 使用中间件,可以干扰整个处理过程，每次请求中都会执行中间件的这个方法
* 示例:获取参数
* 与settings.py同级目录下创建

```
from django.http import HttpResponse
from django.utils.deprecation import MiddlewareMixin

class myMiddle(MiddlewareMixin):

    def process_exception(self,request,response,exception):
        return HttpResponse(exception.message)

    def process_request(self,request):
        print('get参数为',request.GET.get('a'))
```

* 将类myMiddle注册到settings.py文件中

```

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'middleware.myApp.myMiddle.MyMiddle',
]
```

* 执行视图之前被调用，每个请求上调用，会返回一个参数值或None




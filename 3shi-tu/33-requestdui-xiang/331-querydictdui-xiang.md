## QueryDict对象

* 定义在django.http.QueryDict
* request对象的属性GET、POST都是QueryDict类型对象
* 与python字典不同，QueryDict类型的对象用来处理同一个键带有多个值的情况
* 方法get\(\):根据键获取值
  * 只能获取键的一个值
  * 如果一个键同时拥有多个值，获取最后一个值

```
dict.get("键",default)
或简写为
dict['键']
```

* 方法getlist\(\):根据键获取值
  * 将键的值以列表返回，可以获取一个键的多个值

```
dict.getlist("键",default)
```

```
配置路由urls.py:

"""
url(r'^test/$',views.querydict),
"""

views.py:

def querydict(request):
    a = request.GET.getlist('a')
    print(a)
    a1 = a[0]
    a2 = a[1]
    b = request.GET.get('b')
    print(b)
    return HttpResponse(a1+ " " + a2 + " " + b)
    
测试网址:http://localhost:8000/test/?a=1&a=2&b=2

值:1 2 2
```




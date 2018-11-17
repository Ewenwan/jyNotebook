## 缓存

* 缓存数据就是为了保存需要计算资源的结果，这样的话就不必在下次重复消耗计算资源
* Django自带了一个健壮的缓存系统来保存动态页面，避免对于每次请求都重新计算
* Django提供了不同级别的缓存粒度，可以缓存特定视图的输出，可以仅仅缓存哪些很难生产出来的部分、或者可以缓存整个网站

---

### 设置缓存

* 通过设置决定把数据缓存在哪里，是数据中，文件系统，还是内存中
* 通过设置settings文件的CACHES配置来实现
* 参数TIMEOUT:缓存的默认过期时间，以秒为单位，这个参数默认是300秒，即5翻照片那个;设置TIMEOUT为None表示永远不会过期，值设置成0造成缓存立即失效

```
# 本地缓存
CACHES = {
    'default':{
        'BACKEND':'django.core.cache.backends.locmem.LocMemCache',
        'TIMEOUT':60,
    }
}
```

* MemcachedCache

```
缓存包:pip install python-memcached    pip install pylibmc

# 缓存
CACHES = {
    'default':{
        'BACKEND':'django.core.cache.backends.loca.MemcachedCache',
        #'BACKEND':'django.core.backends.memcached.PyLibMCCache'
        'TIMEOUT':60,
        'LOCATION':'127.0.0.1:11211',
    }
}



在此示例中，高速缓存通过在IP地址172.19.26.240和172.19.26.242上运行的Memcached实例共享，这两个实例都位于端口11211上：
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
        'LOCATION': [
            '172.19.26.240:11211',
            '172.19.26.242:11211',
        ]
    }
}
```

* 可以将cache存到redis中，默认采用1数据库，需要安装包并配置如下:

```
安装包:pip install django-redis-cache

# 缓存
CACHES = {
    'default':{
        'BACKEND':'redis_cache.cache.RedisCache',
        #'BACKEND':'django.core.backends.memcached.PyLibMCCache'
        'TIMEOUT':60,
        'LOVATION':'localhost:6379',
    }
}
```

* 连接redis，查看存储的数据

```
开启redis服务:net start reids
连接:redis-cli
切换数据库:select 1
查看键:keys *
查看值:get 键
```

![](/assets/redis-cli.png)

---

### 单个view缓存

* django.views.decorators.cache定义了cache\_page装饰器，用于对视图的输出进行缓存
* 示例代码

```
urls.py
# 配置路由
urlpatterns = [
    path('cache/<int:code>/',views.cache),
]

views.py
#创建视图
@cache_page(60 * 15)
def cache(request,code):
    # return render(request,'html/cache.html')
    return HttpResponse("hello world")
```

* cache\_page:timeout参数，缓存超时，以秒为单位，上述实体，cache视图的结果将被缓存15分钟
* 视图缓存与URL无关，如果多个URL指向同一视图，每个URL将会分别缓存

---

### 模板片段缓存

* 使用cache模板标签来缓存模板的一个片段
* 需要两个参数:
  * 缓存时间，以秒为单位
  * 给缓存片段起的名称
* 示例:

```
{% load cache %}
{% cache 500 hello %}
    hello world
{% endcache %}
```

---

### 底层的缓存api

```
views.py
#缓存视图

from django.core.cache import cache
from django.core.cache.utils import  make_template_fragment_key

def cachesettings(request):

    cache.set('name', 'angle', 60*30)
    print(cache.get('name'))
    # cache.delete('name')
    # cache.clear()
    return render(request,'html/test.html')


urls.py
#配置路由

url(r'^test/$',views.cachesettings)
```

```
from django.core.cache import cache

设置：cache.set(键,值,有效时间)
获取：cache.get(键)
删除：cache.delete(键)
清空：cache.clear()
设置多个值:cache.set_many({'a':1,'b':2})
获取多个值:cache.get_cache(['a','b','c'])
删除多个值:cache.delete_many(['a','b'])
递增:cache.incr('num')
递减:cache.decr('num')
关闭连接:cache.close()
```




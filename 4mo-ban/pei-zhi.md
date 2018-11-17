![](/assets/peizhi1.png)

在templates下创建urls.py

```
from django.conf.urls import url,include
from . import views
app_name = 'myapp'
urlpatterns = [
    url(r'^index/$',views.index),
]
```

在主urls下配置

```

urlpatterns = [
    path('admin/', admin.site.urls),
    url(r'',include('myapp.urls',namespace='myapp')),
]

```

配置settings.py

```
LANGUAGE_CODE = 'zh-Hans'

TIME_ZONE = 'Asia/Shanghai'



TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR,'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]



INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp'
]
```




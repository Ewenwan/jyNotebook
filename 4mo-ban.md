## 模板介绍

* 作为web框架，Django提供了模板，可以很便利的动态生成HTML
* 模板系统致力于表达外观，而不是程序逻辑
* 模板的设计实现了业务逻辑\(view\)与显示内容\(template\)的分离，一个视图可以使用任意一个模板
* 模板包含
  * HTML的静态部分
  * 动态插入内容部分
* django模板语言，简写DTL，定义在django.template包中
* 由startproject命令生成的settings.py定义关于模板的值:
  * DIRS定义了目录列表，模板引擎按列表顺序搜索这些目录一查找木本源文件
  * APP\_DIRS告诉模板引擎是否应该在每个已安装的应用中查找模板
* 常用方式:在项目的根目录下创建templates目录，设置DIRS值

```
'DIRS': [os.path.join(BASE_DIR,'templates')],
```

---

## 模板处理

* Django处理模板分为两个阶段
* 加载:根据给定的标识找到模板然后预处理李，通常会将它编译好放在内存中

```
loader.get_template(template_name),返回一个Template对象
```

* 渲染:使用Context数据对模板插值并返回生成的字符串

  ```
  Template对象的render(RequestContext)方法，使用context渲染模板
  ```

  * 加载渲染完整代码：

  ```
  from django.template import loader, RequestContext
  from django.http import HttpResponse

  def index(request):
      tem = loader.get_template('temtest/index.html')
      context = {}
      return HttpResponse(tem.render(context，request))
  ```

---

## 快捷函数

* 为了减少加载模板，渲染模板的重复代码，django提供了快捷函数
* render\__to\_string\(""\)_
* render\(request,'模板',context\)

```
from django.shortcuts import render
from django.shortcuts import  *

# Create your views here.

def index(request):
    context = {'hello':'hello world'}
    return render(request,'myapp/index.html',context)
```




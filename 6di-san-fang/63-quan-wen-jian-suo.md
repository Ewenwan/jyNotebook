# 全文检索 {#全文检索}

* 全文检索不同于特定字段的模糊查询，使用全文检索的效率更高，并且能够对于中文进行分词处理
* haystack：django的一个包，可以方便地对model里面的内容进行索引、搜索，设计为支持whoosh,solr,Xapian,Elasticsearc四种全文检索引擎后端，属于一种全文检索的框架
* whoosh：纯Python编写的全文搜索引擎，虽然性能比不上sphinx、xapian、Elasticsearc等
* jieba：一款免费的中文分词包

---

### 操作

#### 1.安装所需包

```
pip install django-haystack
pip install whoosh
pip install jieba
```

#### 2.修改settings.py文件

* 添加应用

```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
    'tinymce',
    'haystack',
]
```

* 添加搜索引擎

```
# 添加搜索引擎
HAYSTACK_CONNECTIONS = {
    'default': {
        'ENGINE': 'haystack.backends.whoosh_cn_backend.WhooshEngine',
        'PATH': os.path.join(BASE_DIR, 'whoosh_index'),
    }
}

#自动生成索引
HAYSTACK_SIGNAL_PROCESSOR = 'haystack.signals.RealtimeSignalProcessor'
```

#### 3.在项目的urls.py中添加url

```
urlpatterns = [
    ....
    url(r'^search/$',include('haystack.urls')),
]
```

##### 4.在应用目录myapp下奖励search\_indexes.py文件

```
from haystack import indexes
from .models import Grades

class GradesIndex(indexes.SearchIndex,indexes.Indexable):
    text = indexes.CharField(document=True,use_template=True)

    def get_model(self):
        return Grades

    def index_queryset(self, using=None):
        return self.get_model().objects.all()
```

#### 5.在目录“templates/search/indexes/应用名称”下创建"模型类名称\_text"文件

```
# grades_text.txt,列出要对那些内容进行检索


{{object.gname}}
{{object.gdate}}
```

#### 6.在目录"templates/search"下创建search.html

```
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
{% if query %}
    <h3>搜索结果如下：</h3>
    {% for result in page.object_list %}
        <a href="/{{ result.object.id }}/">{{ result.object.sname }}</a><br/>
    {% empty %}
        <p>啥也没找到</p>
    {% endfor %}

    {% if page.has_previous or page.has_next %}
        <div>
            {% if page.has_previous %}<a href="?q={{ query }}&amp;page={{ page.previous_page_number }}">{% endif %}&laquo; 上一页{% if page.has_previous %}</a>{% endif %}
        |
            {% if page.has_next %}<a href="?q={{ query }}&amp;page={{ page.next_page_number }}">{% endif %}下一页 &raquo;{% if page.has_next %}</a>{% endif %}
        </div>
    {% endif %}
{% endif %}
</body>
</html>
```

#### 7.建立ChineseAnalyzer.py文件

* 在python路径里，保存在haystack的安装文件夹下,路径如:"/lib/site-packages/haystack/backends"

```
import jieba
from whoosh.analysis import Tokenizer, Token


class ChineseTokenizer(Tokenizer):
    def __call__(self, value, positions=False, chars=False,
                 keeporiginal=False, removestops=True,
                 start_pos=0, start_char=0, mode='', **kwargs):
        t = Token(positions, chars, removestops=removestops, mode=mode,
                  **kwargs)
        seglist = jieba.cut(value, cut_all=True)
        for w in seglist:
            t.original = t.text = w
            t.boost = 1.0
            if positions:
                t.pos = start_pos + value.find(w)
            if chars:
                t.startchar = start_char + value.find(w)
                t.endchar = start_char + value.find(w) + len(w)
            yield t


def ChineseAnalyzer():
    return ChineseTokenizer()
```

#### 8.复制whoosh\_backend.py文件，改名为whoosh\_cn\_backend.py {#8复制whooshbackendpy文件，改名为whooshcnbackendpy}

* 注意：复制出来的文件名，末尾会有一个空格，记得要删除这个空格

```
from .ChineseAnalyzer import ChineseAnalyzer 
查找
analyzer=StemmingAnalyzer()
改为
analyzer=ChineseAnalyzer()

```

#### 9.生成索引 {#9生成索引}

* 初始化索引数据

```
python manage.py rebuild_index

```

#### 10.在模板中创建搜索栏 {#10在模板中创建搜索栏}

```
<form method='get' action="/search/" target="_blank">
    <input type="text" name="q">
    <input type="submit" value="查询">
</form>
```




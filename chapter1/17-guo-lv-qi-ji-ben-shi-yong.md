## Jinja2模板过滤器

网址：[http://jinja.pocoo.org/docs/2.10/](http://jinja.pocoo.org/docs/2.10/)  
[http://jinja.pocoo.org/docs/2.10/templates/\#builtin-filters](http://jinja.pocoo.org/docs/2.10/templates/#builtin-filters)

过滤器是通过管道符号\(\|\)进行使用的，例如:\(\(name\|length\)\),将返回name的长度。过滤器相当于是一个函数，把当前的变量传入到过滤器中，然后过滤器根据自己的功能，再返回响应的值，之后再将结果渲染到页面中。

Jinja2中内置了许多过滤器，在这里可以看到所有的过滤器，现对一些常用的过滤器进行讲解:

* abs\(value\):返回一个数值的绝对值。例如:-1\|abs。

* default\(value,default\_value,boolean=false\):如果当前变量没有值，则会使用参数中的值来代替。  
  name\|default\('xiaotuo'\) == 如果name不存在，则会使用xiaotuo来代替。boolean=False默认是在只  
  有这个变量为undefined的时候才会使用default中的值，如果想使用python的形式判断是否为false，则可以传递Boolean=true。也可以使用or来代替

* escape\(value\)或e:转义字符,会将等符号转义成HTML中的符号。例如content\|escape或content\|e

* first\(value\):返回一个序列的第一个元素。name\|first

* format\(value,\*args,\*\*kwargs\):格式化字符串。

* last\(value\):返回一个序列的最后一个元素。示例:names\|last。

* length\(value\):返回一个序列或者字典的长度。示例:names\|length

* join\(value,d='u'\):将一个序列用d这个参数的值拼接成字符串

* safe\(value\):如果开启了全局转义，那么safe过滤器会将变量关掉转义。示例:content\_html\|safe

* int\(value\):将值转换为int类型

* float\(value\):将值转换为float类型

* lower\(value\):将字符串转换为小写

* upper\(value\):将字符串转换为大写

* replace\(value,old,new\):替换将old替换为new的字符串

* truncate\(value,length=253,killwords=False\):截取length长度的字符串

* striptags\(value\):删除字符串中所有的HTML标签，如果出现多个空格，将替换成一个空格

* trim:截取字符串前面和后面的空白字符

* string\(value\):将变量转换成字符串

* wordcount\(s\):计算一个长字符串中单词的个数

```
from datetime import datetime
from flask import Flask, render_template, url_for

app = Flask(__name__)
app.config["TEMPLATES_AUTO_RELOAD"] = True

# @app.route("/")
# def hello_world():
#     return render_template("index.html",position="-5")

@app.route("/")
def index():
    context = {
        'position':-9,
        'signature':'<script>alert("hello")</script>',
        # 'signature': None,
        'article':'hello world',
        'persons':[1,2,3],
        'age':18,
        # 'create_time':datetime.datetime.now(),
        'create_time':datetime(2018,4,27,23,14,0),
    }
    signature = None
    a = signature or '默认值'
    # return render_template('index.html',position="-9")
    return render_template('index.html', **context)

# 自定义过滤器
@app.template_filter('my_cut')
def cut(value):
    # replace(oldstring,newstring)
    value = value.replace("hello","")
    return value

@app.template_filter('handle_time')
def handle_time(time):
    """
    time 距离现在的时间是多少
    如果时间间隔小于1分钟以内，那么就显示'刚刚'
    如果是大于1分钟小于等于1小时以内，那么就显示'xx分钟前'
    如果是大于1小时小于等于24小时内，那么就显示'xx小时前'
    如果大于24小时小于30天以内，那么就显示'xx天前'
    否则就是具体时间:例2017年10月20日
    :param time:
    :return:
    """
    if isinstance(time,datetime):
        now = datetime.now()
        # 两个时间相减，得到描述
        timestamp = (now - time).total_seconds()
        if timestamp < 60:
            return '刚刚'
        elif timestamp < 60*60 and timestamp >= 60:
            minutes = timestamp/60
            return "%s 分钟前" % int(minutes)
        elif timestamp >= 60*60 and timestamp < 60*60*24:
            hours = timestamp/(60*60)
            return  "%s 小时前" % int(hours)
        elif timestamp>= 60*60*24 and timestamp < 60*60*24*30:
            days = timestamp / (60*60*24)
            return "%s 天前" % int(days)
        else:
            return time.strftime('%Y/%m/%d %H:%M')
    else:
        return time

if __name__ == '__main__':
    app.run(debug=True)
```

```
index.html


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>miku</title>
</head>
<body>
{#     <p>position:{{ position }}</p>#}
{#     <p>个数:{{ position|wordcount }}</p>#}
     <p>----------------------------</p>
     <p>signature:{{ signature|default("Angle","boolean") }}</p>
     <p>signature:{{ signature|default("Angle",boolean=True) }}</p>
     <p>{{ signature }}</p>
     <p>{{ signature or 'angle' }}</p>
     <p>----------------</p>
{#     <p>{{ article|my_cut }}</p> #}
     <p>{{ article }}</p>
     <p>-----------------</p>
     <div>
       {#% autoescape off % #}
         <!--禁止转义-->
            <p>个性签名:{{ signature|escape}}</p>
            <!--转义-->
            <p>个性签名:{{ signature|safe}}</p>
       {#% endautoescape % #}
         <p>---------------</p>
         {{ "%s"|format(signature) }}
         {{ persons|length }}
         <p>----------</p>
         {% if age|int == 18 %}
            <p>成年</p>
         {% else %}
            <p>未成年</p>
         {% endif %}
     # 去掉HTML元素标签
     <p>{{ signature|striptags }}</p>
     </div>
     <p>发表时间:{{ create_time|handle_time }}</p>
</body>
</html>
```






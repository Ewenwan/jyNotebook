# 21 自定义时间处理过滤器案例

```text
from flask import Flask,render_template
from datetime import datetime

app = Flask(__name__)
app.config['TEMPLATES_AUTO_RELOAD'] = True

# @app.route('/')
# def hello_world():
#     return render_template('index.html',position="-9")

@app.route('/')
def index():
    context = {
        'position':-9,
        # 'signature':None,
        'signature': 1,
        'article':'hello zhiliao world hello',
        # 'create_time':datetime.now(),
        'create_time': datetime(2018,4,27,23,14,0),
    }
    signature = 1
    a = signature or '默认值'
    return render_template('index.html',**context)

# 指定一个名字
@app.template_filter('my_cut')
def cut(value):
    value = value.replace("hello",'')
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






****************************************************

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>MIKU</title>
</head>
<body>
{#    <p>位置的绝对值是:{{ position }}</p>#}
{#    <p>位置的绝对值是:{{ position|wordcount }}</p>#}
{#    <p>个性签名:{{ signature|default('Angle','boolean')}}</p>#}
{#    <p>个性签名:{{ signature|default('Angle',boolean=True)}}</p>#}
{#    <p>个性签名：{{ signature or 'angle'}}</p>#}
{#    <p>{{ article|my_cut }}</p>#}
{#    <p>{{ article}}</p>#}
    <p>发表时间:{{ create_time|handle_time }}</p>
</body>
</html>
```


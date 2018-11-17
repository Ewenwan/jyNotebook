#### 'for ... in ...':'for'循环可以遍历任何一个序列包括列表、字典、元祖，并且可以进行反向遍历

##### 普通的遍历

```
<ul>
{% for user in users %}
<li>{{user.username|e}}</li>
{% endfor %}
</ul>
```

##### 遍历字典:

```
<dl>
    {% for key,value in my_dict_iteritems() %}
    <dt>{{key|e}}</dt>
    <dd>{{value|e}}</dd>
    {% endfor %}
</dl>
```

#### 并且'Jinja2'中的'for'循环还包含以下遍历，可以用来获取当前的遍历状态:

loop.index:当前迭代的索引\(从i开始\)

loop.index0:当前迭代的索引\(从0开始\)

loop.first:是否是第一次迭代，返回True或者False

loop.last:是否是最后一次迭代，返回True或者False

loop.length:序列的长度

另外，不可以使用'continue'和'break'表达式来控制循环的执行

```
index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <ul>
        {% for user in users|reverse %}
            <li>{{ user }}</li>
        {% else %}
            <li>没有任何值</li>
        {% endfor %}
    </ul>

    <!-- table:表格 thead:表头 tr:行 th,td:列 tbody：主体 -->
    <table>
        <thead>
            <tr>
                <th>用户名</th>
                <th>年龄</th>
                <th>花</th>
            </tr>
        </thead>
        <tbody>
            <tr>
{#                <td>{{ person.username }}</td>#}
{#                <td>{{ person.age }}</td>#}
{#                <td>{{ person.flower }}</td>#}
{#                {% for value in person.values() %}#}
{#                {% for key,value in person.items() %}#}
                {% for key in person.keys() %}
{#                    <td>{{ value }}</td>#}
                    <td>{{ key }}</td>
                {% endfor %}


            </tr>
        </tbody>
    </table>


    <table>
        <thead>
            <tr>
                <th>书名</th>
                <th>作者</th>
                <th>价格</th>
            </tr>
        </thead>
        <tbody>
            {% for book in books %}
                {% if loop.first %}
                    <tr style="background: red;">
                {% elif loop.last %}
                    <tr style="background: pink;">
                {% else %}
                    <tr>
                {% endif %}
                    <td>{{ loop.index0 }}</td>
                    <td>{{ book.name }}</td>
                    <td>{{ book.author }}</td>
                    <td>{{ book.price }}</td>
                    <td>{{ loop.length }}</td>
                </tr>
            {% endfor %}
        </tbody>
    </table>

    <table border="1">
        <tbody>
            {% for i in range(1,10) %}
                <tr>
                    {% for j in range(1,i+1) %}
                        <td>{{ j }}*{{ i }}={{ i*j }}</td>
                    {% endfor %}
                </tr>
            {% endfor %}
        </tbody>
    </table>
</body>
</html>
```

```
from flask import Flask,render_template

app = Flask(__name__)


@app.route('/')
def index():

    context = {
        'users':['miku1','miku2','miku3'],
        # 'users':[],
        'person':{
            'username':'miku',
            'age':15,
            'flower':'1',
        },
        'books':[
            {
                'name':'miku1',
                'author':'angle1',
                'price':111,
            },
            {
                'name': 'miku2',
                'author': 'angle2',
                'price': 112,
            },
            {
                'name': 'miku3',
                'author': 'angle3',
                'price': 113,
            },
            {
                'name': 'miku4',
                'author': 'angle4',
                'price': 114,
            },
        ]
    }
    # keys(),values(),items() --> iter
    return render_template("index.html",**context)


if __name__ == '__main__':
    app.run(debug=True)
```




## 模板-参数

1. 在使用"render\_template"渲染模板的时候，可以传递参数u，以后直接在模板中使用就可以了
2. 如果参数过多，可以将所有的字典放到一个字典中，然后在传入这个字典参数的时候，使用两个星号，将字典打散成关键参数

   from flask import Flask, Response, jsonify, render\_template  
    app = Flask\(name\)  
    @app.route\("/"\)  
    def hell0\_world\(\):  
    context = {  
        "username":"miku",  
        "age":18,  
        "contry":"china",  
        "childrens":{  
            "name":"abc",  
            "height":180,  
        }  
    }

   return render\_template\("index.html",\*\*context\)  
    if name == 'main':  
        app.run\(debug=True\)



```
index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>MIKU</title>
</head>
<body>
    这是从模板中渲染的数据
{#    <p>{{ context.username }}</p>#}
{#    <p>{{ context.age }}</p>#}
{#    <p>{{ context.contry }}</p>#}

    <p>{{ username }}</p>
    <p>{{ age }}</p>
    <p>{{ contry }}</p>
    <p>{{ childrens }}</p>
    <p>{{ childrens.name }}</p>
    <p>{{ childrens['name'] }}</p>
</body>
</html>
```




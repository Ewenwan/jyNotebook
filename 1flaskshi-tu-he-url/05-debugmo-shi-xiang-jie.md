# 05 debug模式详解

## 为什么需要开启debug模式:

1.如果开启了DEBUG模式，那么在代码中如果抛出了异常，在浏览器的页面中可以看到具体的错误信息，以及具体的错误代码位置，方便开发者调试

2.如果开启了debug模式，那么以后在python代码中修改了任何代码，只要按"ctrl+s"，'flask'就会自动的重新记载整个网站，不需要手动点击重新运行。

## 配置debug模型的四种方式

1.在'app.run\(\)'中传递一个参数'debug=True'就可以开启'DEBUG'模式

1.1.app.run\(debug=True\)

2.给'app.debug=True'也可以开启'debug'模式

2.1.app.debug = True

3.通过配置参数的形式设置DEBUG模式,'app.config.update\(DEBUG=True\)'

3.1.app.config.update\(DEBUG=True\)

4.通过配置文件的形式设置DEBUG模式:'app.config.from\_object\(config\)'

## PING码

如果想要在网页上调试代码，name应该输入'PIN'码

```text
from flask import Flask, config

app = Flask(__name__)
# app.debug = True
# 设置配置参数的形式
# DEBUG必须要大写，不能小写

# app.config.from_object(config)
app.config.update(DEBUG=True)
# print(isinstance(app.config.dict))

@app.route('/')
def hello_world():
    return 'Hello World!'


if __name__ == '__main__':
    # app.run(debug=True)
    app.run()
```


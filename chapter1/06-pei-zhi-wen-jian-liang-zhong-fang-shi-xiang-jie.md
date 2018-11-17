## config配置笔记

### 使用"app.config.from\_object\(config\)"的方式加载配置文件

1. 导入"import config"
2. 使用"app.config.from\_object\(config\)"

### 使用“app.config.from\_pyfile”的方式加载配置文件

app.config.from\_pyfile\("config.py"\)

app.config.from\_pyfile\("config.py"\)

```
## config.py/config.txt

DEBUG = True
```

app.config.from\_pyfile\("config.txt",silent=False\)

silent=False如果不存在，则会报错

silent=True，如果文件不存在，则不会报错


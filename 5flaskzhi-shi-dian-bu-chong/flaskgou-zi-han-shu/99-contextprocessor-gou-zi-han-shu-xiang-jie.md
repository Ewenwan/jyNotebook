# 99 context\_processor钩子函数详解

context\_processor:上下处理器。返回的字典中的键可以在模板上下文中使用

```text
@app.context_processor
def context_processor():
    # return {"current_user":"angle"}
    if hasattr(g,'user'):
        return {'current_user':'angle'}
    else:
        return {"current_user":None}

{{current_user}}
```


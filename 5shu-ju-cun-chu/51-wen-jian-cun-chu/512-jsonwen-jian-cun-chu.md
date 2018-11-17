### 1.说明

Json，全称为JavaScript Object Notation，即JavaScript对象标记

json格式:

```
[{
    "name": "Bob",
    "gender": "male",
    "birthday": "1992-10-18"
}, {
     "name": "Selina",
    "gender": "female",
    "birthday": "1995-10-18"
}]
```

### 2.读取Json

通过json库实现对json文件的读写操作，调用json库的loads\(\)方法将Json文本字符串转为Json对象，可以通过dumps\(\)方法将Json对象转为文本字符串

实例:

```
import json

content = """
            [{
                "name": "Bob",
                "gender": "male",
                "birthday": "1992-10-18"
            }, {
                "name": "Selina",
                "gender": "female",
                "birthday": "1995-10-18"
            }]
        """
print(type(content))
content = json.loads(content)
print(type(content))
print(content)
```

运行结果:

```
<class 'str'>
<class 'dict'>
[{'name': 'Bob', 'gender': 'male', 'birthday': '1992-10-18'}, {'name': 'Selina', 'gender': 'female', 'birthday': '1995-10-18'}]
```

注意: Json 的数据需要用双引号来包围，不能使用单引号，不然会抛出如下错误

```
json.decoder.JSONDecodeError: Expecting property name enclosed in double quotes: line 3 column 5 (char 8)
```

从json文本中读取内容

```
import json

with open('test.json','r') as f:
    content = f.read()
    content = json.loads(content)
    print(content)
```

运行结果:

```
[{'name': 'Bob', 'gender': 'male', 'birthday': '1992-10-18'}, {'name': 'Selina', 'gender': 'female', 'birthday': '1995-10-18'}]
```

### 3.输出json

利用dumps\(\)方法将json对象转化为字符串，然后使用write\(\)方法写入文本中

```
import json

content = [{
        'name': 'Bob',
        'gender': 'male',
        'birthday': '1992-10-18'
}]
with open('test2.json','w') as f:
    f.write(json.dumps(content))
```

如果json中包含中文字符，为了保证输出正文，需要指定一个参数ensure\_ascii=False，另外还需要指定文件输出的编码

```
import json

content = [{
        'name': '天使',
        'gender': '女',
        'birthday': '1992-10-18'
}]
with open('test2.json','w',encoding='utf-8') as f:
    f.write(json.dumps(content,ensure_ascii=False,indent=2))

```




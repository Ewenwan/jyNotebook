### 1.说明

CSV，全称叫做Comma-Separated Values，即逗号分隔符或字符分隔符

### 2.写入

通过open\(\)方法写入并创建一个csv文件，调用csv库的writer\(\)方法初始化一个写入对象，传入该语柄，然后调用writerow\(\)方法传入每行的数据即可完成写入

```
import csv

with open('data.csv', 'w',newline='') as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(['id', 'name'])
    writer.writerow(['10001', '米库'])
```

注意:如果不带newline=‘’，会发现也能写入结果，但是每行内容之间总是会多出一个空行

如果想修改列与列之间的分隔符可以传入delimiter参数

```
import csv

with open('data.csv', 'w',newline='') as csvfile:
    writer = csv.writer(csvfile,delimiter='0')
    writer.writerow(['id', 'name'])
    writer.writerow(['10001', '米库'])
```

默认的分隔符逗号\(,\)会被换成delimeter参数设置的分隔符

可以同时传入多行，需要使用witerrows\(\)方法

注意:是writerrows而不是writerow

```
import csv

with open('data.csv', 'w',newline='') as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(['id', 'name'])
    writer.writerows([['10001', '米库'],['10001', '米库'],['10001', '米库']])
```

以字典的形式写入csv文件

```
import csv

with open('data.csv', 'w',newline='') as csvfile:
    # 预先定义字段
    fieldnames = ['id','name']
    # 初始化一个字典写入对象
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    # 调用writeheader()方法先写入头信息
    writer.writeheader()
    # 调用writerow传入相应字典
    writer.writerow({'id':1,"name":"angle"})
```

追加csv文本内容

注意这里就不同调用writeheader\(\)方法，不然会将头部信息一并写入

```
import csv

with open('data.csv', 'a',newline='') as csvfile:
    # 预先定义字段
    fieldnames = ['id','name']
    # 初始化一个字典写入对象
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    # 调用writerow传入相应字典
    writer.writerow({'id':1,"name":"angle"})
```

若将中文写入csv文件中，需要指定编码格式

```
import csv

with open('data.csv', 'a',newline=''，encoding='utf-8') as csvfile:
    # 预先定义字段
    fieldnames = ['id','name']
    # 初始化一个字典写入对象
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    # 调用writerow传入相应字典
    writer.writerow({'id':1,"name":"angle"})
```

利用pandas库写入csv文件

注意，字典的键值对中值的类型是列表形式

```
import pandas as pd

data = {
    'name':["angle"],
    "age":[18],
}
print(data)
df = pd.DataFrame(data)
# print(df)
df.to_csv('csv1.csv')
```

### 3.读取

```
import csv

with open('data.csv','r',encoding='utf-8') as csvfile:
    reader = csv.reader(csvfile)
    for content in reader:
        print(content)
```

运行结果:

```
['id', 'name']
['1', 'angle']
['id', 'name']
['1', 'angle']
['id', 'name']
```

利用pandas中read\_csv\(\)方法将数据从csv中读取出来

```
import csv
with open('data.csv', 'w',newline='',encoding='utf-8') as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(['id', 'name'])
    writer.writerows([['10001', '米库'],['10001', '米库'],['10001', '米库']])


# 用pandas读取csv文本内容，需要写入csv文本后时指定编码格式utf-8

import pandas as pd

print(pd.read_csv('data.csv'))
```

运行结果:

```
      id name
0  10001   米库
1  10001   米库
2  10001   米库
```




### 1.实例

利用open\(\)方法打开一个文本文件，并获取一个文件操作的对象

```
import requests
from pyquery import PyQuery as pq

url = "https://www.zhihu.com/explore"
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36'
}
response = requests.get(url,headers=headers)
content = response.text
# pq解析
doc = pq(content)
items = doc('.explore-tab .feed-item').items()
for item in items:
    question = item('.question_link').text()
    author = item('.avatar-link').text()
    answer = pq(item.find('.content').html()).text()
    with open('explore.txt','a',encoding='utf-8') as f:
        f.write('\n'.join([question,author,answer]))
        f.write('\n'+'='*50+'\n')
```

### 2.打开方式

```
r:以只读方式打开文件
rb:以二进制格式打开文件用于只读
r+:以读写方式打开
rb+:以二进制方式打开并读写文件
w:以只写方式打开文件，如果文件已存在则会被覆盖，不存在则会新建一个文件
w+:以读写方式打开文件，如果文件已存在则会被覆盖，不存在则会新建一个文件
wb+:以二进制方式打开并读写文件，如果文件已存在则会被覆盖，不存在则会新建一个文件
a:打开文件向文本追加新内容，如果文件已存在则会被覆盖，不存在则会新建一个文件
a+:以二进制方式打开文件向文本追加新内容，如果文件已存在则会被覆盖，不存在则会新建一个文件
```

### 3.写法

有两种打开文件的方法

```
    with open('explore.txt','a',encoding='utf-8') as f:
        f.write('\n'.join([question,author,answer]))
        f.write('\n'+'='*50+'\n')

```

文件会自动关闭，不需要再去调用close\(\)方法

另一种需要调用close\(\)方法，关闭打开的文件

```
    f = open('explore.txt','a',encoding='utf-8')
    f.write('\n'.join([question,author,answer]))
    f.write('\n'+'='*50+'\n')
    f.close()

```




### 目标

* #### 网页

分析地址:[http://image.baidu.com/search/flip?tn=baiduimage&ie=utf-8&pn=0&gsm=78&ct=⁣=0&lm=-1&width=0&height=0&word=天使](http://image.baidu.com/search/flip?tn=baiduimage&ie=utf-8&pn=0&gsm=78&ct=&ic=0&lm=-1&width=0&height=0&word=天使)

可以知道word是搜索的关键字，然后上下页不停点击翻页，可以发现pn参数在改变，而且是整数倍改变，再根据当前的图片数量可知，pn是改变页数的参数，即pn/20+1页即为当前的页数

![](/assets/spider-15.17.4-1.png)

![](/assets/spider-15.17.4-2.png)

其他参数不用管，但是也不能丢弃

* #### 图片

一般情况下网站数据要么是异步刷新，要么是直接写在源码中，因为如果没有相应的地址是无法获取到数据的，所以接下来开始抓包分析，现在打开开发者工具，然后点击到network面板，按下crl+r或者F5进行刷新页面，将数据刷新出来

* 首先查看源码看看是否有数据

![](/assets/spider-15.17.4-3.png)

可以发现没有数据加载出来，所以看下源码，是不是把数据放到js中的，如果在，就看下如何爬取数据，如果没在，就一个个筛选链接，看看是否有数据，如果都没找到，最后只能模拟浏览器浏览网页，获取数据

幸运的是，在源码中找到了数据

![](/assets/spider-15.17.4-4.png)

现在开始解析数据，如何获取想要的数据

### 解析

* 获取源码

```
r = requests.get(url=self.url,headers=headers,params=params,proxies=proxies)
```

* 利用正则表达式匹配在文本中的相应的数据

```
img_url = '"objURL":"(.*?)"'
imgs = re.findall(img_url,r.text,re.S)
```

* 获取下一页，因为前面分析指导pn是20,20的加的

```
self.parse(word=word,pn=pn+20)
```

* 存储数据

```
def save_to_image(self,word,image,pn):
    if not os.path.exists("image/"+word+"/"+pn):
        os.makedirs("image/"+word+"/"+pn)
    if not os.path.exists("image/"+word+"/"+pn+"/"+''.join(str(image).split('/')[4:])):
        with open("image/"+word+"/"+pn+"/"+''.join(str(image).split('/')[4:]),"wb") as f:
            r = requests.get(image)
            f.write(r.content)
            f.flush()
```

* [完整源码](https://github.com/CoderAngle/image.git)




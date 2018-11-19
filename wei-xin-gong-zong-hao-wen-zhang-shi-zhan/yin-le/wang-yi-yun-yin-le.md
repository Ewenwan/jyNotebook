### 分析网址

地址:https://music.163.com/\#/album?id=74267804

打开开发者工具后，切换到Network面板，然后刷新一下网页，然后点下`XHR`的选项，就会看到

![](/assets/10.17.2.1-1.png)

url的这个选项中，就包含了想要的歌曲的地址

![](/assets/10.17.2.1-2.png)

现在点下headers选项，往下找，发现有两个参数

![](/assets/10.17.2.1-3.png)

发现这些参数都看不懂是什么意思?

![](/assets/10.17.2.1+4.png)

点击js文件，然后在js文件搜索encSecKey，刚才看到的参数，搜索后，发现有三处相同的值

```
!function() {
    function a(a) {
        var d, e, b = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789", c = "";
        for (d = 0; a > d; d += 1)
            e = Math.random() * b.length,
            e = Math.floor(e),
            c += b.charAt(e);
        return c
    }
    function b(a, b) {
        var c = CryptoJS.enc.Utf8.parse(b)
          , d = CryptoJS.enc.Utf8.parse("0102030405060708")
          , e = CryptoJS.enc.Utf8.parse(a)
          , f = CryptoJS.AES.encrypt(e, c, {
            iv: d,
            mode: CryptoJS.mode.CBC
        });
        return f.toString()
    }
    function c(a, b, c) {
        var d, e;
        return setMaxDigits(131),
        d = new RSAKeyPair(b,"",c),
        e = encryptedString(d, a)
    }
    function d(d, e, f, g) {
        var h = {}
          , i = a(16);
        return h.encText = b(d, g),
        h.encText = b(h.encText, i),
        h.encSecKey = c(i, e, f),
        h
    }
    function e(a, b, d, e) {
        var f = {};
        return f.encText = c(a + e, b, d),
        f
    }
    window.asrsea = d,
    window.ecnonasr = e
}();
```

![](/assets/10.17.2.1-6.png)

可是看了只知道这个用到了加密算法aes，rsa

现在建立一个项目，在项目中把刚才的js文件拷贝一份过来

![](/assets/10.17.2.1-7.png)

并且在箭头这个地方，写一个alert，看看这串数据是什么？

接下来就打开一个 charles 抓包工具，抓取到如下数据:

![](/assets/10.17.2.1-8.png)

并且找到js所在位置

```
https://s3.music.126.net/web/s/core_b3eea79bf02325c69016228f3c0eda1e.js
```

然后找到在抓包工具中所在位置，然后如下操作



![](/assets/10.17.2.1-9.png)



![](/assets/10.17.2.1-10.png)

然后将刚在修改的js文件将进行选择，是为了替换原来的js文件，接下来刷新网页，观察网页的情况，然后会发现一些重要的数据出现了，就是四个参数构成的，有三个参数一直不变，只有self哪里的参数再改变

```
param2='010001'
param3='00e0b509f6259df8642dbc35662901477df22677ec152b5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417629ec4ee341f56135fccf695280104e0312ecbda92557c93870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b424d813cfe4875d3e82047b97ddef52741d546b8e289dc6935b3ece0462db0a22b8e7'
param4='0CoJUm6Qyw8W8jud'



self.params_mp3 = '{"ids":"[%s]","br":128000,"csrf_token":""}'
self.params_comments = '{"rid":"R_SO_4_%s","offset":"%s","total":"true","limit":"%s","csrf_token":""}'
self.params_lyric = '{"id":"%s","lv":-1,"tv":-1,"csrf_token":""}'
```

其实这些数据，是加密成了encSecKey，所以导致看不懂了，现在看懂，就开始写代码吧

### 实战

#### 加密部分代码

```
import base64
from Crypto.Cipher import AES

param2='010001'
param3='00e0b509f6259df8642dbc35662901477df22677ec152b5ff68ace615bb7b725152b3ab17a876aea8a5aa76d2e417629ec4ee341f56135fccf695280104e0312ecbda92557c93870114af6c9d05c4f7f0c3685b7a46bee255932575cce10b424d813cfe4875d3e82047b97ddef52741d546b8e289dc6935b3ece0462db0a22b8e7'
param4='0CoJUm6Qyw8W8jud'

def get_params(page,param):
    # 获取encText,也就是params
    iv = "0102030405060708"
    key1 = param4
    key2 = "F" * 16
    encText = aes_encrypt(param,key1,iv)
    encText = aes_encrypt(encText.decode('utf-8'),key2,iv)
    return encText

def aes_encrypt(text,key,iv):
    count = 16 - len(text) % 16
    text = text + count * chr(count)
    encryptor = AES.new(key.encode('utf-8'), AES.MODE_CBC, iv.encode('utf-8'))
    encrypt_text = encryptor.encrypt(text.encode('utf-8'))
    encrypt_text = base64.b64encode(encrypt_text)
    return encrypt_text

def get_encSecKey():
    key2 = "F" * 16
    encSEckey = "257348aecb5e556c066de214e531faadd1c55d814f9be95fd06d6bff9f4c7a41f831f6394d5a3fd2e3881736d94a02ca919d952872e7d0a50ebfa1769a7a62d512f5f1ca21aec60bc3819a9c3ffca5eca9a0dba6d6f7249b06f5965ecfff3695b54e1c28f3f624750ed39e7de08fc8493242e26dbc4484a01c76f739e135637c"
    return encSEckey


```

#### 接下来看下主要部分

```
import config
from utils import str_to_dict
from proxy import get_proxy
import _encrypt
import requests
import logging
import json
import sys
import re
from scrapy.selector import Selector
from pyquery import PyQuery as pq
sys.setrecursionlimit(1000000000)

# logging.basicConfig(level=logging.WARNING,
#                     format='%(asctime)s - %(filename)s[line:%(lineno)d] - %(levelname)s: %(message)s')
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s - %(filename)s[line:%(lineno)d] - %(levelname)s: %(message)s')

class Music:

    def __init__(self):
        self.headers = str_to_dict(config.HEADERS)
        self.url_mp3 = "https://music.163.com/weapi/song/enhance/player/url?csrf_token="
        self.url_comments = "https://music.163.com/weapi/v1/resource/comments/R_SO_4_{}?crsf_token="
        self.url_lyric = "https://music.163.com/weapi/song/lyric?csrf_token="
        self.url_detail = 'http://music.163.com/api/song/detail?ids=[{}]'

        self.params_mp3 = '{"ids":"[%s]","br":128000,"csrf_token":""}'
        self.params_comments = '{"rid":"R_SO_4_%s","offset":"%s","total":"true","limit":"%s","csrf_token":""}'
        self.params_lyric = '{"id":"%s","lv":-1,"tv":-1,"csrf_token":""}'


        self.song = "https://music.163.com/#/song?id={}"

        self.request = requests.Session()



    def proxy(self):
        ip = get_proxy()
        proxies = {
            'http': ip,
            'https': ip,
        }
        return proxies

    def get_encSEckey(self):
        encSEckey = _encrypt.get_encSecKey()
        return encSEckey

    # def get_comments_url(self,id):
    #      return "https://music.163.com/weapi/v1/resource/comments/R_SO_4_{}?crsf_token=".format(id)
    #
    # def get_params_mp3(self,id):
    #     return '{"ids":"[%s]","br":128000,"csrf_token":""}' % (id)
    #
    # def get_params_comments(self,id):
    #     return '{"rid":"R_SO_4_%s","offset":"%s","total":"true","limit":"%s","csrf_token":""}' % (id,id,id)


    def get_song_params(self,id,musicType):

        if musicType is "mp3":
            self.get_song_mp3(id,musicType)
        elif musicType is "comments":
            self.get_song_comments(id,musicType)
        elif musicType is "lyric":
            self.get_song_lysic(id,musicType)
        else:
            logging.info(msg="没有此类型")
            id = None

    # 歌曲
    def get_song_mp3(self,id,musicType):
        url_mp3 = self.url_mp3
        mp3 = self.params_mp3 % (id)
        self.parse_song(mp3, url_mp3, musicType,id)

    # 歌曲评论
    def get_song_comments(self,id,musicType,offset=0,limit=20):
        comments = self.params_comments % (id, offset, limit)
        url_comments = self.url_comments.format(id)
        self.parse_song(comments, url_comments, musicType,id)

    # 歌词
    def get_song_lysic(self,id,musicType):
        url_lyric = self.url_lyric
        lyric = self.params_lyric % (id)
        # logging.info(url_lyric)
        # logging.info(lyric)
        self.parse_song(lyric,url_lyric,musicType,id)

    # 解析json数据
    def parse_song(self,param,url,musicType,id):
        logging.info(url)
        logging.info(param)
        params = _encrypt.get_params(page=1, param=param)
        encSEckey = _encrypt.get_encSecKey()
        form_data = {
            "params": params,
            "encSecKey": encSEckey,
        }
        try:
            r = requests.post(url=url, headers=self.headers, data=form_data)
            content = r.text
            content = json.loads(content)
            data = self.parse_detail(id)
            if musicType == "mp3":
                if str(content["data"][0]["code"]) == str(200):
                    self.parse_mp3(content,data)
            elif musicType == "lyric":
                if not bool(content["sgc"]):
                    return
                if content:
                    self.parse_lyric(content,data)
                else:
                    print("没有")
            else:
                self.parse_comments(content,data, musicType)
        except:
            self.parse_song(param,url,musicType,id)

    # 解析歌曲
    def parse_mp3(self,content,data):
        c = content["data"][0]
        id = c["id"]
        url = c["url"]
        c = {
            "id":id,
            "url":url,
        }
        logging.info("歌曲名:{}-歌手名:{}".format(data["name"], data["singer"]))
        logging.info("获得歌曲地址:{}".format(c["url"]))

    # 解析歌曲信息
    def parse_detail(self,id):
        try:
            logging.info("解析歌曲id为{}的信息".format(id))
            r = requests.get(self.url_detail.format(id), headers=str_to_dict(config.HEADERS))
            content = r.text
            content = json.loads(content)
            if bool(content["songs"]):
                songs = content["songs"][0]
                name = songs["name"]
                artists = songs["artists"][0]
                singer = artists['name']
                data = {
                    "name": name,
                    "singer": singer,
                }
                logging.info("歌曲名:{}-歌手名:{}".format(data["name"], data["singer"]))
                return data
            else:
                logging.info("没有歌曲id为{}信息".format(id))
        except:
            self.parse_detail(id)


    # 解析评论
    def parse_comments(self,content,data,musicType):
        total = content["total"]
        if total >= 1:
            comments = content["comments"]
            # print(bool(content.get("hotComments")))
            logging.info("只获取部分评论")
            if bool(content.get("hotComments")):
                hotComments = content["hotComments"]
                logging.info("热评信息:")
                for hotComment in hotComments:
                    logging.info(hotComment)
                    logging.info("*"*50)
            for comment in comments:
                logging.info(comment)
                logging.info("*" * 50)

    # 解析歌词
    def parse_lyric(self,content,data):
        lyric = content["lrc"]["lyric"]
        nickname = ""
        try:
            nickname = content["lyricUser"]["nickname"]
        except:
            pass
        s = lyric
        lyric= ""
        count = 1
        for a in s.split('\n'):
            if a.strip(' '):
                g = re.sub(r'.*?]', "", a)
                lyric+=g+'\n'
        lyric_word = {
            "word":lyric,
            "nickname":nickname,
        }
        # logging.info("歌曲名:{}-歌手名:{}".format(data["name"],data["singer"]))
        logging.info("*"*30+"歌词"+"*"*30)
        logging.info(lyric_word["word"])
        logging.info("*" * 30 + "歌词" + "*" * 30)

Music().get_song_params(id=36025590, musicType="lyric")
```

### 项目地址

```
git clone https://github.com/CoderAngle/163spider.git
```

[zip下载](https://codeload.github.com/CoderAngle/163spider/zip/master)


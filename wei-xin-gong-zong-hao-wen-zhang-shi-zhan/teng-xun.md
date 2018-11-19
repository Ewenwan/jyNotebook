### 分析地址

地址:https://v.qq.com/x/cover/lgoty81x6m41mgb.html

打开开发者工具，从源码可以找到COVER\_INFO、VIDEO\_INFO等一些词，其中有一些信息对分析有帮助

![](/assets/10.17.3.5-1.png)

```
    def parse_url(self,url):
        r = requests.get(url,headers=self.headers)
        content = r.content.decode('utf-8',"ignore")

        list_info_search = re.search("LIST_INFO.*?=(.*?{.*?}.*?})", content, re.I)
        # print(list_info_search.group(1))
        list_info =  list_info_search.group(1).strip(' ')
        try:
            list_info = json.loads(list_info)
            vids = list_info["vid"]
        except:
            pass
        # print(vids)


        cover_info_search = re.search("COVER_INFO.*?=(.*?{.*?}.*?})", content, re.I)
        # print(cover_info_search.group(1))


        video_info_search = re.search("VIDEO_INFO.*?=(.*?{.*?})", content, re.I)
        # print(video_info_search.group(1))
        video_info = video_info_search.group(1)
        try:
            video_info = json.loads(video_info)
        except:
            pass
        vname_title = ""
        series_part_title = ""
        try:
            vname_title = video_info["vname_title"]
            series_part_title = video_info["series_part_title"]
        except:
            pass
        title = "{}/{}".format(vname_title,series_part_title)
        vid = video_info["vid"]
        # print(video_info)
        # print(title)
        self.parse(vid)
```

然后就开始动手写代码，获取到相关的信息

### API接口

```
info_api = "http://vv.video.qq.com/getinfo?vids={vid}&otype=json&defaultfmt=fhd"
key_api = "http://vv.video.qq.com/getkey?otype=json&platform=11&format={}&vid={}&filename={}&appver=3.2.19.333"
```

这里有两个api接口，info_api接口里面包含了一些视频的相关信息，这后面获取到key值，有帮助，key_


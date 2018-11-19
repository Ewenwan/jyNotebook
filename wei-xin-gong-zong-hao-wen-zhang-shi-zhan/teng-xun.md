### 分析地址

地址:[https://v.qq.com/x/cover/lgoty81x6m41mgb.html](https://v.qq.com/x/cover/lgoty81x6m41mgb.html)

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

```
这里有两个api接口，info_api接口里面包含了一些视频的相关信息，这后面获取到key值，有帮助，key_api
接口需要info_api的数据才能正常访问
```

解析来开始使用这两个接口

```
   def parse(self,vid):

        get_info_url = self.info_api.format(vid=vid)
        # print(get_info_url)
        r = requests.get(url=get_info_url,headers=self.headers)
        content = r.text.strip("QZOutputJson=").strip(";")
        content = json.loads(content)
        # print(content)
        fi = content["fl"]["fi"]

        vi = content["vl"]["vi"][0]

        ui = vi["ul"]["ui"]

        vid = vi["vid"]
        fn_pre = vi["lnk"]
        title = vi["ti"]
        host = content['vl']['vi'][0]['ul']['ui'][0]['url']
        seg_cnt = fc_cnt = content['vl']['vi'][0]['cl']['fc']

        filename = content['vl']['vi'][0]['fn']
        if seg_cnt == 0:
            seg_cnt = 1
        else:
            fn_pre, magic_str, video_type = filename.split('.')

        part_urls = []
        total_size = 0

        video_url = []

        for part in range(1, seg_cnt + 1):
            if fc_cnt == 0:
                part_format_id = content['vl']['vi'][0]['cl']['keyid'].split('.')[-1]
            else:
                part_format_id = content['vl']['vi'][0]['cl']['ci'][part - 1]['keyid'].split('.')[1]
                filename = '.'.join([fn_pre, magic_str, str(part), video_type])

            # self.key_api = "http://vv.video.qq.com/getkey?otype=json&platform=11&format={}&vid={}&filename={}&appver=3.2.19.333".format(
            #     part_format_id, vid, filename)
            # print(key_api)
            key_content = requests.get(url=self.key_api.format(part_format_id, vid, filename), headers=self.headers)
            key_content = key_content.text.strip("QZOutputJson=").strip(";")
            key_json = json.loads(key_content)
            if key_json.get('key') is None:
                vkey = content['vl']['vi'][0]['fvkey']
                url = '{}{}?vkey={}'.format(content['vl']['vi'][0]['ul']['ui'][-1]['url'], fn_pre + '.mp4', vkey)
            else:
                vkey = key_json['key']
                url = '{}{}?vkey={}'.format(host, filename, vkey)

            video_url.append(url)
            size = v_size(url)
            total_size += int(size)
            if not vkey or key_json.get('filename') is None:
                break
        print(video_url,total_size,title)
        self.download_url(urls=video_url,total_size=total_size,title=title)
```

这样就可以获取到如何数据

```
['http://ugcbsy.qq.com/uwMRJfz-r5jAYaQXGdGnC2_ppdhgmrDlPaRvaV7F2Ic/o0792f2x8qr.m701.mp4?vkey=F49418D54803639F94BA123828E59A47B16D7282B9587B28D005D5565FC38A4FD8B9F27472426E9995D29EEF576E9FE79A1C9844AF2ADDE64EE051B8522CD031741D7CB21B80F3BCD36BF69AE3E56B9F13E2F4ADB484152A273FD674B71003869B7D13BFF1BE06CD'] 
5902858 超新星版《生而为赢》MV  火箭少女新歌燃爆了！
```

### 下载视频

得到了视频链接后，就开始下载视频了

```
    def download_url(self,urls,total_size,title):
        print(total_size)
        for url in urls:

            r = requests.get(url).content

            d_size = v_size(url)
            print("{}%%".format(int(d_size)/int(total_size)*100))

            if not os.path.exists("../save_vedio/"):
                os.mkdir("../save_vedio/")

            with open("../save_vedio/{}.download.mp4".format(title),"wb") as f:
                index = 0
                f.write(r)
```

### 完整代码

后续整理好后，发上传到github里






### 目标

* 麻花视频app软件
  * [下载](http://www.mahua.cc/app/download)
* 麻花网页地址:
  * 分析https://www.imahua.tv/moivesfilter?vtype=1&list=

### 抓包工具

* fiddler

可能需要方法:

1. [fiddler抓包出现tunnel to](/wei-xin-gong-zong-hao-wen-zhang-shi-zhan/fiddler-zhua-bao-chu-xian-tunnel-to.md)
2. [fiddler + 模拟器](/wei-xin-gong-zong-hao-wen-zhang-shi-zhan/fiddler-+-shou-ji-mo-ni-qi.md)

### 模拟器

采用MuMu模拟器

### 捕获、分析数据



### 代码

* 最开始的代码，由于走了很多弯路，但是不想删除。。。

  ```
  #coding:utf-8

  import requests
  from util.parse_headers import dict_headers
  from util.parse_ts import get_ts
  from util.proxy import get_proxy
  from util.parse_json import get_json
  import config
  from urllib.parse import urljoin
  import m3u8
  import os,sys
  from selenium import webdriver
  import time

  chrome_options = webdriver.ChromeOptions()
  # prefs = {"profile.managed_default_content_settings.images": 2}
  # chrome_options.add_experimental_option("prefs", prefs)

  # 加载所有配置
  chrome_options.add_argument(r'--user-data-dir=C:\Users\tokimeki\AppData\Local\Google\Chrome\User Data')

  class Mahua:

      def __init__(self):
          # 视频基本地址
          self.base_url = "http://v2.zhubodasai.com/"
          self.headers = dict_headers(config.MAHUA_HEADERS)
          self.session = requests.session()
          # 获取信息的地址
          self.main_url = "http://www.mahua.cc"
          self.browser = webdriver.Chrome(chrome_options=chrome_options)

      # 封装访问每个ts文件
      def parse_url(self,url=None):
          url = urljoin(self.base_url,url)
          r = self.session.get(url=url,headers=self.headers)
          r.encoding = "utf-8"
          return r

      def parse_vedio_m3u8_op(self,url):
          r = self.parse_url(url).text
          tss = get_ts(r)
          print(tss)

      # 下载m3u8文件
      def parse_vedio_m3u8(self,url):

          # url部分链接
          index = [i for i,v in enumerate(url.split('/')) if v.find("m3u8") != -1][0]
          self.url = "/".join(url.split('/')[:index])
          self.url= urljoin(self.base_url, self.url)

          r = self.parse_url(url).text
          print(self.url)
          om3u8 = m3u8.loads(r)
          tss = om3u8.segments.uri
          self.dowlonad_vedio(tss)

      # 下载视频
      def dowlonad_vedio(self,tss):

          filename = "../"+config.MAHUA_DOWNLOAD_DIR_NAME
          vedioname = "刀剑神域.mp4"
          href = self.url
          if not os.path.exists(filename):
              os.makedirs(filename)

          with open(filename+"/"+vedioname, "wb") as f:
              for ts in tss:
                  url = href+"/"+ts
                  r = self.parse_url(url)
                  print(url)
                  for chunk in r.iter_content(1024 * 18):
                      f.write(chunk)


      # 视频的基本信息
      def parse_vedio_info(self,url=None):
          url = "http://www.mahua.cc/moivesfilter?vtype=3&list="
          self.browser.get(url)
          self.next_page()

      # 无法获取ajax请求的信息
      def next_page(self,m=0):

          data = self.browser.page_source
          get_json(data)

          self.browser.implicitly_wait(5)
          time.sleep(3)

          btn = self.browser.find_element_by_css_selector("button.btn-next")
          text = btn.get_attribute("disabled")
          if str(text).strip(' '):
              btn.click()
              self.next_page(m+1)


      # 代理不行
      def parse_vedio_info_json(self):
          url = "http://www.mahua.cc/service/video/queryVideoInfoPage"
          data = {
              "currentPage": 3,
              "flag": 1,
              "pageSize": 30,
              "type": 3,
              "typeList": r"[]",
          }
          ip = get_proxy()
          proxies = {
              "http":ip,
              "https":ip,
          }
          r = requests.post("http://www.baidu.com",proxies=proxies)
          r.encoding = 'utf-8'
          print(r.text)

      # 通过src拼接地址
      def parse_vedio(self,src):
          pass


  url = "mahua/m_video/m_20180804_1099/2/5a17fb6f7af51c82a09a508f64260303_free.m3u8?token=cz03NWJhOTkxYTg3YWMyYTI0Nzg4ZDc5YWE5Mzc4YTYxMCZpPTEyMzQ1ODUyJnA9MTI2MiZ0PTE1NDkzNTMyMjMmbj01YTE3ZmI2ZjdhZjUxYzgyYTA5YTUwOGY2NDI2MDMwM19mcmVlLm0zdTgmcj0xJnY9MS4wLjAmYz0zJmU9NzIw"
  # Mahua().parse_vedio_m3u8(url)
  Mahua().parse_vedio_info()
  ```






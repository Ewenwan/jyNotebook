# 3.2.2 高级用法

## 1. 文件上传 {#1-文件上传}

利用requests实现文件上传

实例:

```text
import requests

files = {'file':open('favicon.ico','rb')}
response = requests.post('http://httpbin.org/post',files=files)
print(response.text)
```

运行结果:

```text
{
  "args": {}, 
  "data": "", 
  "files": {
    "file": "data:application/octet-stream;base64,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AAAAAAAAKysrBhYWGUcWFhiVFRUYvxUVGNkWFhfzFhYX8xUVGNkVFRi/FhYYlRYWGUcrKysGAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA="
  }, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Content-Length": "6665", 
    "Content-Type": "multipart/form-data; boundary=6790c78bd178438aa1f006feb3faf802", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.18.4"
  }, 
  "json": null, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/post"
}
```

## 2. Cookies {#2-cookies}

设置cookies实例:

```text
import requests

response = requests.get('https://www.baidu.com')
print(response.cookies)
for key,value in response.cookies.items():
    print(key+"="+value)
```

运行结果:

```text
<RequestsCookieJar[<Cookie BDORZ=27315 for .baidu.com/>]>
BDORZ=27315
```

返回的是RequestCookieJar 类型

以知乎为例，直接利用 Cookies 来维持登录状态

```text
import requests

headers = {
    'Cookie': 'q_c1=31653b264a074fc9a57816d1ea93ed8b|1474273938000|1474273938000; d_c0="AGDAs254kAqPTr6NW1U3XTLFzKhMPQ6H_nc=|1474273938"; __utmv=51854390.100-1|2=registration_date=20130902=1^3=entry_date=20130902=1;a_t="2.0AACAfbwdAAAXAAAAso0QWAAAgH28HQAAAGDAs254kAoXAAAAYQJVTQ4FCVgA360us8BAklzLYNEHUd6kmHtRQX5a6hiZxKCynnycerLQ3gIkoJLOCQ==";z_c0=Mi4wQUFDQWZid2RBQUFBWU1DemJuaVFDaGNBQUFCaEFsVk5EZ1VKV0FEZnJTNnp3RUNTWE10ZzBRZFIzcVNZZTFGQmZn|1474887858|64b4d4234a21de774c42c837fe0b672fdb5763b0',
    'Host': 'www.zhihu.com',
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.116 Safari/537.36',
}
r = requests.get('https://www.zhihu.com', headers=headers)
print(r.text)
```

运行结果:

```text
<!doctype html>
<html lang="zh" data-hairline="true" data-theme="light"><head><meta charSet="utf-8"/><title data-react-helmet="true">知乎 - 发现更大的世界</title><meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1"/><meta name="renderer" content="webkit"/><meta name="force-rendering" content="webkit"/><meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/><meta name="google-site-verification" content="FTeR0c8arOPKh8c5DYh_9uu98_zJbaWw53J-Sch9MTg"/><link rel="shortcut icon" type="image/x-icon" href="https://static.zhihu.com/static/favicon.ico"/><link rel="search" type="application/opensearchdescription+xml" href="https://static.zhihu.com/static/search.xml" title="知乎"/><link rel="dns-prefetch" href="//static.zhimg.com"/><link rel="dns-prefetch" href="//pic1.zhimg.com"/><link rel="dns-prefetch" href="//pic2.zhimg.com"/><link rel="dns-prefetch" href="//pic3.zhimg.com"/><link rel="dns-prefetch" href="//pic4.zhimg.com"/><link href="https://static.zhihu.com/heifetz/main.app.efada145308ef5d626df.css" rel="stylesheet"/></head><body class="EntrySign-body Body--isAppleDevice"><p hidden="">有问题，上知乎。知乎作为中文互联网最大的知识分享平台，以「知识连接一切」为愿景，致力于构建一个人人都可以便捷接入的知识分享网络，让人们便捷地与世界分享知识、经验和见解，发现更大的世界。</p><div id="root"><div data-zop-usertoken="{}" data-reactroot=""><div class="LoadingBar"></div><div><header role="banner" class="Sticky AppHeader" data-za-module="TopNavBar"><div class="AppHeader-inner"><a href="//www.zhihu.com" aria-label="知乎"><svg viewBox="0 0 200 91" class="Icon ZhihuLogo ZhihuLogo--blue Icon--logo" style="height:30px;width:64px" width="64" height="30" aria-hidden="true"><title></title><g><path d="M53.29 80.035l7.32.002 2.41 8.24 13.128-8.24h15.477v-67.98H53.29v67.978zm7.79-60.598h22.756v53.22h-8.73l-8.718 5.473-1.587-5.46-3.72-.012v-53.22zM46.818 43.162h-16.35c.545-8.467.687-16.12.687-22.955h15.987s.615-7.05-2.68-6.97H16.807c1.09-4.1 2.46-8.332 4.1-12.708 0 0-7.523 0-10.085 6.74-1.06 2.78-4.128 13.48-9.592 24.41 1.84-.2 7.927-.37 11.512-6.94.66-1.84.785-2.08 1.605-4.54h9.02c0 3.28-.374 20.9-.526 22.95H6.51c-3.67 0-4.863 7.38-4.863 7.38H22.14C20.765 66.11 13.385 79.24 0 89.62c6.403 1.828 12.784-.29 15.937-3.094 0 0 7.182-6.53 11.12-21.64L43.92 85.18s2.473-8.402-.388-12.496c-2.37-2.788-8.768-10.33-11.496-13.064l-4.57 3.627c1.363-4.368 2.183-8.61 2.46-12.71H49.19s-.027-7.38-2.372-7.38zm128.752-.502c6.51-8.013 14.054-18.302 14.054-18.302s-5.827-4.625-8.556-1.27c-1.874 2.548-11.51 15.063-11.51 15.063l6.012 4.51zm-46.903-18.462c-2.814-2.577-8.096.667-8.096.667s12.35 17.2 12.85 17.953l6.08-4.29s-8.02-11.752-10.83-14.33zM199.99 46.5c-6.18 0-40.908.292-40.953.292v-31.56c1.503 0 3.882-.124 7.14-.376 12.773-.753 21.914-1.25 27.427-1.504 0 0 3.817-8.496-.185-10.45-.96-.37-7.24 1.43-7.24 1.43s-51.63 5.153-72.61 5.64c.5 2.756 2.38 5.336 4.93 6.11 4.16 1.087 7.09.53 15.36.277 7.76-.5 13.65-.76 17.66-.76v31.19h-41.71s.88 6.97 7.97 7.14h33.73v22.16c0 4.364-3.498 6.87-7.65 6.6-4.4.034-8.15-.36-13.027-.566.623 1.24 1.977 4.496 6.035 6.824 3.087 1.502 5.054 2.053 8.13 2.053 9.237 0 14.27-5.4 14.027-14.16V53.93h38.235c3.026 0 2.72-7.432 2.72-7.432z" fill-rule="evenodd"/></g></svg></a><nav role="navigation" class="AppHeader-nav"><a class="AppHeader-navItem" href="//www.zhihu.com/">首页</a><a class="AppHeader-navItem" href="//www.zhihu.com/explore">发现</a><a href="//www.zhihu.com/topic" class="AppHeader-navItem">话题</a></nav><div class="SearchBar" role="search" data-za-module="PresetWordItem"><div class="SearchBar-toolWrapper"><form class="SearchBar-tool"><div><div class="Popover"><div class="SearchBar-input Input-wrapper Input-wrapper--grey"><input type="text" maxLength="100" value="" autoComplete="off" role="combobox" aria-expanded="false" aria-autocomplete="list" aria-activedescendant="null--1" id="null-toggle" aria-haspopup="true" aria-owns="null-content" class="Input" placeholder=""/><div class="Input-after"><button aria-label="搜索" type="button" class="Button SearchBar-searchIcon Button--primary"><svg viewBox="0 0 16 16" class="Icon Icon--search" style="height:16px;width:16px" width="16" height="16" aria-hidden="true"><title></title><g><path d="M12.054 10.864c.887-1.14 1.42-2.57 1.42-4.127C13.474 3.017 10.457 0 6.737 0S0 3.016 0 6.737c0 3.72 3.016 6.737 6.737 6.737 1.556 0 2.985-.533 4.127-1.42l3.103 3.104c.765.46 1.705-.37 1.19-1.19l-3.103-3.104zm-5.317.925c-2.786 0-5.053-2.267-5.053-5.053S3.95 1.684 6.737 1.684 11.79 3.95 11.79 6.737 9.522 11.79 6.736 11.79z"/></g></svg></button></div></div></div></div></form></div></div><div class="AppHeader-userInfo"><div><button type="button" class="Button AppHeader-login Button--blue">登录</button><button type="button" class="Button Button--primary Button--blue">加入知乎</button></div></div></div></header></div><main role="main" class="App-main"><div class="SignFlowHomepage"><div class="SignFlowHomepage-content"><div class="Card SignContainer-content"><div class="SignFlowHeader" style="padding-bottom:5px"><svg viewBox="0 0 200 91" class="Icon ZhihuLogo ZhihuLogo--blue Icon--logo" style="height:65.625px;width:140px" width="140" height="65.625" aria-hidden="true"><title></title><g><path d="M53.29 80.035l7.32.002 2.41 8.24 13.128-8.24h15.477v-67.98H53.29v67.978zm7.79-60.598h22.756v53.22h-8.73l-8.718 5.473-1.587-5.46-3.72-.012v-53.22zM46.818 43.162h-16.35c.545-8.467.687-16.12.687-22.955h15.987s.615-7.05-2.68-6.97H16.807c1.09-4.1 2.46-8.332 4.1-12.708 0 0-7.523 0-10.085 6.74-1.06 2.78-4.128 13.48-9.592 24.41 1.84-.2 7.927-.37 11.512-6.94.66-1.84.785-2.08 1.605-4.54h9.02c0 3.28-.374 20.9-.526 22.95H6.51c-3.67 0-4.863 7.38-4.863 7.38H22.14C20.765 66.11 13.385 79.24 0 89.62c6.403 1.828 12.784-.29 15.937-3.094 0 0 7.182-6.53 11.12-21.64L43.92 85.18s2.473-8.402-.388-12.496c-2.37-2.788-8.768-10.33-11.496-13.064l-4.57 3.627c1.363-4.368 2.183-8.61 2.46-12.71H49.19s-.027-7.38-2.372-7.38zm128.752-.502c6.51-8.013 14.054-18.302 14.054-18.302s-5.827-4.625-8.556-1.27c-1.874 2.548-11.51 15.063-11.51 15.063l6.012 4.51zm-46.903-18.462c-2.814-2.577-8.096.667-8.096.667s12.35 17.2 12.85 17.953l6.08-4.29s-8.02-11.752-10.83-14.33zM199.99 46.5c-6.18 0-40.908.292-40.953.292v-31.56c1.503 0 3.882-.124 7.14-.376 12.773-.753 21.914-1.25 27.427-1.504 0 0 3.817-8.496-.185-10.45-.96-.37-7.24 1.43-7.24 1.43s-51.63 5.153-72.61 5.64c.5 2.756 2.38 5.336 4.93 6.11 4.16 1.087 7.09.53 15.36.277 7.76-.5 13.65-.76 17.66-.76v31.19h-41.71s.88 6.97 7.97 7.14h33.73v22.16c0 4.364-3.498 6.87-7.65 6.6-4.4.034-8.15-.36-13.027-.566.623 1.24 1.977 4.496 6.035 6.824 3.087 1.502 5.054 2.053 8.13 2.053 9.237 0 14.27-5.4 14.027-14.16V53.93h38.235c3.026 0 2.72-7.432 2.72-7.432z" fill-rule="evenodd"/></g></svg><div class="SignFlowHeader-slogen">登录<!-- -->知乎，发现更大的世界</div></div><div class="SignContainer-inner"><div class="Login-content"><form novalidate="" class="SignFlow"><div class="SignFlow-account"><div class="SignFlow-supportedCountriesSelectContainer"></div><div class="SignFlowInput SignFlow-accountInputContainer"><div class="SignFlow-accountInput Input-wrapper"><input type="text" value="" name="username" class="Input" placeholder="手机号或邮箱"/></div><div class="SignFlowInput-errorMask SignFlowInput-requiredErrorMask SignFlowInput-errorMask--hidden"></div></div></div><div class="SignFlow-password"><div class="SignFlowInput"><div class="Input-wrapper"><input type="password" value="" name="password" class="Input" placeholder="密码"/></div><div class="SignFlowInput-errorMask SignFlowInput-requiredErrorMask SignFlowInput-errorMask--hidden"></div></div><button tabindex="-1" type="button" class="Button SignFlow-switchPassword Button--plain"><svg width="24" height="20" viewBox="0 0 24 24" class="Icon SignFlow-switchPasswordIcon Icon--inconspicuous" style="vertical-align:middle;height:20px;width:24px" aria-hidden="true"><title></title><g><title>Inconspicuous</title><path d="M17.007 11.504c0 .65-.13 1.26-.36 1.83l3 3.073S23 14.136 23 11.504C23 8.008 17.255 4 11.995 4c-1.4 0-2.741.25-3.982.701l2.161 2.16c.57-.23 1.18-.36 1.831-.36a5.004 5.004 0 0 1 5.002 5.003zM2.57 4.342l2.067 2.075C3.499 7.258 1 9.119 1 11.504c0 3.336 5.79 7.503 11.005 7.503 1.55 0 3.031-.3 4.382-.84l.42.42 2.125 2.118s.782.571 1.314 0-.074-1.305-.074-1.305L3.955 3.183s-.76-.742-1.385-.19c-.626.554 0 1.35 0 1.35zm4.963 4.96l1.55 1.552c-.05.21-.08.43-.08.65 0 1.66 1.341 3.001 3.002 3.001.22 0 .44-.03.65-.08l1.551 1.551c-.67.33-1.41.53-2.2.53a5.004 5.004 0 0 1-5.003-5.002c0-.79.2-1.53.53-2.201zm4.312-.78l3.151 3.152.02-.16c0-1.66-1.34-3.001-3.001-3.001l-.17.01z" fill-rule="evenodd"/></g></svg></button></div><div class="Captcha SignFlow-captchaContainer" style="width:0;height:0;opacity:0;overflow:hidden;margin:0;padding:0;border:0"><div><div class="Captcha-chineseOperator"><span class="Captcha-info">请点击图中倒立的文字</span><button type="button" class="Button Captcha-chineseRefreshButton Button--plain"><svg class="Zi Zi--Refresh" fill="currentColor" viewBox="0 0 24 24" width="20" height="20"><path d="M20 12.878C20 17.358 16.411 21 12 21s-8-3.643-8-8.122c0-4.044 3.032-7.51 6.954-8.038.034-1.185.012-1.049.012-1.049-.013-.728.461-1.003 1.057-.615l3.311 2.158c.598.39.596 1.026 0 1.418l-3.31 2.181c-.598.393-1.08.12-1.079-.606 0 0 .006-.606-.003-1.157-2.689.51-4.675 2.9-4.675 5.708 0 3.21 2.572 5.822 5.733 5.822 3.163 0 5.733-2.612 5.733-5.822 0-.633.51-1.148 1.134-1.148.625 0 1.133.515 1.133 1.148" fill-rule="evenodd"></path></svg></button></div><div class="Captcha-chineseContainer"><img data-tooltip="看不清楚？换一张" class="Captcha-chineseImg" src="data:image/jpg;base64,null" alt="图形验证码"/></div></div></div><div class="Login-options"><button type="button" class="Button Login-switchType Button--plain">手机验证码登录</button><button type="button" class="Button Login-cannotLogin Button--plain">忘记密码？</button></div><button type="submit" class="Button SignFlow-submitButton Button--primary Button--blue">登录</button><div class="Login-footer"><span class="Login-qrcode"><button type="button" class="Button Button--plain">二维码登录</button></span><span class="Login-footerSeparate Login-qrcodeSeparate"> · </span><span class="Login-aboardPhone"><button type="button" class="Button Button--plain">海外手机登录</button></span><span class="Login-footerSeparate"> · </span><span class="Login-socialLogin"><button type="button" class="Button Login-socialButtonEntrance Button--plain">社交帐号登录</button><span class="Login-socialButtonGroup Login-socialButtonGroup--hidden"><button disabled="" type="button" class="Button Login-socialButton Button--plain"><svg viewBox="0 0 20 19" class="Icon Login-socialIcon Icon--wechat" style="height:17px;width:18px" width="18" height="17" aria-hidden="true"><title></title><g><path fill-rule="evenodd" d="M.224 18.667s4.24-1.825 4.788-2.056C13.03 20.14 20 14.715 20 8.9 20 3.984 15.523 0 10 0S0 3.984 0 8.898c0 1.86.64 3.585 1.737 5.013-.274.834-1.513 4.757-1.513 4.757zM6.167 8.96c.69 0 1.25-.57 1.25-1.27 0-.703-.56-1.272-1.25-1.272s-1.25.57-1.25 1.27c0 .703.56 1.272 1.25 1.272zm7.583 0c.69 0 1.25-.57 1.25-1.27 0-.703-.56-1.272-1.25-1.272s-1.25.57-1.25 1.27c0 .703.56 1.272 1.25 1.272z"/></g></svg></button><button disabled="" type="button" class="Button Login-socialButton Button--plain"><svg viewBox="0 0 22 18" class="Icon Login-socialIcon Icon--weibo" style="height:16px;width:20px" width="20" height="16" aria-hidden="true"><title></title><g><g fill-rule="evenodd">     <path d="M14.518.06s-.87.644.03 1.71c0 0 6.287-1.19 5.69 6.33 0 0 1.05 1.13 1.674-.31 0 .002 1.44-8.584-7.394-7.73zM4.883 13.17s.038 2.584 3.326 2.584c3.657 0 3.683-2.98 3.683-2.98S12.1 9.67 8.687 9.61c-3.863-.07-3.804 3.56-3.804 3.56zM7.41 14.21c-.668 0-1.214-.447-1.214-.998 0-.55.543-.998 1.215-.998.67 0 1.213.447 1.213.998 0 .55-.54.998-1.212.998z"/>     <path d="M4.317 4.52C-2.603 10.353.873 14.85.873 14.85c.57 1.01 3.382 3.1 8.596 3.1 5.21 0 9.314-3.628 9.314-6.44 0-2.813-2.918-2.714-2.918-2.714 1.04-1.554.19-2.65.19-2.65-1.684-2.118-5.404-.16-5.407-.158.772-1.717.11-2.797.11-2.797C8.932.66 4.317 4.52 4.317 4.52zm10.448 7.79s-.467 4.16-6.447 4.16c-5.745 0-5.82-3.322-5.842-3.712 0 0-.073-4.423 6.58-4.654 5.94-.204 5.71 4.207 5.71 4.207zM18.65 7.045s1.018-4.37-3.864-3.818c0 0-.628.58.09 1.346 0 0 2.602-.58 2.397 2.598 0 0 .715.885 1.376-.125z"/>   </g></g></svg></button><button disabled="" type="button" class="Button Login-socialButton Button--plain"><svg width="17" height="19" viewBox="0 0 18 20" xmlns="http://www.w3.org/2000/svg" class="Icon Login-socialIcon Icon--qq" style="height:19px;width:17px" aria-hidden="true"><title></title><g><title>QQ</title><path d="M9.003 0c-2.265 0-6.29 1.364-6.29 7.325V8.52S.55 12.96.55 15.474c0 .665.17 1.025.28 1.025.115 0 .903-.485 1.75-2.073 0 0-.18 2.197 1.903 3.967 0 0-1.77.495-1.77 1.182 0 .686 4.078.43 6.29 0 2.24.425 6.287.687 6.287 0 0-.688-1.768-1.182-1.768-1.182 2.085-1.77 1.905-3.967 1.905-3.967.845 1.588 1.634 2.072 1.746 2.072.11 0 .283-.36.283-1.026 0-2.514-2.166-6.954-2.166-6.954V7.325C15.29 1.365 11.268 0 9.003 0z" fill-rule="evenodd"/></g></svg></button></span></span></div></form></div><div class="SignContainer-switch">没有帐号？<span>注册</span></div><div class="SignFlowHomepage-qrImage SignFlowHomepage-qrImageHidden"><div></div></div></div></div><button type="button" class="Button SignFlowHomepage-downloadBtn">下载知乎 App</button></div><footer class="SignFlowHomepage-footer"><div class="ZhihuLinks"><a target="_blank" rel="noopener noreferrer" href="https://zhuanlan.zhihu.com">知乎专栏</a><a target="_blank" rel="noopener noreferrer" href="/roundtable">圆桌</a><a target="_blank" rel="noopener noreferrer" href="/explore">发现</a><a target="_blank" rel="noopener noreferrer" href="/app">移动应用</a><a target="_blank" rel="noopener noreferrer" href="/contact">联系我们</a><a target="_blank" rel="noopener noreferrer" href="https://app.mokahr.com/apply/zhihu">来知乎工作</a><a target="_blank" rel="noopener noreferrer" href="/org/signup">注册机构号</a></div><div class="ZhihuRights"><span>© 2018 知乎</span><a target="_blank" rel="noopener noreferrer" href="http://www.miibeian.gov.cn/">京 ICP 证 110745 号</a><span>京公网安备 11010802010035 号<a href="http://zhstatic.zhihu.com/assets/zhihu/publish-license.jpg" target="_blank" rel="noopener noreferrer">出版物经营许可证</a></span></div><div class="ZhihuReports"><a target="_blank" rel="noopener noreferrer" href="https://zhuanlan.zhihu.com/p/28852607">侵权举报</a><a target="_blank" rel="noopener noreferrer" href="http://www.12377.cn">网上有害信息举报专区</a><a target="_blank" rel="noopener noreferrer" href="/jubao">儿童色情信息举报专区</a><span>违法和不良信息举报：010-82716601</span></div><div class="ZhihuIntegrity"><div><img src="https://static.zhihu.com/static/revved/img/index/chengxing_logo@2x.65dc76e8.png" alt="诚信网站示范企业"/><a href="https://credit.szfw.org/CX20170607038331320388.html">诚信网站示范企业</a></div></div></footer></div></main></div></div><div id="data" style="display:none" data-state="{&quot;common&quot;:{&quot;ask&quot;:{}},&quot;privacy&quot;:{&quot;showPrivacy&quot;:false},&quot;loading&quot;:{&quot;global&quot;:{&quot;count&quot;:0},&quot;local&quot;:{&quot;env/getExperiments/&quot;:false}},&quot;entities&quot;:{&quot;users&quot;:{},&quot;questions&quot;:{},&quot;answers&quot;:{},&quot;articles&quot;:{},&quot;columns&quot;:{},&quot;topics&quot;:{},&quot;roundtables&quot;:{},&quot;favlists&quot;:{},&quot;comments&quot;:{},&quot;notifications&quot;:{},&quot;ebooks&quot;:{},&quot;activities&quot;:{},&quot;feeds&quot;:{},&quot;pins&quot;:{},&quot;promotions&quot;:{},&quot;drafts&quot;:{}},&quot;currentUser&quot;:&quot;&quot;,&quot;account&quot;:{&quot;lockLevel&quot;:{},&quot;unlockTicketStatus&quot;:false,&quot;unlockTicket&quot;:null,&quot;challenge&quot;:[],&quot;errorStatus&quot;:false,&quot;message&quot;:&quot;&quot;,&quot;isFetching&quot;:false,&quot;accountInfo&quot;:{},&quot;urlToken&quot;:{&quot;loading&quot;:false}},&quot;settings&quot;:{&quot;socialBind&quot;:null,&quot;inboxMsg&quot;:null,&quot;notification&quot;:{},&quot;email&quot;:{},&quot;privacyFlag&quot;:null,&quot;blockedUsers&quot;:{&quot;isFetching&quot;:false,&quot;paging&quot;:{&quot;pageNo&quot;:1,&quot;pageSize&quot;:6},&quot;data&quot;:[]},&quot;blockedFollowees&quot;:{&quot;isFetching&quot;:false,&quot;paging&quot;:{&quot;pageNo&quot;:1,&quot;pageSize&quot;:6},&quot;data&quot;:[]},&quot;ignoredTopics&quot;:{&quot;isFetching&quot;:false,&quot;paging&quot;:{&quot;pageNo&quot;:1,&quot;pageSize&quot;:6},&quot;data&quot;:[]},&quot;restrictedTopics&quot;:null,&quot;laboratory&quot;:{}},&quot;notification&quot;:{},&quot;people&quot;:{&quot;profileStatus&quot;:{},&quot;activitiesByUser&quot;:{},&quot;answersByUser&quot;:{},&quot;answersSortByVotesByUser&quot;:{},&quot;answersIncludedByUser&quot;:{},&quot;votedAnswersByUser&quot;:{},&quot;thankedAnswersByUser&quot;:{},&quot;voteAnswersByUser&quot;:{},&quot;thankAnswersByUser&quot;:{},&quot;topicAnswersByUser&quot;:{},&quot;articlesByUser&quot;:{},&quot;articlesSortByVotesByUser&quot;:{},&quot;articlesIncludedByUser&quot;:{},&quot;pinsByUser&quot;:{},&quot;questionsByUser&quot;:{},&quot;commercialQuestionsByUser&quot;:{},&quot;favlistsByUser&quot;:{},&quot;followingByUser&quot;:{},&quot;followersByUser&quot;:{},&quot;mutualsByUser&quot;:{},&quot;followingColumnsByUser&quot;:{},&quot;followingQuestionsByUser&quot;:{},&quot;followingFavlistsByUser&quot;:{},&quot;followingTopicsByUser&quot;:{},&quot;publicationsByUser&quot;:{},&quot;columnsByUser&quot;:{},&quot;allFavlistsByUser&quot;:{},&quot;brands&quot;:null},&quot;env&quot;:{&quot;ab&quot;:{&quot;config&quot;:{&quot;experiments&quot;:[{&quot;expId&quot;:&quot;launch-ad_rtl_http-2&quot;,&quot;expPrefix&quot;:&quot;ad_rtl_http&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_adr_mini-2&quot;,&quot;expPrefix&quot;:&quot;gw_adr_mini&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_adr_wbtp-2&quot;,&quot;expPrefix&quot;:&quot;gw_adr_wbtp&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_anr_wxbk-2&quot;,&quot;expPrefix&quot;:&quot;gw_anr_wxbk&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_ios_mini-2&quot;,&quot;expPrefix&quot;:&quot;gw_ios_mini&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_ios_wxb-2&quot;,&quot;expPrefix&quot;:&quot;gw_ios_wxb&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_unif-4&quot;,&quot;expPrefix&quot;:&quot;gw_unif&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-gw_wbtp-2&quot;,&quot;expPrefix&quot;:&quot;gw_wbtp&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-mp_hb_si-3&quot;,&quot;expPrefix&quot;:&quot;mp_hb_si&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-mp_ios_webp-2&quot;,&quot;expPrefix&quot;:&quot;mp_ios_webp&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-mp_video_feed-2&quot;,&quot;expPrefix&quot;:&quot;mp_video_feed&quot;,&quot;isDynamicallyUpdated&quot;:false,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-vd_adrupload_cdn-2&quot;,&quot;expPrefix&quot;:&quot;vd_adrupload_cdn&quot;,&quot;isDynamicallyUpdated&quot;:false,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;launch-vd_upload_cdn-2&quot;,&quot;expPrefix&quot;:&quot;vd_upload_cdn&quot;,&quot;isDynamicallyUpdated&quot;:false,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false},{&quot;expId&quot;:&quot;top_dtmt-10&quot;,&quot;expPrefix&quot;:&quot;top_dtmt&quot;,&quot;isDynamicallyUpdated&quot;:true,&quot;isRuntime&quot;:false,&quot;includeTriggerInfo&quot;:false}],&quot;params&quot;:[{&quot;id&quot;:&quot;top_yhgc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_ad_skip_pos&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;up&quot;},{&quot;id&quot;:&quot;top_tag_isolation&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_video_agent_4_22&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;top_lowup&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_tr&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_video_rew&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;tp_sft&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;a&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_comment&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;adr_task_statistics&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;top_alt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_ad_cta&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_edit_question&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_real_time_launch_http&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;http_off&quot;},{&quot;id&quot;:&quot;ios_ps&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_billread&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_nad&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_newfollow&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_unif&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;on&quot;},{&quot;id&quot;:&quot;top_an&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_pdf&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;n&quot;},{&quot;id&quot;:&quot;adr_android_video_continuous&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_sqtc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_billab&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_feedre_cpt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;101&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_cta&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_topsearch&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;2&quot;},{&quot;id&quot;:&quot;adr_mini&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_qtoc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_billupdate1&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_feedre&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_video_fix_position&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_book_is_card&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_member_switch&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_psn&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;n&quot;},{&quot;id&quot;:&quot;top_followtop&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_hqt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_nuc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_tagore&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_perm&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_ge4&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;3&quot;},{&quot;id&quot;:&quot;adr_profile_label&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_answer_preload&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_magitab&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_video_feed&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;web_logoc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;blue&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_editor_version&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;V2&quot;},{&quot;id&quot;:&quot;adr_invite&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;ios_adr_vid_vol&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_login_card&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_anp&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;android_answer_pager_off&quot;},{&quot;id&quot;:&quot;adr_traffic_leak&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;top_ntr&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_root_few_topic&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_sj&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;2&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_book_is_card&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_gr_topic_reweight&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_wbtp&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_nmt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_root_mg&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_ps&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_profile_sig&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;true&quot;},{&quot;id&quot;:&quot;top_yc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_prt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;pin_efs&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;orig&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_wxbk&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_nid&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_profile_badge&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;top_root_web&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_follow_reason&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_root&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_comment&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_billpic&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_gr_auto_model&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_universalebook&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_vdio_rew&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_video_topic_volume_control&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_wbtp&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_wxbk&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_le_nav&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_spic&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ls_play_continuous_order&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_feedre_rtt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;41&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_asp&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;off&quot;},{&quot;id&quot;:&quot;ios_x_z_c0&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_30&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;ios_km_center&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_real_time_launch_is_http&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_feedre_itemcf&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;31&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_mlt_model&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_spic&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_traffic_monitor&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;ios_hybrid_editor_v3&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_notif_new_invite&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;off&quot;},{&quot;id&quot;:&quot;adr_guest_login&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_ljb&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;launch_jump_button_up&quot;},{&quot;id&quot;:&quot;ios_real_time_launch_http&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;http_off&quot;},{&quot;id&quot;:&quot;ios_webp&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_ebook&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_use_cashier&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;new&quot;},{&quot;id&quot;:&quot;ios_more_editcard&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;ios_q_bar&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;NO&quot;},{&quot;id&quot;:&quot;ios_video_continuous&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_recall&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_anr_watch&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;false&quot;},{&quot;id&quot;:&quot;ios_pay_view&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;new&quot;},{&quot;id&quot;:&quot;ios_article_new_comment&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_billvideo&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_is_gr&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_nszt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_medal&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_q_bar&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;NO&quot;},{&quot;id&quot;:&quot;ios_1752&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_hybrid_intercepting&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_next_ans&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;N&quot;},{&quot;id&quot;:&quot;se_tf&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_sjre&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_grow_guide_login_4&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;3&quot;},{&quot;id&quot;:&quot;adr_profile_medal&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_wxfb&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_billupdate&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_multi_model&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_tmt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_more_hyb_card&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;adr_next_answer_btn&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;ios_mini&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_video_upload_cdn&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;top_bill&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_dtmt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;2&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_nucc&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_tffrt&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_video_upload_cdn&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_7324&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;web_ask_flow&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;default&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;pin_ef&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;orig&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_topic_feedre&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;21&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_wxfb&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;1&quot;},{&quot;id&quot;:&quot;ios_apm&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;},{&quot;id&quot;:&quot;top_gif&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;top_gr_model&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;0&quot;,&quot;chainId&quot;:&quot;_all_&quot;},{&quot;id&quot;:&quot;adr_pdf&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;n&quot;},{&quot;id&quot;:&quot;adr_traffic_threshold&quot;,&quot;type&quot;:&quot;String&quot;,&quot;value&quot;:&quot;314572800&quot;}],&quot;chains&quot;:[{&quot;chainId&quot;:&quot;_all_&quot;}]},&quot;triggers&quot;:{}},&quot;experiment&quot;:{&quot;ge3&quot;:&quot;ge3_10&quot;,&quot;ge2&quot;:&quot;ge2_1&quot;,&quot;searchAdvertPosition&quot;:&quot;1&quot;,&quot;growthSearch&quot;:&quot;s2&quot;,&quot;nwebQAGrowth&quot;:&quot;experiment&quot;,&quot;qawebRelatedReadingsContentControl&quot;:&quot;close&quot;,&quot;liveStore&quot;:&quot;ls_a1_b1_c1_f2&quot;,&quot;nwebSearch&quot;:&quot;nweb_search_heifetz&quot;,&quot;searchHybridTabs&quot;:&quot;pin-3#album-7&quot;,&quot;newSignBg&quot;:&quot;new&quot;,&quot;rt&quot;:&quot;y&quot;,&quot;isOffice&quot;:&quot;false&quot;,&quot;newLiveFeedMediacard&quot;:&quot;new&quot;,&quot;newMobileAppHeader&quot;:&quot;true&quot;,&quot;androidPassThroughPush&quot;:&quot;all&quot;,&quot;np&quot;:&quot;1&quot;,&quot;hybridZhmoreVideo&quot;:&quot;yes&quot;,&quot;nwebGrowthPeople&quot;:&quot;default&quot;,&quot;nwebSearchSuggest&quot;:&quot;default&quot;,&quot;qrcodeLogin&quot;:&quot;qrcode&quot;,&quot;isShowUnicomFreeEntry&quot;:&quot;unicom_free_entry_off&quot;,&quot;androidSearchTabStyle&quot;:&quot;search_tab_style_b&quot;,&quot;newMobileColumnAppheader&quot;:&quot;new_header&quot;,&quot;androidDbRecommendAction&quot;:&quot;open&quot;,&quot;searchTab&quot;:&quot;collapse&quot;,&quot;zcmLighting&quot;:&quot;zcm&quot;,&quot;androidDbFeedHashTagStyle&quot;:&quot;button&quot;,&quot;appStoreRateDialog&quot;:&quot;close&quot;,&quot;mobileFeedGuide&quot;:&quot;block&quot;,&quot;default&quot;:&quot;None&quot;,&quot;isNewNotiPanel&quot;:&quot;no&quot;,&quot;adR&quot;:&quot;a&quot;,&quot;uRe&quot;:&quot;0&quot;,&quot;androidProfilePanel&quot;:&quot;panel_b&quot;},&quot;experimentOrigin&quot;:{&quot;ge3&quot;:&quot;ge3_10&quot;,&quot;ge2&quot;:&quot;ge2_1&quot;,&quot;search_advert_position&quot;:&quot;1&quot;,&quot;growth_search&quot;:&quot;s2&quot;,&quot;nwebQAGrowth&quot;:&quot;experiment&quot;,&quot;qaweb_related_readings_content_control&quot;:&quot;close&quot;,&quot;live_store&quot;:&quot;ls_a1_b1_c1_f2&quot;,&quot;nweb_search&quot;:&quot;nweb_search_heifetz&quot;,&quot;search_hybrid_tabs&quot;:&quot;pin-3#album-7&quot;,&quot;new_sign_bg&quot;:&quot;new&quot;,&quot;rt&quot;:&quot;y&quot;,&quot;is_office&quot;:&quot;false&quot;,&quot;new_live_feed_mediacard&quot;:&quot;new&quot;,&quot;new_mobile_app_header&quot;:&quot;true&quot;,&quot;android_pass_through_push&quot;:&quot;all&quot;,&quot;np&quot;:&quot;1&quot;,&quot;hybrid_zhmore_video&quot;:&quot;yes&quot;,&quot;nweb_growth_people&quot;:&quot;default&quot;,&quot;nweb_search_suggest&quot;:&quot;default&quot;,&quot;qrcode_login&quot;:&quot;qrcode&quot;,&quot;is_show_unicom_free_entry&quot;:&quot;unicom_free_entry_off&quot;,&quot;android_search_tab_style&quot;:&quot;search_tab_style_b&quot;,&quot;new_mobile_column_appheader&quot;:&quot;new_header&quot;,&quot;android_db_recommend_action&quot;:&quot;open&quot;,&quot;search_tab&quot;:&quot;collapse&quot;,&quot;zcm-lighting&quot;:&quot;zcm&quot;,&quot;android_db_feed_hash_tag_style&quot;:&quot;button&quot;,&quot;app_store_rate_dialog&quot;:&quot;close&quot;,&quot;mobile_feed_guide&quot;:&quot;block&quot;,&quot;default&quot;:&quot;None&quot;,&quot;is_new_noti_panel&quot;:&quot;no&quot;,&quot;ad_r&quot;:&quot;a&quot;,&quot;u_re&quot;:&quot;0&quot;,&quot;android_profile_panel&quot;:&quot;panel_b&quot;},&quot;userAgent&quot;:{&quot;Edge&quot;:false,&quot;Wechat&quot;:false,&quot;Weibo&quot;:false,&quot;QQ&quot;:false,&quot;Mobile&quot;:false,&quot;Android&quot;:false,&quot;iOS&quot;:false,&quot;isAppleDevice&quot;:true,&quot;Zhihu&quot;:false,&quot;ZhihuHybrid&quot;:false,&quot;isBot&quot;:false,&quot;Tablet&quot;:false,&quot;UC&quot;:false,&quot;Sogou&quot;:false,&quot;Qihoo&quot;:false,&quot;Baidu&quot;:false,&quot;isWebView&quot;:false,&quot;origin&quot;:&quot;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.116 Safari/537.36&quot;},&quot;trafficSource&quot;:&quot;production&quot;,&quot;edition&quot;:{&quot;baidu&quot;:false,&quot;sogou&quot;:false,&quot;baiduBeijing&quot;:false,&quot;yidianzixun&quot;:false},&quot;theme&quot;:&quot;light&quot;,&quot;referer&quot;:&quot;&quot;,&quot;conf&quot;:{},&quot;ipInfo&quot;:{},&quot;logged&quot;:false},&quot;me&quot;:{&quot;accountInfoLoadStatus&quot;:{},&quot;organizationProfileStatus&quot;:{},&quot;columnContributions&quot;:[]},&quot;comments&quot;:{&quot;pagination&quot;:{},&quot;collapsed&quot;:{},&quot;reverse&quot;:{},&quot;reviewing&quot;:{},&quot;conversation&quot;:{},&quot;parent&quot;:{}},&quot;pushNotifications&quot;:{&quot;default&quot;:{&quot;isFetching&quot;:false,&quot;isDrained&quot;:false,&quot;ids&quot;:[]},&quot;follow&quot;:{&quot;isFetching&quot;:false,&quot;isDrained&quot;:false,&quot;ids&quot;:[]},&quot;vote_thank&quot;:{&quot;isFetching&quot;:false,&quot;isDrained&quot;:false,&quot;ids&quot;:[]},&quot;currentTab&quot;:&quot;default&quot;,&quot;notificationsCount&quot;:{&quot;default&quot;:0,&quot;follow&quot;:0,&quot;vote_thank&quot;:0}},&quot;messages&quot;:{&quot;data&quot;:{},&quot;currentTab&quot;:&quot;common&quot;,&quot;messageCount&quot;:0},&quot;register&quot;:{&quot;registerValidateSucceeded&quot;:null,&quot;registerValidateErrors&quot;:{},&quot;registerConfirmError&quot;:null,&quot;sendDigitsError&quot;:null,&quot;registerConfirmSucceeded&quot;:null},&quot;login&quot;:{&quot;loginUnregisteredError&quot;:false,&quot;loginBindWechatError&quot;:false,&quot;loginConfirmError&quot;:null,&quot;sendDigitsError&quot;:null,&quot;validateDigitsError&quot;:false,&quot;loginConfirmSucceeded&quot;:null,&quot;qrcodeLoginToken&quot;:&quot;&quot;,&quot;qrcodeLoginScanStatus&quot;:0,&quot;qrcodeLoginError&quot;:null,&quot;qrcodeLoginReturnNewToken&quot;:false},&quot;active&quot;:{&quot;sendDigitsError&quot;:null,&quot;activeConfirmSucceeded&quot;:null,&quot;activeConfirmError&quot;:null},&quot;switches&quot;:{},&quot;coupon&quot;:{&quot;isRedeemingCoupon&quot;:false},&quot;question&quot;:{&quot;followers&quot;:{},&quot;concernedFollowers&quot;:{},&quot;answers&quot;:{},&quot;hiddenAnswers&quot;:{},&quot;createdAnswers&quot;:{},&quot;collapsedAnswers&quot;:{},&quot;notificationAnswers&quot;:{},&quot;invitationCandidates&quot;:{},&quot;inviters&quot;:{},&quot;invitees&quot;:{},&quot;similarQuestions&quot;:{},&quot;relatedCommodities&quot;:{},&quot;recommendReadings&quot;:{},&quot;bio&quot;:{},&quot;brand&quot;:{},&quot;permission&quot;:{},&quot;advancedStyle&quot;:{},&quot;commonAnswerCount&quot;:0,&quot;hiddenAnswerCount&quot;:0,&quot;meta&quot;:{},&quot;autoInvitation&quot;:{},&quot;simpleConcernedFollowers&quot;:{}},&quot;shareTexts&quot;:{},&quot;answers&quot;:{&quot;voters&quot;:{},&quot;copyrightApplicants&quot;:{},&quot;favlists&quot;:{},&quot;newAnswer&quot;:{},&quot;concernedUpvoters&quot;:{},&quot;simpleConcernedUpvoters&quot;:{}},&quot;banner&quot;:{},&quot;topic&quot;:{&quot;bios&quot;:{},&quot;hot&quot;:{},&quot;newest&quot;:{},&quot;top&quot;:{},&quot;unanswered&quot;:{},&quot;questions&quot;:{},&quot;followers&quot;:{},&quot;parent&quot;:{},&quot;children&quot;:{},&quot;bestAnswerers&quot;:{},&quot;index&quot;:{},&quot;intro&quot;:{},&quot;meta&quot;:{},&quot;schema&quot;:{}},&quot;captcha&quot;:{&quot;captchaNeeded&quot;:false,&quot;captchaValidated&quot;:false,&quot;captchaBase64String&quot;:null,&quot;captchaValidationMessage&quot;:null,&quot;loginCaptchaExpires&quot;:false},&quot;sms&quot;:{&quot;supportedCountries&quot;:[]},&quot;explore&quot;:{&quot;recommendations&quot;:{}},&quot;articles&quot;:{&quot;voters&quot;:{}},&quot;favlists&quot;:{&quot;relations&quot;:{}},&quot;pins&quot;:{&quot;voters&quot;:{}},&quot;topstory&quot;:{&quot;topstorys&quot;:{&quot;isFetching&quot;:false,&quot;isDrained&quot;:false,&quot;afterId&quot;:0,&quot;items&quot;:[],&quot;next&quot;:null},&quot;sidebar&quot;:null,&quot;announcement&quot;:{},&quot;hotList&quot;:[],&quot;guestFeeds&quot;:{&quot;isFetching&quot;:false,&quot;isDrained&quot;:false,&quot;afterId&quot;:0,&quot;items&quot;:[],&quot;next&quot;:null}},&quot;upload&quot;:{},&quot;video&quot;:{&quot;data&quot;:{}},&quot;guide&quot;:{&quot;guide&quot;:{&quot;isFetching&quot;:false,&quot;isShowGuide&quot;:false}},&quot;reward&quot;:{&quot;answer&quot;:{},&quot;article&quot;:{},&quot;question&quot;:{}},&quot;search&quot;:{&quot;recommendSearch&quot;:[],&quot;topSearch&quot;:{},&quot;attachedInfo&quot;:{},&quot;nextOffset&quot;:{},&quot;generalByQuery&quot;:{},&quot;generalByQueryInADay&quot;:{},&quot;generalByQueryInAWeek&quot;:{},&quot;generalByQueryInThreeMonths&quot;:{},&quot;peopleByQuery&quot;:{},&quot;topicByQuery&quot;:{},&quot;columnByQuery&quot;:{},&quot;liveByQuery&quot;:{},&quot;albumByQuery&quot;:{},&quot;eBookByQuery&quot;:{}},&quot;creator&quot;:{&quot;tools&quot;:{&quot;question&quot;:{&quot;invitationCount&quot;:{&quot;questionFolloweeCount&quot;:0,&quot;questionTotalCount&quot;:0},&quot;goodatTopics&quot;:[]},&quot;customPromotion&quot;:{&quot;itemLists&quot;:{}}},&quot;explore&quot;:{&quot;academy&quot;:{&quot;tabs&quot;:[],&quot;article&quot;:{}}},&quot;rights&quot;:[],&quot;rightsStatus&quot;:{}},&quot;publicEditPermission&quot;:{}}" data-config="{&quot;apiAddress&quot;:&quot;/api/v4/&quot;,&quot;deployEnv&quot;:&quot;production&quot;}" data-useragent="{&quot;os&quot;:{&quot;name&quot;:&quot;Mac OS&quot;,&quot;version&quot;:&quot;10.11.4&quot;},&quot;browser&quot;:{&quot;name&quot;:&quot;Chrome&quot;,&quot;version&quot;:&quot;53.0.2785.116&quot;,&quot;major&quot;:&quot;53&quot;}}"></div><script src="https://static.zhihu.com/heifetz/vendor.caf889932b6061dcc35e.js"></script><script src="https://static.zhihu.com/heifetz/main.raven.d45641973a98a902cea1.js" defer=""></script><script src="https://static.zhihu.com/heifetz/main.app.cf660aebca0ff7adefa1.js"></script><script></script></body></html>
```

当然也可以通过 cookies 参数来设置，不过这样就需要构造 RequestsCookieJar 对象，而且需要分割一下 Cookies ，相对繁琐，不过效果是相同的，实例如下：

```text
import requests

cookies = 'q_c1=31653b264a074fc9a57816d1ea93ed8b|1474273938000|1474273938000; d_c0="AGDAs254kAqPTr6NW1U3XTLFzKhMPQ6H_nc=|1474273938"; __utmv=51854390.100-1|2=registration_date=20130902=1^3=entry_date=20130902=1;a_t="2.0AACAfbwdAAAXAAAAso0QWAAAgH28HQAAAGDAs254kAoXAAAAYQJVTQ4FCVgA360us8BAklzLYNEHUd6kmHtRQX5a6hiZxKCynnycerLQ3gIkoJLOCQ==";z_c0=Mi4wQUFDQWZid2RBQUFBWU1DemJuaVFDaGNBQUFCaEFsVk5EZ1VKV0FEZnJTNnp3RUNTWE10ZzBRZFIzcVNZZTFGQmZn|1474887858|64b4d4234a21de774c42c837fe0b672fdb5763b0'
jar = requests.cookies.RequestsCookieJar()
headers = {
    'Host': 'www.zhihu.com',
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.116 Safari/537.36'
}
for cookie in cookies.split(';'):
    key, value = cookie.split('=', 1)
    jar.set(key, value)
r = requests.get('http://www.zhihu.com', cookies=jar, headers=headers)
print(r.text)
```

首先新建了一个 RequestCookieJar 对象，然后将复制下来的 Cookies 利用 split\(\) 方法分割，利用 set\(\) 方法设置好每一个 Cookie 的 key 和 value，然后通过调用 Requests 的 get\(\) 方法并传递给 cookies 参数即可，当然由于知乎本身的限制， headers 参数也不能少，只不过不需要在原来的 headers 参数里面设置 Cookie 字段了

## 3. 会话维持 {#3-会话维持}

测试网址:[http://httpbin.org/cookies/set/number/123456789](http://httpbin.org/cookies/set/number/123456789)

解决这个问题的主要方法就是维持同一个会话，也就是相当于打开一个新的浏览器选项卡而不是新开一个浏览器。但是我又不想每次设置 Cookies，那该怎么办？这时候就有了新的利器 Session对象。

利用它，我们可以方便地维护一个会话，而且不用担心 Cookies 的问题，它会帮我们自动处理好

实例:

```text
import requests

requests.get("http://httpbin.org/cookies/set/number/123456789")
r = requests.get("http://httpbin.org/cookies")
print(r.text)
```

运行结果:

```text
{
  "cookies": {
  }
}
```

不能成功获取到设置的 Cookies

使用session测试

```text
import requests

s  = requests.Session()
s.get("http://httpbin.org/cookies/set/number/123456789")
r = s.get("http://httpbin.org/cookies")
print(r.text)
```

运行结果:

```text
{
  "cookies": {
    "number": "123456789"
  }
}
```

利用 Session 我们可以做到模拟同一个会话，而且不用担心 Cookies 的问题，通常用于模拟登录成功之后再进行下一步的操作

## 4. SSL证书验证 {#4-ssl证书验证}

测试网址:[https://www.12306.cn](https://www.12306.cn)

Requests 提供了证书验证的功能，当发送 HTTP 请求的时候，它会检查 SSL 证书，我们可以使用 verify 这个参数来控制是否检查此证书，其实如果不加的话默认是 True，会自动验证。

测试:

```text
import requests

response = requests.get("https://www.12306.cn")
print(response.status_code)
```

运行结果:

```text
requests.exceptions.SSLError: HTTPSConnectionPool(host='www.12306.cn', port=443): Max retries exceeded with url: / (Caused by SSLError(CertificateError("hostname 'www.12306.cn' doesn't match either of 'webssl.chinanetcenter.com', 'i.l.inmobicdn.net', '*.fn-mart.com', 'www.1zhe.com', '*.pinganfang.com', '*.anhouse.com', 'dl.jphbpk.gxpan.cn', 'dl.givingtales.gxpan.cn', 'dl.toyblast.gxpan.cn', 'dl.sds.gxpan.cn', 'download.ctrip.com', 'mh.tiancity.com', 'app.4399.cn', 'i.4399.cn', 'm.4399.cn', 'a.4399.cn', 'cdn.hxjyios.iwan4399.com', 'ios.hxjy.iwan4399.com', 'gjzx.gjzq.com.cn', 'f.3000test.com', 'tj.img4399.com', '*.zhe800.com', '*.qiyipic.com', '*.vxinyou.com', '*.gdjh.vxinyou.com', '*.3000.com', 'pay.game2.cn', 'static1.j.cn', 'static2.j.cn', 'static3.j.cn', 'static4.j.cn', 'video1.j.cn', 'video2.j.cn', 'video3.j.cn', 'online.j.cn', 'playback.live.j.cn', 'audio1.guang.j.cn', 'audio2.guang.j.cn', 'audio3.guang.j.cn', 'img1.guang.j.cn', 'img2.guang.j.cn', 'img3.guang.j.cn', 'img4.guang.j.cn', 'img5.guang.j.cn', 'img6.guang.j.cn', '*.4399youpai.com', 'w.tancdn.com', '*.3000api.com', 'static11.j.cn', '*.kuyinyun.com', '*.kuyin123.com', '*.diyring.cc', '3000test.com', '*.3000test.com', 'www.3387.com', 'bbs.4399.cn', '*.cankaoxiaoxi.com', '*.service.kugou.com', 'test.macauslot.com', 'testm.macauslot.com', 'testtran.macauslot.com', 'xiuxiu.huodong.meitu.com', '*.meitu.com', '*.meitudata.com', '*.wheetalk.com', '*.shanliaoapp.com', 'xiuxiu.web.meitu.com', 'api.account.meitu.com', 'open.web.meitu.com', 'id.api.meitu.com', 'api.makeup.meitu.com', 'im.live.meipai.com', '*.meipai.com', 'm.macauslot.com', 'www.macauslot.com', 'web.macauslot.com', 'translation.macauslot.com', 'img1.homekoocdn.com', 'cdn.homekoocdn.com', 'cdn1.homekoocdn.com', 'cdn2.homekoocdn.com', 'cdn3.homekoocdn.com', 'cdn4.homekoocdn.com', 'img.homekoocdn.com', 'img2.homekoocdn.com', 'img3.homekoocdn.com', 'img4.homekoocdn.com', '*.macauslot.com', '*.samsungapps.com', 'auto.tancdn.com', '*.winbo.top', 'static.bst.meitu.com', 'api.xiuxiu.meitu.com', 'api.photo.meituyun.com', 'h5.selfiecity.meitu.com', 'api.selfiecity.meitu.com', 'h5.beautymaster.meiyan.com', 'api.beautymaster.meiyan.com', 'www.yawenb.com', 'm.yawenb.com', 'www.biqugg.com', 'www.dawenxue.net', 'cpg.meitubase.com', 'www.qushuba.com', 'www.ranwena.com', 'www.u8xsw.com', '*.4399sy.com', 'ms.awqsaged.cn', 'fanxing2.kugou.com', 'fanxing.kugou.com', 'sso.56.com', 'upload.qf.56.com', 'sso.qianfan.tv', 'cdn.danmu.56.com', 'www-ppd.hermes.cn', 'www-uat.hermes.cn', 'www-ts2.hermes.cn', 'www-tst.hermes.cn', '*.syyx.com', 'img.wgeqr.cn', 'img.wgewa.cn', 'img.09mk.cn', 'img.85nh.cn', '*.zhuoquapp.com', 'img.dtmpekda8.cn', 'img.etmpekda6.cn', '*.5054399.com', '*.aiwan4399.com', 'user.beevideo.bestv.com.cn', '*.3839.com', '*.actdelivery.net', '*.4399.cn'",),))
```

提示一个错误，叫做 SSLError，证书验证错误。所以如果我们请求一个 HTTPS 站点，但是证书验证错误的页面时，就会报这样的错误

如何避免这个错误,只需把 verify 这个参数设置为 False 即可。

```text
import requests

response = requests.get("https://www.12306.cn",verify=False)
print(response.status_code)
```

运行结果:

```text
E:\Python36\lib\site-packages\urllib3\connectionpool.py:858: InsecureRequestWarning: Unverified HTTPS request is being made. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
  InsecureRequestWarning)
200
```

不过发现报了一个警告，它提示建议让我们给它指定证书。

可以通过设置忽略警告的方式来屏蔽这个警告：

```text
import requests
import urllib3

urllib3.disable_warnings()
response = requests.get("https://www.12306.cn",verify=False)
print(response.status_code)
```

运行结果:

```text
200
```

或者通过捕获警告到日志的方式忽略警告：

```text
import requests
import logging

logging.captureWarnings(True)
response = requests.get("https://www.12306.cn",verify=False)
print(response.status_code)
```

可以指定一个本地证书用作客户端证书，可以是单个文件（包含密钥和证书）或一个包含两个文件路径的元组

```text
import requests

response = requests.get('https://www.12306.cn',verify="E:/SRCA.crt")
print(response.status_code)
```

## 5. 代理设置 {#5-代理设置}

设置代理，在 Requests 中需要用到 proxies 这个参数

```text
import requests

# 代理池
proxies = {
    'http': 'http://10.10.1.10:3128',
    'https': 'http://10.10.1.10:1080',
}

r = requests.get('https://www.taobao.com',proxies=proxies)
print(r.status_code)
```

若代理需要使用 HTTP Basic Auth，可以使用类似[http://user:password@host:port](http://user:password@host:port/)这样的语法来设置代理

实例:

```text
import requests

proxies = {
    'https': 'http://user:password@10.10.1.10:3128/',
}
requests.get('https://www.taobao.com', proxies=proxies)
```

除了基本的 HTTP 代理，Requests 还支持 SOCKS 协议的代理。

需要安装 Socks 这个库，命令如下：

```text
pip3 install "requests[socks]"
```

然后就可以使用 SOCKS 协议代理了

```text
socks5://user:password@host:port
```

实例:

```text
import requests

proxies = {
    'http': 'socks5://user:password@host:port',
    'https': 'socks5://user:password@host:port'
}
requests.get('https://www.taobao.com', proxies=proxies)
```

## 6. 超时设置 {#6-超时设置}

设置超时时间需要用到 timeout 参数。这个时间的计算是发出 Request 到服务器返回 Response 的时间

```text
import requests

r = requests.get('https://www.taobao.com', timeout=1)
print(r.status_code)
```

通过这样的方式，我们可以将超时时间设置为 1 秒，如果 1 秒内没有响应，那就抛出异常。

实际上请求分为两个阶段，即 connect（连接）和 read（读取）。

上面的设置 timeout 值将会用作 connect 和 read 二者的 timeout 总和。

如果要分别指定，就可以传入一个元组：

```text
r = requests.get('https://www.taobao.com', timeout=(5, 11))
```

如果想永久等待，那么我们可以直接将 timeout 设置为 None，或者不设置直接留空，因为默认是 None。这样的话，如果服务器还在运行，但是响应特别慢，那就慢慢等吧，它永远不会返回超时错误的。

```text
r = requests.get('https://www.taobao.com', timeout=None)
或者
r = requests.get('https://www.taobao.com')
```

## 7. 身份认证 {#7-身份认证}

![](../../.gitbook/assets/3.2.2-1.png)有可能遇到这样的页面认证，可以使用Requests字典的身份认证功能

```text
import requests
from requests.auth import HTTPBasicAuth

r = requests.get('http://localhost:5000', auth=HTTPBasicAuth('username', 'password'))
print(r.status_code)
```

更简便的认证，可以直接传一个元组，它会默认使用 HTTPBasicAuth 这个类来认证

```text
import requests

r = requests.get('http://localhost:5000', auth=('username', 'password'))
print(r.status_code)
```

Requests 还提供了其他的认证方式，如 OAuth 认证，不过需要安装 oauth 包

```text
pip install requests_oauthlib
```

使用OAuth1方法认证

```text
import requests
from requests_oauthlib import OAuth1

url = 'https://api.twitter.com/1.1/account/verify_credentials.json'
auth = OAuth1('YOUR_APP_KEY', 'YOUR_APP_SECRET',
              'USER_OAUTH_TOKEN', 'USER_OAUTH_TOKEN_SECRET')
requests.get(url,auth=auth)
```

requests\_oauthlib官方文档:[https://requests-oauthlib.readthedocs.org/](https://requests-oauthlib.readthedocs.org/)

## 8. Prepared Request {#8-prepared-request}

实例:

```text
from requests import Request,Session

url = 'http://httpbin.org/post'
data = {
    'name':'angle',
}
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.116 Safari/537.36'
}
s = Session()
req = Request('POST',url,data=data,headers=headers)
prepped = s.prepare_request(req)
r = s.send(prepped)
print(r.text)
```

引入 Request，然后用 url、data、headers 参数构造了一个 Request 对象，需要再调用 Session 的 prepare\_request\(\) 方法将其转换为一个 Prepared Request 对象，然后调用 send\(\) 方法发送即可

运行结果:

```text
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "angle"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Content-Length": "10", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.116 Safari/537.36"
  }, 
  "json": null, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/post"
}
```

有了 Request 这个对象，就可以将一个个请求当做一个独立的对象来看待，这样在进行队列调度的时候会非常方便

## 9.相关链接

官方文档:[http://docs.python-requests.org/](http://docs.python-requests.org/)


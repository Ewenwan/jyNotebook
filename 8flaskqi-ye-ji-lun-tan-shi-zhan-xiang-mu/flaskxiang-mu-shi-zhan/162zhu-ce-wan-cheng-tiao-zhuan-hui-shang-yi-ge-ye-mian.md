隐藏文本

```
<span style="display: none;" id="return-to-span">{{ return_to }}</span>
```

获取隐藏的文本

```
var return_to = $('#return-to-span').text();
```

判断return\_to参数值

```
def get(self):
    return_to = request.referrer
    if return_to and return_to != request.url and safeutils.is_safe_url(return_to):
        return render_template('front/signup.html',return_to=return_to)
    else:
        return render_template('front/signup.html')
```

防止return\_to被利用跳转到其他页面，进行url判断

```
from urllib.parse import  urlparse,urljoin
from flask import request

def is_safe_url(target):
    ref_url = urlparse(request.host_url)
    print(request.host_url)
    test_url = urlparse(urljoin(request.host_url,target))
    return test_url.scheme in ('http','https') and ref_url.netloc == test_url.netloc
```




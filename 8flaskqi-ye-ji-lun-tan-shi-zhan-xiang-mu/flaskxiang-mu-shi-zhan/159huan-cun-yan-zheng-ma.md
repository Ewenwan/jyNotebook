利用memcached进行缓存验证码

```
@bp.route('/sms_captcha/',methods=['POST'])
def sms_captcha():
....
            zlcache.set(telephone,captcha)
....
        return restful.params_error(message="参数错误")


@bp.route('/captcha/')
def graph_captcha():
....
        zlcache.set(text.lower(),text.lower())
....
    return resp

```




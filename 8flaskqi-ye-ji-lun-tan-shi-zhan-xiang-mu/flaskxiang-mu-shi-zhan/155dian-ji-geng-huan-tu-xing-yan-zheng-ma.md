修改验证码的细节

```
.captcha-addon{
    padding:0;
    /*溢出隐藏*/
    overflow: hidden;
}

.captcha-img{
    width:94px;
    height:32px;
    cursor:pointer;
}

<span class="input-group-addon captcha-addon">
    <img id="captcha-img" class="captcha-img" src="{{ url_for('front.graph_captcha') }}" alt="">
</span>
```

参数替换

```
/**
 * Created by Administrator on 2017/3/24.
 */

var zlparam = {
    setParam: function (href,key,value) {
        // 重新加载整个页面
        var isReplaced = false;
        var urlArray = href.split('?');
        if(urlArray.length > 1){
            var queryArray = urlArray[1].split('&');
            for(var i=0; i < queryArray.length; i++){
                var paramsArray = queryArray[i].split('=');
                if(paramsArray[0] == key){
                    paramsArray[1] = value;
                    queryArray[i] = paramsArray.join('=');
                    isReplaced = true;
                    break;
                }
            }

            if(!isReplaced){
                var params = {};
                params[key] = value;
                if(urlArray.length > 1){
                    href = href + '&' + $.param(params);
                }else{
                    href = href + '?' + $.param(params);
                }
            }else{
                var params = queryArray.join('&');
                urlArray[1] = params;
                href = urlArray.join('?');
            }
        }else{
            var param = {};
            param[key] = value;
            if(urlArray.length > 1){
                href = href + '&' + $.param(param);
            }else{
                href = href + '?' + $.param(param);
            }
        }
        return href;
    }
};
```

点击更换图片url

```
$(function () {
    $('#captcha-img').click(function (event) {
        var self = $(this);
        var src = self.attr('src');
        var newsrc = zlparam.setParam(src,'r',Math.random())
        self.attr('src',newsrc);
    });
});
```




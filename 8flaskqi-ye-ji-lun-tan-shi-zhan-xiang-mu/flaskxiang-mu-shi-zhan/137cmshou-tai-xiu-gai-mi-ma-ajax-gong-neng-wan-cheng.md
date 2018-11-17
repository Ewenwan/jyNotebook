在页面不刷新的情况下，异步加载把数据传给服务器

```
// $ ==> JQuery
$(function () {

    $("#submit").click(function (even) {
        //阻止表单按钮的提交表单的事件
        even.preventAndSave();

        var oldpwdElement = $("input[name=oldpwd]");
        var newpwdElement = $("input[name=newpwd]");
        var newpwd2Element = $("input[name=newpwd2]");

        var oldpwd = oldpwdElement.val();
        var newpwd = newpwdElement.val();
        var newpwd2 = newpwd2Element.val();

        //1.要在模板的meta中渲染一个crsf_token
        //2.在ajax请求的头部中设置X-CSRFtolen
        zlajax.post({
            'url':'/cms/resetpwd/',
            'data':{
                'oldpwd':oldpwd,
                'newpwd':newpwd,
                'newpwd2':newpwd2,
            },
            'success':function (data) {
                console.log(data);
            },
            'fail':function (error) {
                console.log(error);
            }
        })

    });
});
```

对jquery的ajax的封装

```
/**
 * Created by hynev on 2017/11/10.
 */
// 对jquery的ajax的封装

'use strict';
var zlajax = {
    'get':function(args) {
        args['method'] = 'get';
        this.ajax(args);
    },
    'post':function(args) {
        args['method'] = 'post';
        this.ajax(args);
    },
    'ajax':function(args) {
        // 设置csrftoken
        this._ajaxSetup();
        $.ajax(args);
    },
    '_ajaxSetup': function() {
        $.ajaxSetup({
            'beforeSend':function(xhr,settings) {
                if (!/^(GET|HEAD|OPTIONS|TRACE)$/i.test(settings.type) && !this.crossDomain) {
                    var csrftoken = $('meta[name=csrf-token]').attr('content');
                    xhr.setRequestHeader("X-CSRFToken", csrftoken)
                }
            }
        });
    }
};
```




导入sweetalert相关的包

然后书写js，利用ajax异步加载时处理

```
// $ ==> JQuery
$(function () {

    $("#submit").click(function (even) {
        //阻止表单按钮的提交表单的事件
        even.preventDefault();

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
                if (data['code'] == 200) {
                zlalert.alertSuccessToast("密码成功");
                // 清除密码，如果还有文本存在，需要清理缓存
                oldpwdElement.val("");
                newpwdElement.val("");
                newpwd2Element.val("");
            }
                else{
                    var message = data["message"];
                    zlalert.alertInfo(message);
                }

            },
            'fail':function (error) {
                zlalert.alertNetworkError();
            }
        })

    });
});
```




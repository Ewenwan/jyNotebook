发送验证码按钮

```
<script src="{{ static("common/zlajax.js") }}"></script>
<link rel="stylesheet" href="{{ static("common/sweetalert/sweetalert.css") }}">
<script src="{{ static("common/sweetalert/sweetalert.min.js") }}"></script>
<script src="{{ static("common/sweetalert/zlalert.js") }}"></script>


<button  id="sms-captcha-btn" class="btn btn-default">
    发送验证码
</button>
```

js验证手机号码格式和ajax发送验证码、倒计时

```
$(function () {
    $('#sms-captcha-btn').click(function (event) {
        event.preventDefault();
        var self = $(this);
        var telephone = $("input[name='telephone']").val();
        if(!(/^1[345789]\d{9}$/.test(telephone))){
            zlalert.alertInfoToast("请输入正确的手机号码");
            return ;
        }
        zlajax.get({
            'url':'/c/sms_captcha?telephone='+telephone,
            'success':function (data) {
                // console.log(data)
                if (data['code'] == 200) {
                    zlalert.alertSuccessToast("短信验证码发送成功!");
                    self.attr('disabled', 'disabled');
                    //倒计时,每隔1秒执行1次
                    var timeCount = 6;
                    var timer = setInterval(function () {
                        timeCount--;
                        self.text(timeCount);
                        if (timeCount <= 0) {
                            self.removeAttr('disabled');
                            clearInterval(timer);
                            self.text("发送验证码");
                        }
                    }, 1000)
                }else{
                    zlalert.alertInfoToast(data["message"]);
                }
            }
        })
    })
})
```




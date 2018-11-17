js混淆网站:[https://www.sojson.com/jscodeconfusion.html](https://www.sojson.com/jscodeconfusion.html)

js加密，前端和后端指定同一加密规则

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
        var timestamp = (new Date).getTime();
        var sign = md5(timestamp+telephone+"A@^JIJw55a7832a@kddad@！&12=");
        zlajax.post({
            'url':'/c/sms_captcha/',
            'data':{
                'telephone':telephone,
                'timestamp':timestamp,
                'sign':sign,
            },
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

```
from apps.forms import BaseForm
from wtforms import StringField
from wtforms.validators import regexp,InputRequired
import hashlib
class SMSCaptchaForm(BaseForm):
    salt = "A@^JIJw55a7832a@kddad@！&12="
    telephone = StringField(validators=[regexp(r'^1[345789]\d{9}')])
    timestamp = StringField(validators=[regexp(r'\d{13}')])
    sign = StringField(validators=[InputRequired()])

    def validate(self):
        result = super(SMSCaptchaForm,self).validate()
        if not result:
            return False
        telephone = self.telephone.data
        timestamp = self.timestamp.data
        sign = self.sign.data
        # md5(timestamp+telephone+salt)
        # md5函数必须要传入一个bytes类型的字符串进去
        # 从md5对象中获取字符串需要调用hexdigest()方法
        sign2 = hashlib.md5((timestamp+telephone+self.salt).encode('utf-8')).hexdigest()
        print("客户端提交的",sign)
        print("服务器提交的",sign2)
        if sign == sign2:
            return True
        else:
            False
```

视图以post方法重写

```
@bp.route('/sms_captcha/',methods=['POST'])
def sms_captcha():
    # telephone
    # timestamp
    # md5(ts+telephone+salt)
    form = SMSCaptchaForm(request.form)
    if form.validate():
        telephone = form.telephone.data
        captcha = Captcha.gene_text(4)
        if demo_sms_send.send_api(telephone,code=captcha):
            return restful.success()
        else:
            return restful.params_error(message="短信验证码发送失败！")
    else:
        return restful.params_error(message="参数错误")
```

由于考虑安全性，需要对js进行混淆

网址:[https://www.sojson.com/jscodeconfusion.html](https://www.sojson.com/jscodeconfusion.html)

混淆后的js文件

一般操作是先加密再混淆

```
window["\x65\x76\x61\x6c"](function(WSPoHOSkF1,Akgo2,L3,vqX4,migsoYcRM5,$gG6){migsoYcRM5=function(L3){return L3['\x74\x6f\x53\x74\x72\x69\x6e\x67'](36)};if('\x30'['\x72\x65\x70\x6c\x61\x63\x65'](0,migsoYcRM5)==0){while(L3--)$gG6[migsoYcRM5(L3)]=vqX4[L3];vqX4=[function(migsoYcRM5){return $gG6[migsoYcRM5]||migsoYcRM5}];migsoYcRM5=function(){return'\x5b\x32\x2d\x35\x37\x38\x61\x62\x65\x2d\x6b\x5d'};L3=1};while(L3--)if(vqX4[L3])WSPoHOSkF1=WSPoHOSkF1['\x72\x65\x70\x6c\x61\x63\x65'](new window["\x52\x65\x67\x45\x78\x70"]('\\\x62'+migsoYcRM5(L3)+'\\\x62','\x67'),vqX4[L3]);return WSPoHOSkF1}('\x24\x28\x35\x28\x29\x7b\x24\x28\'\x23\x73\x6d\x73\x2d\x63\x61\x70\x74\x63\x68\x61\x2d\x62\x74\x6e\'\x29\x2e\x63\x6c\x69\x63\x6b\x28\x35\x28\x68\x29\x7b\x68\x2e\x70\x72\x65\x76\x65\x6e\x74\x44\x65\x66\x61\x75\x6c\x74\x28\x29\x3b\x32 \x34\x3d\x24\x28\x74\x68\x69\x73\x29\x3b\x32 \x33\x3d\x24\x28\x22\x69\x6e\x70\x75\x74\x5b\x6e\x61\x6d\x65\x3d\'\x33\'\x5d\x22\x29\x2e\x76\x61\x6c\x28\x29\x3b\x62\x28\x21\x28\x2f\x5e\x31\x5b\x33\x34\x35\x37\x38\x39\x5d\\\x64\x7b\x39\x7d\x24\x2f\x2e\x74\x65\x73\x74\x28\x33\x29\x29\x29\x7b\x65\x2e\x69\x28\x22\u8bf7\u8f93\u5165\u6b63\u786e\u7684\u624b\u673a\u53f7\u7801\x22\x29\x3b\x72\x65\x74\x75\x72\x6e\x7d\x32 \x37\x3d\x28\x6e\x65\x77 \x44\x61\x74\x65\x29\x2e\x67\x65\x74\x54\x69\x6d\x65\x28\x29\x3b\x32 \x66\x3d\x6d\x64\x35\x28\x37\x2b\x33\x2b\x22\x41\x40\x5e\x4a\x49\x4a\x77\x35\x35\x61\x37\x38\x33\x32\x61\x40\x6b\x64\x64\x61\x64\x40\uff01\x26\x31\x32\x3d\x22\x29\x3b\x7a\x6c\x61\x6a\x61\x78\x2e\x70\x6f\x73\x74\x28\x7b\'\x75\x72\x6c\'\x3a\'\x2f\x63\x2f\x73\x6d\x73\x5f\x63\x61\x70\x74\x63\x68\x61\x2f\'\x2c\'\x38\'\x3a\x7b\'\x33\'\x3a\x33\x2c\'\x37\'\x3a\x37\x2c\'\x66\'\x3a\x66\x2c\x7d\x2c\'\x73\x75\x63\x63\x65\x73\x73\'\x3a\x35\x28\x38\x29\x7b\x62\x28\x38\x5b\'\x63\x6f\x64\x65\'\x5d\x3d\x3d\x32\x30\x30\x29\x7b\x65\x2e\x61\x6c\x65\x72\x74\x53\x75\x63\x63\x65\x73\x73\x54\x6f\x61\x73\x74\x28\x22\u77ed\u4fe1\u9a8c\u8bc1\u7801\u53d1\u9001\u6210\u529f\x21\x22\x29\x3b\x34\x2e\x61\x74\x74\x72\x28\'\x67\'\x2c\'\x67\'\x29\x3b\x32 \x61\x3d\x36\x3b\x32 \x6a\x3d\x73\x65\x74\x49\x6e\x74\x65\x72\x76\x61\x6c\x28\x35\x28\x29\x7b\x61\x2d\x2d\x3b\x34\x2e\x6b\x28\x61\x29\x3b\x62\x28\x61\x3c\x3d\x30\x29\x7b\x34\x2e\x72\x65\x6d\x6f\x76\x65\x41\x74\x74\x72\x28\'\x67\'\x29\x3b\x63\x6c\x65\x61\x72\x49\x6e\x74\x65\x72\x76\x61\x6c\x28\x6a\x29\x3b\x34\x2e\x6b\x28\x22\u53d1\u9001\u9a8c\u8bc1\u7801\x22\x29\x7d\x7d\x2c\x31\x30\x30\x30\x29\x7d\x65\x6c\x73\x65\x7b\x65\x2e\x69\x28\x38\x5b\x22\x6d\x65\x73\x73\x61\x67\x65\x22\x5d\x29\x7d\x7d\x7d\x29\x7d\x29\x7d\x29',[],21,'\x7c\x7c\x76\x61\x72\x7c\x74\x65\x6c\x65\x70\x68\x6f\x6e\x65\x7c\x73\x65\x6c\x66\x7c\x66\x75\x6e\x63\x74\x69\x6f\x6e\x7c\x7c\x74\x69\x6d\x65\x73\x74\x61\x6d\x70\x7c\x64\x61\x74\x61\x7c\x7c\x74\x69\x6d\x65\x43\x6f\x75\x6e\x74\x7c\x69\x66\x7c\x7c\x7c\x7a\x6c\x61\x6c\x65\x72\x74\x7c\x73\x69\x67\x6e\x7c\x64\x69\x73\x61\x62\x6c\x65\x64\x7c\x65\x76\x65\x6e\x74\x7c\x61\x6c\x65\x72\x74\x49\x6e\x66\x6f\x54\x6f\x61\x73\x74\x7c\x74\x69\x6d\x65\x72\x7c\x74\x65\x78\x74'['\x73\x70\x6c\x69\x74']('\x7c'),0,{}))
```




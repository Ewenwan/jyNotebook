### 1.相关链接

阿里大于API文档:[https://api.alidayu.com/docs/api.htm?spm=a3142.7629065.4.7.tg21p0&apiId=25450](https://api.alidayu.com/docs/api.htm?spm=a3142.7629065.4.7.tg21p0&apiId=25450)

短信服务:[https://dysms.console.aliyun.com/dysms.htm?spm=a3142.8039393.0.0.41b81fd2jo7ezh\#/overview](https://dysms.console.aliyun.com/dysms.htm?spm=a3142.8039393.0.0.41b81fd2jo7ezh#/overview)

接口:[https://help.aliyun.com/document\_detail/55491.html?spm=a2c4g.11186623.6.568.XFNNA9](https://help.aliyun.com/document_detail/55491.html?spm=a2c4g.11186623.6.568.XFNNA9)

### 2.阿里大于短信验证码介绍

* 阿里大于是一个通信平台，通过这个平台，中小企业开发者可以在最短的时间内实现短信验证码发送，短信服务提醒，语音验证码，语音服务通知，IVR及呼叫中心，码号，后向流量，隐私保护相关的能力，实现互联网电信化
* 官网:[https://www.alidayu.com/](https://www.alidayu.com/)

### 3.操作

## 发送短信接口\(SendSms\) {#h2--sendsms-1}

#### 步骤 1 创建阿里云账号 {#h4--1-}

为了访问短信服务，您需要有一个阿里云账号。如果没有，可首先按照如下步骤创建阿里云账号：

1. 访问阿里云[官方网站](https://www.aliyun.com/?spm=a2c4g.11186623.2.3.qcwY5l)，单击页面上的 免费注册 按钮。
2. 按照屏幕提示完成注册流程并进行实名认证，短信服务只支持实名认证用户使用。为了更好地使用阿里云服务，建议尽快完成实名认证，否则部分阿里云服务将无法使用。具体实名认证流程，请参考[这里](https://help.aliyun.com/knowledge_detail/37171.html?spm=a2c4g.11186623.2.4.qcwY5l)。

#### 步骤 2 获取阿里云访问密钥 {#h4--2-}

为了使用短信发送API-Python SDK，您必须申请阿里云的访问密钥。

阿里云访问秘钥是阿里云为用户使用 API（非控制台）来访问其云资源设计的“安全口令”。您可以用它来签名 API 请求内容以通过服务端的安全验证。

该访问秘钥成对（AccessKeyId 与 AccessKeySecret）生成和使用。每个阿里云用户可以创建多对访问秘钥，且可随时启用（Active）、禁用（Inactive）或者删除已经生成的访问秘钥对。

您可以通过阿里云控制台的[秘钥管理页面](https://ak-console.aliyun.com/?spm=a2c4g.11186623.2.5.qcwY5l#/accesskey)创建、管理所有的访问秘钥对，且保证它处于“启用”状态。由于访问秘钥是阿里云对 API 请求进行安全验证的关键因子，请妥善保管你的访问秘钥。如果某些秘钥对出现泄漏风险，建议及时删除该秘钥对并生成新的替代秘钥对。

#### 步骤 3 在控制台完成模板与签名的申请，获得调用接口必备的参数 {#h4--3-}

**短信签名**

根据用户属性来创建符合自身属性的签名信息。企业用户需要上传相关企业资质证明，个人用户需要上传证明个人身份的证明。

_短信签名需要审核通过后才可以使用。_

**短信模板**

短信模板，即具体发送的短信内容。

短信模板可以支持验证码、短信通知、推广短信、国际/港澳台消息四种模式。验证码和短信通知，通过变量替换实现个性短信定制。推广短信不支持在模板中添加变量。国际/港澳台消息只能使用国际/港澳台短信模版发送短信。

_短信模板需要审核通过后才可以使用。_

**为了成功发送一条短信通知，您至少需要完成以下步骤**

一、在控制台完成短信签名与短信模板的申请，获得调用接口必备的参数

在“短信签名”页面完成签名的申请，获得短信签名的字符串[签名申请手册](https://help.aliyun.com/document_detail/55327.html?spm=a2c4g.11186623.2.6.qcwY5l)

在“短信模板”页面完成模板的申请，获得模板ID。[模板申请手册](https://help.aliyun.com/document_detail/55330.html?spm=a2c4g.11186623.2.7.qcwY5l)

#### 入参列表 {#h4-u5165u53C2u5217u8868}

| 参数名称 | 参数类型 | 必填与否 | 样例取值 | 参数说明 |
| :--- | :--- | :--- | :--- | :--- |
| PhoneNumbers | String | 必须 | 15000000000 | 短信接收号码。支持以逗号分隔的形式进行批量调用，批量上限为1000个手机号码,批量调用相对于单条调用及时性稍有延迟,验证码类型的短信推荐使用单条调用的方式，发送国际/港澳台消息时，接收号码格式为00+国际区号+号码，如“0085200000000” |
| SignName | String | 必须 | 云通信 | 短信签名 |
| TemplateCode | String | 必须 | SMS\_0000 | 短信模板ID，发送国际/港澳台消息时，请使用国际/港澳台短信模版 |
| TemplateParam | String | 可选 | {“code”:”1234”,”product”:”ytx”} | 短信模板变量替换JSON串,友情提示:如果JSON中需要带换行符,请参照标准的JSON协议对换行符的要求,比如短信内容中包含\r\n的情况在JSON中需要表示成\r\n,否则会导致JSON在服务端解析失败 |
| OutId | String | 可选 | abcdefgh | 外部流水扩展字段 |

#### 出参列表 {#h4-u51FAu53C2u5217u8868}

| 出参名称 | 出参类型 | 样例取值 | 参数说明 |
| :--- | :--- | :--- | :--- |
| RequestId | String | 8906582E-6722 | 请求ID |
| Code | String | OK | 状态码-返回OK代表请求成功,其他错误码详见错误码列表 |
| Message | String | 请求成功 | 状态码的描述 |
| BizId | String | 134523^4351232 | 发送回执ID,可根据该ID查询具体的发送状态 |

#### 技术对接步骤 {#h4-u6280u672Fu5BF9u63A5u6B65u9AA4}

* python版本要求：python 2.6+, python3.x
* SDK下载：[下载地址](https://help.aliyun.com/document_detail/55359.html)

* 执行：

  * 安装依赖：进入根目录执行命令： python setup.py install \#如果为python3，请执行：python3 setup.py install
  * 修改信息：从阿里云控制台上获取ACCESS\_KEY\_ID与ACCESS\_KEY\_SECRET，并填入文件const.py中
  * 运行程序：python demo\_sms\_send.py \#如果为python3，请执行python3 demo\_sms\_send.py
  * `注意：您还需要在控制台上申请短信模板，并将相关信息填入至文件demo_sms_send.py中`

#### 错误码列表 {#h4-u9519u8BEFu7801u5217u8868}

| Code | 描述 |
| :--- | :--- |
| OK | 请求成功 |
| isp.RAM\_PERMISSION\_DENY | RAM权限DENY |
| isv.OUT\_OF\_SERVICE | 业务停机 |
| isv.PRODUCT\_UN\_SUBSCRIPT | 未开通云通信产品的阿里云客户 |
| isv.PRODUCT\_UNSUBSCRIBE | 产品未开通 |
| isv.ACCOUNT\_NOT\_EXISTS | 账户不存在 |
| isv.ACCOUNT\_ABNORMAL | 账户异常 |
| isv.SMS\_TEMPLATE\_ILLEGAL | 短信模板不合法 |
| isv.SMS\_SIGNATURE\_ILLEGAL | 短信签名不合法 |
| isv.INVALID\_PARAMETERS | 参数异常 |
| isp.SYSTEM\_ERROR | 系统错误 |
| isv.MOBILE\_NUMBER\_ILLEGAL | 非法手机号 |
| isv.MOBILE\_COUNT\_OVER\_LIMIT | 手机号码数量超过限制 |
| isv.TEMPLATE\_MISSING\_PARAMETERS | 模板缺少变量 |
| isv.BUSINESS\_LIMIT\_CONTROL | 业务限流 |
| isv.INVALID\_JSON\_PARAM | JSON参数不合法，只接受字符串值 |
| isv.BLACK\_KEY\_CONTROL\_LIMIT | 黑名单管控 |
| isv.PARAM\_LENGTH\_LIMIT | 参数超出长度限制 |
| isv.PARAM\_NOT\_SUPPORT\_URL | 不支持URL |
| isv.AMOUNT\_NOT\_ENOUGH | 账户余额不足 |

**注：查询所有错误码及解决办法请点击**[短信接口调用错误码](https://help.aliyun.com/knowledge_detail/57717.html?spm=5176.doc55322.6.583.l6PFQ7)

#### 时间戳格式： {#h4--}

格式为：yyyy-MM-dd’T’HH:mm:ss’Z’；时区为：GMT

### 4.实例

下载zip文件后，打开后改写一下demo\_sms\_send.py

```
# -*- coding: utf-8 -*-
import sys
from utils.sms.aliyunsdkdysmsapi.request.v20170525 import SendSmsRequest
from utils.sms.aliyunsdkdysmsapi.request.v20170525 import QuerySendDetailsRequest
from aliyunsdkcore.client import AcsClient
import uuid
from aliyunsdkcore.profile import region_provider
from aliyunsdkcore.http import method_type as MT
from aliyunsdkcore.http import format_type as FT
from  utils.sms import const
import json

"""
短信业务调用接口示例，版本号：v20170525

Created on 2017-06-12

"""

# 注意：不要更改
REGION = "cn-hangzhou"
PRODUCT_NAME = "Dysmsapi"
DOMAIN = "dysmsapi.aliyuncs.com"

acs_client = AcsClient(const.ACCESS_KEY_ID, const.ACCESS_KEY_SECRET, REGION)
region_provider.add_endpoint(PRODUCT_NAME, REGION, DOMAIN)

def send_sms(business_id, phone_numbers, sign_name, template_code, template_param=None):
    smsRequest = SendSmsRequest.SendSmsRequest()
    # 申请的短信模板编码,必填
    smsRequest.set_TemplateCode(template_code)

    # 短信模板变量参数
    if template_param is not None:
        smsRequest.set_TemplateParam(template_param)

    # 设置业务请求流水号，必填。
    smsRequest.set_OutId(business_id)

    # 短信签名
    smsRequest.set_SignName(sign_name)

    # 数据提交方式
    # smsRequest.set_method(MT.POST)

    # 数据提交格式
    smsRequest.set_accept_format(FT.JSON)

    # 短信发送的号码列表，必填。
    smsRequest.set_PhoneNumbers(phone_numbers)

    # 调用短信发送接口，返回json
    smsResponse = acs_client.do_action_with_exception(smsRequest)

    # TODO 业务处理

    return smsResponse



def send_api(phone=None,code=None):
    try:
        __business_id = uuid.uuid1()
        #print(__business_id)
        params = r'{"code":"%s"}' % code
        # print(params)
        #params = u'{"name":"wqb","code":"12345678","address":"bz","phone":"13000000000"}'
        response = send_sms(__business_id, phone, const.SIGN_NAME,const.TEMPLATE_CODE, params).decode('utf-8')
        print(response,phone,code)
        response = json.loads(response)
        if response['Code']  == 'OK':
            return True
        else:
            return False
    except:
        return False
```

短信接口视图

```
@bp.route('/sms_captcha/')
def sms_captcha():
    result = demo_sms_send.send_api("18892332606","18892332606")
    if result:
        return "发送成功"
    else:
        return "发送失败"
```




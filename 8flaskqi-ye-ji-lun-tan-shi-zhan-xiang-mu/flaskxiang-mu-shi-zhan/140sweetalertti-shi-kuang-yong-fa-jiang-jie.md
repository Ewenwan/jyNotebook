### 1.相关链接

SweetAlert中文文档:[http://mishengqiang.com/sweetalert/](http://mishengqiang.com/sweetalert/)

官方文档:[https://sweetalert.js.org/docs/](https://sweetalert.js.org/docs/)

### 2.实例:

封装sweetalert

xtalert.js

```
/**
 * Created by Administrator on 2016/12/14.
 */

var xtalert = {
    /*
        功能：提示错误
        参数：
            - msg：提示的内容（可选）
    */
    'alertError': function (msg) {
        swal('提示',msg,'error');
    },
    /*
        功能：信息提示
        参数：
            - msg：提示的内容（可选）
    */
    'alertInfo':function (msg) {
        swal('提示',msg,'warning');
    },
    /*
        功能：可以自定义标题的信息提示
        参数：
            - msg：提示的内容（可选）
    */
    'alertInfoWithTitle': function (title,msg) {
        swal(title,msg);
    },
    /*
        功能：成功的提示
        参数：
            - msg：提示的内容（必须）
            - confirmCallback：确认按钮的执行事件（可选）
    */
    'alertSuccess':function (msg,confirmCallback) {
        args = {
            'title': '提示',
            'text': msg,
            'type': 'success',
        }
        swal(args,confirmCallback);
    }, 
    /*
        功能：带有标题的成功提示
        参数：
            - title：提示框的标题（必须）
            - msg：提示的内容（必须）
    */
    'alertSuccessWithTitle':function (title,msg) {
        swal(title,msg,'success');
    },
    /*
        功能：确认提示
        参数：字典的形式
            - title：提示框标题（可选）
            - type：提示框的类型（可选）
            - confirmText：确认按钮文本（可选）
            - cancelText：取消按钮文本（可选）
            - msg：提示框内容（必须）
            - confirmCallback：确认按钮点击回调（可选）
            - cancelCallback：取消按钮点击回调（可选）
    */
    'alertConfirm':function (params) {
        swal({
            'title': params['title'] ? params['title'] : '提示',
            'showCancelButton': true,
            'showConfirmButton': true,
            'type': params['type'] ? params['type'] : '',
            'confirmButtonText': params['confirmText'] ? params['confirmText'] : '确定',
            'cancelButtonText': params['cancelText'] ? params['cancelText'] : '取消',
            'text': params['msg'] ? params['msg'] : ''
        },function (isConfirm) {
            if(isConfirm){
                if(params['confirmCallback']){
                    params['confirmCallback']();
                }
            }else{
                if(params['cancelCallback']){
                    params['cancelCallback']();
                }
            }
        });
    },
    /*
        功能：带有一个输入框的提示
        参数：字典的形式
            - title：提示框的标题（可选）
            - text：提示框的内容（可选）
            - placeholder：输入框的占位文字（可选）
            - confirmText：确认按钮文字（可选）
            - cancelText：取消按钮文字（可选）
            - confirmCallback：确认后的执行事件
    */
    'alertOneInput': function (params) {
        swal({
            'title': params['title'] ? params['title'] : '请输入',
            'text': params['text'] ? params['text'] : '',
            'type':'input',
            'showCancelButton': true,
            'animation': 'slide-from-top',
            'closeOnConfirm': false,
            'showLoaderOnConfirm': true,
            'inputPlaceholder': params['placeholder'] ? params['placeholder'] : '',
            'confirmButtonText': params['confirmText'] ? params['confirmText'] : '确定',
            'cancelButtonText': params['cancelText'] ? params['cancelText'] : '取消',
        },function (inputValue) {
            if(inputValue === false) return false;
            if(inputValue === ''){
                swal.showInputError('输入框不能为空！');
                return false;
            }
            if(params['confirmCallback']){
                params['confirmCallback'](inputValue);
            }
        });
    },
    /*
        功能：网络错误提示
        参数：无
    */
    'alertNetworkError':function () {
        this.alertErrorToast('网络错误');
    },
    /*
        功能：信息toast提示（1s后消失）
        参数：
            - msg：提示消息
    */
    'alertInfoToast':function (msg) {
        this.alertToast(msg,'info');
    },
    /*
        功能：错误toast提示（1s后消失）
        参数：
            - msg：提示消息
    */
    'alertErrorToast':function (msg) {
        this.alertToast(msg,'error');
    },
    /*
        功能：成功toast提示（1s后消失）
        参数：
            - msg：提示消息
    */
    'alertSuccessToast':function (msg) {
        if(!msg){msg = '成功！';}
        this.alertToast(msg,'success');
    },
    /*
        功能：弹出toast（1s后消失）
        参数：
            - msg：提示消息
            - type：toast的类型
    */
    'alertToast':function (msg,type) {
        swal({
            'title': msg,
            'text': '',
            'type': type,
            'showCancelButton': false,
            'showConfirmButton': false,
            'timer': 1000,
        });
    },
    // 关闭当前对话框
    'close': function () {
        swal.close();
    }
};
```

index.html

```
<!DOCTYPE html>
<html>
<head>
    <title>sweetalert用法</title>
    <link rel="stylesheet" href="sweetalert/sweetalert.css"/>
    <script src="sweetalert/sweetalert.min.js"></script>
    <script type="text/javascript" src="sweetalert/xtalert.js"></script>
</head>
<body>
    <button id="btn1">错误提示</button>
    <script type="text/javascript">
        var btn = document.getElementById("btn1");
        btn.onclick = function(){
            xtalert.alertError("不能删除板块")
        }
    </script>

    <button id="btn2">消息提示</button>
    <script type="text/javascript">
        var btn = document.getElementById("btn2");
        btn.onclick = function(){
            xtalert.alertInfo("当前用户没有权限")
        }
    </script>

    <button id="btn3">成功提示</button>
    <script type="text/javascript">
        var btn = document.getElementById("btn3");
        btn.onclick = function(){
            xtalert.alertSuccess("发表成功")
        }
    </script>

    <button id="btn4">成功提示</button>
    <script type="text/javascript">
        var btn = document.getElementById("btn4");
        btn.onclick = function(){
            xtalert.alertConfirm({
                "confirmText":"再发一篇",
                "cancelText":"回到首页",
                "text":"文章发表成功",
                "confirmCallback":function(){
                    alert("点击了确认按钮")
                },
                "cancelCallback":function(){
                    alert("点击了取消按钮")
                }
            })
        }
    </script>

    <button id="btn5">输入框</button>
    <script type="text/javascript">
        var btn = document.getElementById("btn5");
        btn.onclick = function(){
            xtalert.alertOneInput({
                'title':"提示(输入)",
                "text":"添加新版块",
                "placeholder":"输入版块名称",
                "confirmText":"确认",
                "cancelText":"取消",
                "confirmCallback":function(inputValue){
                    alert("输入了"+inputValue)
                }
            })
        }
    </script>


    <button id="btn6">提示框</button>
    <script type="text/javascript">
        var btn = document.getElementById("btn6");
        btn.onclick = function(){
            xtalert.alertSuccessToast("修改成功")
        }
    </script>    
</body>
</html>
```




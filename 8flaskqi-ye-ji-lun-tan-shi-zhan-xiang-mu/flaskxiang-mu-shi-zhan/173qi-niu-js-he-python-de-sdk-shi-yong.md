### 在网站中使用七牛存储文件

#### 安装sdk

```
pip install qiniu
```

#### 编写获取uptoken的接口

```
@app.route('/uptoken/')
def uptoken():
    # AK
    access_key = "xxxxxxx"
    # SK
    secret_key = "xxxxxxx"
    # 验证
    q = qiniu.Auth(access_key,secret_key)
    # 储存空间名字
    bucket = "tokimeki"
    token = q.upload_token(bucket)
    return jsonify({"uptoken":token})
```

![](/assets/173-01.png)

在前端中添加js的sdk:七牛为javascript提供了一个专门用来传文件的接口

```
    <script src="https://cdn.staticfile.org/Plupload/2.1.1/moxie.js"></script>
    <script src="https://cdn.staticfile.org/Plupload/2.1.1/plupload.dev.js"></script>
    <script src="https://cdn.staticfile.org/qiniu-js-sdk/1.0.14-beta/qiniu.js"></script>
```

在前段添加zlqiniu.js，js文件封装了七牛的初始化和配置相关的参数

```
<script src{{ url_for('static',filename='zlqiniu.js') }}""></script>
```

zlqiniu.js

```
'use strict';

var zlqiniu = {
    'setUp': function(args) {
        var domain = args['domain'];
        var params = {
            browse_button:args['browse_btn'],
            runtimes: 'html5,flash,html4', //上传模式，依次退化
            max_file_size: '500mb', //文件最大允许的尺寸
            dragdrop: false, //是否开启拖拽上传
            chunk_size: '4mb', //分块上传时，每片的大小
            uptoken_url: args['uptoken_url'], //ajax请求token的url
            domain: domain, //图片下载时候的域名
            get_new_uptoken: false, //是否每次上传文件都要从业务服务器获取token
            auto_start: true, //如果设置了true,只要选择了图片,就会自动上传
            unique_names: true,
            multi_selection: false,
            filters: {
                mime_types :[
                    {title:'Image files',extensions: 'jpg,gif,png'},
                    {title:'Video files',extensions: 'flv,mpg,mpeg,avi,wmv,mov,asf,rm,rmvb,mkv,m4v,mp4'}
                ]
            },
            log_level: 5, //log级别
            init: {
                'FileUploaded': function(up,file,info) {
                    if(args['success']){
                        var success = args['success'];
                        file.name = domain + file.target_name;
                        success(up,file,info);
                    }
                },
                'Error': function(up,err,errTip) {
                    if(args['error']){
                        var error = args['error'];
                        error(up,err,errTip);
                    }
                },
                'UploadProgress': function (up,file) {
                    if(args['progress']){
                        args['progress'](up,file);
                    }
                },
                'FilesAdded': function (up,files) {
                    if(args['fileadded']){
                        args['fileadded'](up,files);
                    }
                },
                'UploadComplete': function () {
                    if(args['complete']){
                        args['complete']();
                    }
                }
            }
        };

        // 把args中的参数放到params中去
        for(var key in args){
            params[key] = args[key];
        }
        var uploader = Qiniu.uploader(params);
        return uploader;
    }
};
```

初始化七牛:使用以下代码初始化七牛，配置一些参数

```
        window.onload = function () {
            zlqiniu.setUp({
                /*http://7xqenu.coml.z0.glb.clouddn.com/*/
                'domain': 'http://pdhjzz2pa.bkt.clouddn.com/',
                'browse_btn': 'upload-btn',
                'uptoken_url': '/uptoken/',
                'success': function (up,file,info) {
                    console.log(info)
                }
            });
        }
```

参数解释:

* browser\_btn:按钮id
* uptoken\_url:uptoken的视图url
* domain:域名

---

index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="https://cdn.staticfile.org/Plupload/2.1.1/moxie.js"></script>
    <script src="https://cdn.staticfile.org/Plupload/2.1.1/plupload.dev.js"></script>
    <script src="https://cdn.staticfile.org/qiniu-js-sdk/1.0.14-beta/qiniu.js"></script>
    <script src="{{ url_for('static',filename='zlqiniu.js') }}"></script>
    <script>
        window.onload = function () {
            zlqiniu.setUp({
                /*http://7xqenu.coml.z0.glb.clouddn.com/*/
                'domain': 'http://pdhjzz2pa.bkt.clouddn.com/',
                'browse_btn': 'upload-btn',
                'uptoken_url': '/uptoken/',
                'success': function (up,file,info) {
                    var image_url = file.name
                    var imageInput = document.getElementById("image-input");
                    imageInput.value = image_url;

                    var im = document.getElementById("img");
                    im.setAttribute("src",image_url);

                }
            });
        }
    </script>
</head>
<body>
    <button id="upload-btn">上传文件</button>
    <input type="text" id="image-input">
    <img src="" alt="" id="img"/>
</body>
</html>
```




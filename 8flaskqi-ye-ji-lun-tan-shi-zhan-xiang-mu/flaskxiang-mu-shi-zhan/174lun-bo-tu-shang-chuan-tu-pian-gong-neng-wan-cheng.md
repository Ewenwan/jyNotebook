banner.js

```
$(function () {
   zlqiniu.setUp({
       'domain':'http://pdhjzz2pa.bkt.clouddn.com/',
       'browse_btn':'upload-btn',
       'uptoken_url':'/c/uptoken/',
       'success':function (up,file,info) {
           var imageInput = $("input[name='image_url']");
           imageInput.val(file.name)
       }
   });
});
```

banner.html

```
 <script src="https://cdn.staticfile.org/Plupload/2.1.1/moxie.js"></script>
    <script src="https://cdn.staticfile.org/Plupload/2.1.1/plupload.dev.js"></script>
    <script src="https://cdn.staticfile.org/qiniu-js-sdk/1.0.14-beta/qiniu.js"></script>
    <script src="{{ url_for('static',filename="cms/js/banners.js") }}"></script>
    <script src="{{ url_for('static',filename="common/zlqiniu.js") }}"></script>
```




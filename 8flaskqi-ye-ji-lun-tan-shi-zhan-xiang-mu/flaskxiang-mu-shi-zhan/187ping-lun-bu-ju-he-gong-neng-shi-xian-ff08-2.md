### 添加标签，判断是否登录

```
<span id="login-tag" data-is-login="1" style="display: none"></span>
```

### 通过ajax传递数据

```
$(function () {
    $('#comment-btn').click(function (event) {
        event.preventDefault();

        var loginTag = $('#login-tag').attr("data-is-login");
        // console.log(loginTag);
        if (!loginTag) {
            window.location = '/signin/';
        }else{
            var content = window.ue.getContent();
            var post_id = $("#post-content").attr('data-id');

            zlajax.post({
                'url':'/acomment/',
                'data':{
                  'content':content,
                  'post_id':post_id,
                },
                'success':function (data) {
                    if(data['code'] == 200) {
                        window.location.reload();
                    }
                    else{
                        zlalert.alertInfo(data["message"]);
                    }
                },
                'fail':function () {
                    zlalert.alertNetworkError();
                }
            });
        }
    });
});
```




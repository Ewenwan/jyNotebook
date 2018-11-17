### 定义钩子函数，定义全局用户

```
from .views import bp
import config
from flask import session,g
from .models import FrontUser

@bp.before_request
def before_request():
    if config.FRONT_USER_ID in session:
        user_id = session.get(config.FRONT_USER_ID)
        user = FrontUser.query.get(user_id)
        if user:
            g.front_user = user
```

### 判断用户是否登录

```
         {% if g.front_user %}
                    <li class="dropdown">
                        <a href="#" class="dropdown-toggle" type="button" id="dropdownMenu1"
                                data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
                            {{ g.front_user.username }}
                            <span class="caret"></span>
                        </a>
                        <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
                            <li><a href="#">个人中心</a></li>
                            <li><a href="#">设置</a></li>
                            <li><a href="#">注销</a></li>
                        </ul>
                    </li>
                {% else %}
                    <li><a href="{{ url_for("front.signin") }}">登陆</a></li>
                    <li><a href="{{ url_for("front.signup") }}">注册</a></li>
                {% endif %}
```

### ajax发送post请求传递数据

```
$(function () {
    var ue = UE.getEditor("editor",{
        'serverUrl':'/ueditor/upload/',
    });

    $("#submit-btn").click(function (event) {
        event.preventDefault();
        var titleInput = $('input[name="title"]');
        var boardSelect = $("select[name='board_id']");

        var title = titleInput.val();
        var board_id = boardSelect.val();
        console.log(board_id)
        var content = ue.getContent();

        if( !title || ! board_id || !content){
            zlalert.alertInfo("请输入相应内容！");
            return ;
        }

        zlajax.post({
            'url':'/apost/',
            'data':{
                'title':title,
                'content':content,
                'board_id':board_id,
            },
            'success':function (data) {
                if(data['code'] == 200){
                    zlalert.alertConfirm({
                        'msg':"帖子发表成功",
                        'cancelText':'回到首页',
                        'confirmText':'再发一篇帖子',
                        'cancelCallback':function () {
                            window.location = '/';
                        },
                        'confirmCallback':function () {
                            titleInput.val("");
                            ue.setContent("");
                        }
                    });
                }else{
                    zlalert.alertNetworkError();
                }
            }
        });
    });
});
```




利用jq获取数据，然后使用ajax以post请求方式传送数据

```
$(function () {
   $('#save-banner-btn').click(function (event) {
       event.preventDefault();

       var dialog = $('#banner-dialog');
       var nameInput = $("input[name='name']");
       var imageInput = $("input[name='image_url']");
       var linkInput = $("input[name='link_url']");
       var priorityInput = $("input[name='priority']");

       var name = nameInput.val();
       var image_url = imageInput.val();
       var link_url = linkInput.val();
       var priority = priorityInput.val();

       if(!name || !image_url || !link_url || !priority){
           zlalert.alertInfoToast("请输入完整的轮播图数据！");
           return ;
       }

       zlajax.post({
           'url':'/cms/abanner/',
           'data':{
               'name':name,
               'image_url':image_url,
               'link_url':link_url,
               'priority':priority,
           },
           'success':function (data) {
               dialog.modal("hide");
               if(data['code'] == 200){
                   //重新加载页面
                   window.location.reload();
               }else{
                   zlalert.alertInfo(data["message"]);
               }
           },
           'fail':function () {
             zlalert.alertNetworkError();
           },

       })
   });
});
```

轮播图数据显示

```
<tbody>
            {% for banner in banners %}
                <tr>
                    <td>{{ banner.name }}</td>
                    <td><a href="{{ banner.image_url }}" target="_blank">{{ banner.image_url }}</a></td>
                    <td><a href="{{ banner.link_url }}" target="_blank">{{ banner.link_url }}</a></td>
                    <td>{{ banner.priority }}</td>
                    <td>{{ banner.create_time }}</td>
                    <td>
                        <button class="btn btn-default btn-xs">编辑</button>
                        <button class="btn btn-danger btn-xs">删除</button>
                    </td>
                </tr>
            {% endfor %}
        </tbody>
```




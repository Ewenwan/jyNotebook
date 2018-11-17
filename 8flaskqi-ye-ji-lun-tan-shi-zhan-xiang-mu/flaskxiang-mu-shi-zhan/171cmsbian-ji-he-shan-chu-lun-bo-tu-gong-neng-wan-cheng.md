### 更新轮播图数据

将数据绑定到tr上，就能从button按钮获取父节点的父节点，然后得到绑定在tr上属性的数据

```
  {% for banner in banners %}
                <tr data-name="{{ banner.name }}" data-image="{{ banner.image_url }}" data-link="{{ banner.link_url }}" data-priority="{{ banner.priority }}" data-id="{{ banner.id }}">
                    <td>{{ banner.name }}</td>
                    <td><a href="{{ banner.image_url }}" target="_blank">{{ banner.image_url }}</a></td>
                    <td><a href="{{ banner.link_url }}" target="_blank">{{ banner.link_url }}</a></td>
                    <td>{{ banner.priority }}</td>
                    <td>{{ banner.create_time }}</td>
                    <td>
                        <button class="btn btn-default btn-xs edit-banner-btn">编辑</button>
                        <button class="btn btn-danger btn-xs">删除</button>
                    </td>
                </tr>
            {% endfor %}
```

编辑按钮

```
$(function () {
    $(".edit-banner-btn").click(function (event) {
        event.preventDefault();
        var self = $(this);
        var dialog = $('#banner-dialog');
        dialog.modal("show");

        /*获取数据*/
        var tr = self.parent().parent();
        var name = tr.attr("data-name");
        var image_url = tr.attr("data-image");
        var link_url = tr.attr("data-link");
        var priority = tr.attr("data-priority");

        /*填充数据*/
        var nameInput = dialog.find("input[name='name']");
        var imageInput = dialog.find("input[name='image_url']");
        var linkInput = dialog.find("input[name='link_url']");
        var priorityInput = dialog.find("input[name='priority']");
        var saveBtn = dialog.find('#save-banner-btn');

        nameInput.val(name);
        imageInput.val(image_url);
        linkInput.val(link_url);
        priorityInput.val(priority);
        saveBtn.attr("data-type",'update');
        saveBtn.attr("data-id",tr.attr('data-id'));
    });
});
```

表单数据更新/提交

```
$(function () {
   $('#save-banner-btn').click(function (event) {
       event.preventDefault();
        var self = $(this);
       var dialog = $('#banner-dialog');
       var nameInput = $("input[name='name']");
       var imageInput = $("input[name='image_url']");
       var linkInput = $("input[name='link_url']");
       var priorityInput = $("input[name='priority']");

       var name = nameInput.val();
       var image_url = imageInput.val();
       var link_url = linkInput.val();
       var priority = priorityInput.val();
       var submitType = self.attr("data-type");
       var banner_id = self.attr("data-id");
       console.log(banner_id);
       if(!name || !image_url || !link_url || !priority){
           zlalert.alertInfoToast("请输入完整的轮播图数据！");
           return ;
       }

       var url = ""
       if(submitType == "update"){
           url = "/cms/ubanner/";
       }else{
           url = "/cms/abanner/";
       }

       zlajax.post({
           'url':url,
           'data':{
               'name':name,
               'image_url':image_url,
               'link_url':link_url,
               'priority':priority,
               'banner_id':banner_id,
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

更新视图

```
@bp.route("/ubanner/",methods=["POST"])
@login_required
def ubanner():
    form = UpdateBannerForm(request.form)
    if form.validate():
        banner_id = form.banner_id.data
        name = form.name.data
        image_url = form.image_url.data
        link_url = form.link_url.data
        priority = form.priority.data
        banner = BannerModel.query.get(banner_id)
        if banner:
            banner.name = name
            banner.image_url = image_url
            banner.link_url = link_url
            banner.priority = priority
            db.session.commit()
            return restful.success()
        else:
            return restful.params_error(message="没有这个轮播图")
    else:
        return restful.params_error(message=form.get_error())
```

### 删除

删除按钮

```
 <button class="btn btn-danger btn-xs delete-banner-btn">删除</button>
```

删除js文件

```
$(function () {
   $(".delete-banner-btn").click(function (event) {
       event.preventDefault();
       var self = $(this);
       var tr = self.parent().parent();
       var banner_id = tr.attr("data-id");
       zlalert.alertConfirm({
           'msg':"请确定是否要删除当前的轮播图?",
           "confirmCallback":function () {
               zlajax.post({
                   'url':'/cms/dbanner/',
                   'data':{
                       'banner_id':banner_id,
                   },
                   'success':function (data) {
                       if(data['code'] == 200){
                           window.location.reload();
                       }else{
                           zlalert.alertInfo(data["message"]);
                       }
                   },
                   'fail':function () {
                       zlalert.alertNetworkError();
                   },
               })
           },
       });
   }) ;
});
```

删除视图

```
@bp.route('/dbanner/',methods=['POST'])
@login_required
def dbanner():
    banner_id = request.form.get("banner_id")
    if not banner_id:
        return restful.params_error(message="请传入轮播图id")
    banner = BannerModel.query.get(banner_id)
    if not banner:
        return restful.params_error(message="没有这个轮播图")
    db.session.delete(banner)
    db.session.commit()
    return restful.success()
```




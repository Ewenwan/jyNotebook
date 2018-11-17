### 1.相关链接

模态框:[https://v3.bootcss.com/javascript/\#modals](https://v3.bootcss.com/javascript/#modals)

栅格:[https://v3.bootcss.com/css/\#grid-options](https://v3.bootcss.com/css/#grid-options)

### 2.按钮

```
<button class="btn btn-warning" data-toggle="modal" data-target="#banner-dialog">
            添加轮播图
 </button>
```

通过data-target="\#banner-dialog"跳转到相应的id，并执行有相应id的部分

```
 <!-- Modal -->
    <div class="modal fade" id="banner-dialog" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span
                            aria-hidden="true">&times;</span></button>
                    <h4 class="modal-title" id="myModalLabel">轮播图</h4>
                </div>
                <div class="modal-body">
                    <form action="" class="form-horizontal">
                        <div class="form-group">
                            <label class="col-sm-2 control-label">名称:</label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" name="name" placeholder="轮播图名称">
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-sm-2 control-label">图片:</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="image_url" placeholder="轮播图图片">
                            </div>
                            <button class="btn btn-info col-sm-2">
                                    添加图片
                            </button>
                        </div>
                        <div class="form-group">
                            <label class="col-sm-2 control-label">跳转:</label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" name="link_url" placeholder="跳转链接">
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-sm-2 control-label">权重:</label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" name="priority" placeholder="优先级">
                            </div>
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">关闭</button>
                    <button type="button" class="btn btn-primary">保存</button>
                </div>
            </div>
        </div>
    </div>
```




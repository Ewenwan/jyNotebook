### 1.相关链接

定制工具栏图标:[http://fex.baidu.com/ueditor/\#start-toolbar](http://fex.baidu.com/ueditor/#start-toolbar)

### 2.完整的按钮列表

```
toolbars: [
    [
        'anchor', //锚点
        'undo', //撤销
        'redo', //重做
        'bold', //加粗
        'indent', //首行缩进
        'snapscreen', //截图
        'italic', //斜体
        'underline', //下划线
        'strikethrough', //删除线
        'subscript', //下标
        'fontborder', //字符边框
        'superscript', //上标
        'formatmatch', //格式刷
        'source', //源代码
        'blockquote', //引用
        'pasteplain', //纯文本粘贴模式
        'selectall', //全选
        'print', //打印
        'preview', //预览
        'horizontal', //分隔线
        'removeformat', //清除格式
        'time', //时间
        'date', //日期
        'unlink', //取消链接
        'insertrow', //前插入行
        'insertcol', //前插入列
        'mergeright', //右合并单元格
        'mergedown', //下合并单元格
        'deleterow', //删除行
        'deletecol', //删除列
        'splittorows', //拆分成行
        'splittocols', //拆分成列
        'splittocells', //完全拆分单元格
        'deletecaption', //删除表格标题
        'inserttitle', //插入标题
        'mergecells', //合并多个单元格
        'deletetable', //删除表格
        'cleardoc', //清空文档
        'insertparagraphbeforetable', //"表格前插入行"
        'insertcode', //代码语言
        'fontfamily', //字体
        'fontsize', //字号
        'paragraph', //段落格式
        'simpleupload', //单图上传
        'insertimage', //多图上传
        'edittable', //表格属性
        'edittd', //单元格属性
        'link', //超链接
        'emotion', //表情
        'spechars', //特殊字符
        'searchreplace', //查询替换
        'map', //Baidu地图
        'gmap', //Google地图
        'insertvideo', //视频
        'help', //帮助
        'justifyleft', //居左对齐
        'justifyright', //居右对齐
        'justifycenter', //居中对齐
        'justifyjustify', //两端对齐
        'forecolor', //字体颜色
        'backcolor', //背景色
        'insertorderedlist', //有序列表
        'insertunorderedlist', //无序列表
        'fullscreen', //全屏
        'directionalityltr', //从左向右输入
        'directionalityrtl', //从右向左输入
        'rowspacingtop', //段前距
        'rowspacingbottom', //段后距
        'pagebreak', //分页
        'insertframe', //插入Iframe
        'imagenone', //默认
        'imageleft', //左浮动
        'imageright', //右浮动
        'attachment', //附件
        'imagecenter', //居中
        'wordimage', //图片转存
        'lineheight', //行间距
        'edittip ', //编辑提示
        'customstyle', //自定义标题
        'autotypeset', //自动排版
        'webapp', //百度应用
        'touppercase', //字母大写
        'tolowercase', //字母小写
        'background', //背景
        'template', //模板
        'scrawl', //涂鸦
        'music', //音乐
        'inserttable', //插入表格
        'drafts', // 从草稿箱加载
        'charts', // 图表
    ]
]
```

### 3.实例

```
$(function () {
    var ue = UE.getEditor("editor",{
        'serverUrl':'/ueditor/upload/',
        toolbars: [[
        'undo', //撤销
        'redo', //重做
        'bold', //加粗
        'italic', //斜体
        'blockquote', //引用
        'selectall', //全选
        'insertcode', //代码语言
        'fontfamily', //字体
        'fontsize', //字号
        'paragraph', //段落格式
        'simpleupload', //单图上传
        'emotion', //表情
        'searchreplace', //查询替换
        'insertvideo', //视频
        'justifyleft', //居左对齐
        'justifyright', //居右对齐
        'justifycenter', //居中对齐
        'justifyjustify', //两端对齐
        'forecolor', //字体颜色
    ]]
    });
});
```

```
<script src="{{ static("front/js/pdetail.js") }}"></script>
<script id="editor" type="text/plain"></script>
```

### 4.定义评论模型

```
class CommentModel(db.Model):
    __tablename__ = "comment"
    id = db.Column(db.Integer,primary_key=True,autoincrement=True)
    content = db.Column(db.Text,nullable=False)
    create_time = db.Column(db.DateTime,default=datetime.now)

    post_id = db.Column(db.Integer,db.ForeignKey("post.id"))
    author_id = db.Column(db.String(100),db.ForeignKey("front_user.id"),nullable=False)

    post = db.relationship("PostModel",backref="comments")
    author = db.relationship("FrontUser",backref="comments")
```

### 5.定义添加评论视图

```
@bp.route('/acomment/')
@login_required
def add_comment():
    form = AddCommentForm(request.form)
    if form.validate():
        content = form.content.data
        # 通过帖子id，判断是否有当前帖子
        post_id = form.post_id.data
        post = PostModel.query.get(post_id)
        if post:
            comment = CommentModel(content=content)
            comment.post = post
            comment.author = g.front_user
            db.session.add(comment)
            db.session.commit()
            return restful.success()
        else:
            return  restful.params_error("没有这篇帖子！")
    else:
        return restful.params_error(form.get_error())
```

### 6.前端评论布局

```
        <div class="comment-group">
            <h3>评论列表</h3>
            <ul class="comment-list-group">
                {% for comment in post.comments %}
                    <li>{{ comment.content }}</li>
                {% endfor %}
            </ul>
        </div>
        <div class="add-comment-group">
            <h3>发表评论</h3>
            <script id="editor" type="text/plain" style="height:100px;"></script>
            <div class="comment-btn-group">
                <button class="btn btn-primary">发表评论</button>
            </div>
        </div>
    </div>
```

样式表

```
.comment-group{
    margin-top:20px;
    border:1px solid #e8e8e8;
    padding:10px;
}

.add-comment-group{
    margin-top: 20px;
    padding:10px;
    border:1px solid #e8e8e8;
}

.add-comment-group h3{
    margin-bottom: 10px;
}

.comment-btn-group{
    margin-top: 10px;
    text-align: right;
}

```




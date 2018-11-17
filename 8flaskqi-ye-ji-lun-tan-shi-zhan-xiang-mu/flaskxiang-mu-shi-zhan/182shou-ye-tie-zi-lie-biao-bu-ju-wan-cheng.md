帖子布局index.html

```
<div class="post-group">
                <ul class="post-group-head">
                    <li class="active"><a href="#">最新</a></li>
                    <li><a href="#">精华帖子</a></li>
                    <li><a href="#">点赞最多</a></li>
                    <li><a href="#">评论最多</a></li>
                </ul>

                <ul class="post-list-group">
                    {% for post in posts %}
                        <li>
                            <div class="author-avatar-group">
                                <img src="{{ post.author.avatar or url_for('static',filename="common/images/logo.png") }}"
                                     alt="">
                            </div>
                            <div class="post-info-group">
                                <p class="post-title">{{ post.title }}</p>
                                <p class="post-info">
                                    <span>作者:{{ post.author.username }}</span>
                                    <span>发表时间:{{ post.create_time }}</span>
                                    <span>评论:0</span>
                                    <span>阅读:0</span>
                                </p>
                            </div>
                        </li>
                    {% endfor %}
                </ul>
            </div>
```

帖子样式index.css

```
.index-banner{
    border-radius: 10px;
    overflow: hidden;
    height:200px;
}

.index-banner img{
    height: 200px;
}

.post-group{
    border: 1px solid #ddd;
    margin-top:20px;
    overflow: hidden;
    border-radius: 5px;
    padding:10px;
}

.post-group-head{
    overflow: hidden;
    list-style: none;
}

.post-group-head li{
    float: left;
    padding:5px 10px;
    /*background-color: red;*/
}

.post-group-head li a{
    color:#333;
}

.post-group-head > li.active{
    background:#ccc;
}

.post-list-group{
    margin-top:20px;
}

.author-avatar-group{
    float:left;
}

.author-avatar-group img{
    width:50px;
    height: 50px;
    border-radius: 50%;
}

.post-info-group{
    float:left;
    margin-left:10px;
}

.post-info-group .post-info{
    margin-top:10px;
    color: #8c8c8c;
    font-size:12px;
}

.post-info span{
    margin-right:10px;
}
```

需要去除浏览器自带样式

```
a, abbr, acronym, address, applet, article, aside, audio, b, big, blockquote, body, canvas, caption, center, cite, code, dd, del, details, dfn, div, dl, dt, em, embed, fieldset, figcaption, figure, footer, form, h1, h2, h3, h4, h5, h6, header, hgroup, html, i, iframe, img, ins, kbd, label, legend, li, mark, menu, nav, object, ol, output, p, pre, q, ruby, s, samp, section, small, span, strike, strong, sub, summary, sup, table, tbody, td, tfoot, th, thead, time, tr, tt, u, ul, var, video {
    margin: 0;
    padding: 0;
    border: 0;
    vertical-align: baseline;
    list-style: none;
}
```

修改posts模型，增加外键author\_id

```
class PostModel(db.Model):
    __tablename__ = "post"
    id = db.Column(db.Integer,primary_key=True,autoincrement=True)
    title = db.Column(db.String(200),nullable=False)
    content = db.Column(db.Text,nullable=False)
    create_time = db.Column(db.DateTime,default=datetime.now)
    board_id = db.Column(db.Integer,db.ForeignKey("board.id"))
    author_id = db.Column(db.String(100),db.ForeignKey("front_user.id"),nullable=False)
    # 一对多
    board = db.relationship("BoardModel",backref="posts")
    author = db.relationship("FrontUser",backref="posts")
```




显示各个用户所能显示的版块

```
                  {% set cms_user = g.cms_user %}

                  {% if cms_user.has_permission(CMSPersmission.POSTER) %}
                    <li class="nav-group post-manage"><a href="#">帖子管理</a></li>
                  {% endif %}

                  {% if cms_user.has_permission(CMSPersmission.COMMENTER) %}
                    <li class="comments-manage"><a href="#">评论管理</a></li>
                  {% endif %}

                  {% if cms_user.has_permission(CMSPersmission.BOARDER) %}
                      <li class="board-manage"><a href="#">板块管理</a></li>
                  {% endif %}

                  {% if cms_user.has_permission(CMSPersmission.FRONTUSER) %}
                      <li class="nav-group user-manage"><a href="#">前台用户管理</a></li>
                  {% endif %}

                  {% if cms_user.has_permission(CMSPersmission.CMSUSER) %}
                     <li class="nav-group cmsuser-manage"><a href="#">CMS用户管理</a></li>
                  {% endif %}

                  {% if cms_user.is_developer %}
                    <li class="cmsrole-manage"><a href="#">CMS组管理</a></li>
                  {% endif %}
```

注意需要使用类或者其他的数据，可以使用上下文

```
# 上下文，这样在bp蓝图下的模板都能够使用
@bp.context_processor
def cms_context_peocessor():
    return {"CMSPersmission":CMSPersmission}
```

```
# 添加测试数据
# 访问者
# python manage.py create_cms_user -u 我是访问者 -p 123456 -e visitor@qq.com
# python manage.py add_user_to_role -e visitor@qq.com -n 访问者
# 运营
# python manage.py create_cms_user -u 我是运营者 -p 123456 -e operator@qq.com
# python manage.py add_user_to_role -e operator@qq.com -n 运营
# 管理员
# python manage.py create_cms_user -u 我是管理员 -p 123456 -e admin@qq.com
# python manage.py add_user_to_role -e admin@qq.com -n 管理员
# 开发者
# python manage.py create_cms_user -u 我是开发者 -p 123456 -e developer@qq.com
# python manage.py add_user_to_role -e developer@qq.com -n 开发者
```




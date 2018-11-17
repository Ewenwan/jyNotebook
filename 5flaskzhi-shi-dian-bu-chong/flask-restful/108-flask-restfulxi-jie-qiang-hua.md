# 108 Flask-Restful细节强化

1. 在蓝图中，如果使用'flask-restful'，那么创建'Api'对象的时候，就不要再使用'app'了，而是使用蓝图

   ```text
   article_bp = Blueprint('article',__name__,url_prefix='/article')
   api = Api(article_bp)
   ```

2. 如果在'flask-restful'的视图中想要返回'html'代码或者是模板，那么就应该使用'api.representation'这个装饰器来定义一个函数，在这个函数中，应该对'html'代码进行一个封装，再返回

   ```text
   @api.representation('text/html')
   def output_html(data,code,headers):
       print(data)
       # 在representation装饰的函数中，必须返回一个Response对象
       resp = make_response(data)
       return resp

   class ListView(Resource):
       def get(self):
           return render_template('index.html')
   api.add_resource(ListView,'/list/',endpoint='list')
   ```


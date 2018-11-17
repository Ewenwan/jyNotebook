Vue.js路由允许通过不同的url访问不同的内容

通过vue.js可以实现多视图的单页web应用

Vue.js 路由需要载入[vue-router 库](https://github.com/vuejs/vue-router)

中文文档地址：[vue-router文档](http://router.vuejs.org/zh-cn/)

### 安装

#### 1、直接下载 / CDN

```
https://unpkg.com/vue-router/dist/vue-router.js
```

#### NPM

推荐使用淘宝镜像：

```
cnpm install vue-router
```

### 简单实例

Vue.js+vue-router可以很简单的实现单页应用

&lt;router-link&gt;是一个组件，该组件用于设置一个导航链接，切换不用HTML内容。to属性为目标地址，即显示的内容。

实例:将vue-router加进来，然后配置组件和路由映射，再告诉vue-router在哪里渲染

```
<!DOCTYPE html>
<html>

    <head>
        <meta charset="UTF-8">
        <title>test55</title>
        <script src="https://cdn.staticfile.org/vue/2.4.2/vue.js"></script>
        <script src="https://cdn.staticfile.org/vue-router/2.7.0/vue-router.js"></script>
    </head>

    <body>
        <div id="test55">
            <h1>Angle</h1>
            <p>
                <!-- 使用router-link 组件来导航 -->
                <!--通过传入to属性指定链接 -->
                <!-- <router-link默认会被渲染成一个<a>标签 -->
                <router-link to="/angle">go to Angle</router-link>
                <router-link to="/miku">go to Miku</router-link>
            </p>

            <!-- 路由出口 -->
            <!-- 路由匹配到的组件将渲染在这里 -->
            <router-view></router-view>
        </div>

        <script type="text/javascript">
            //0.如果使用模块化机制编程，导入vue和vuerouter，要调用vue.use(VueRouter)
            //1.定义(路由)组件
            // 可以从其他文件import进来
            const angle = {
                template: '<div>angle</div>'
            }
            const miku = {
                template: '<div>miku</div>'
            }

            //2.定义路由
            //每个路由应该映射一个组件，其中"component"可以是通过Vue.extend()创建的组件构造器
            //或者，只是一个组件配置对象
            const routes = [{
                    path: "/angle",
                    component: angle,
                },
                {
                    path: "/miku",
                    component: miku,
                }
            ]

            //3.创建router实例，然后传"routes"配置，可以传别的配置参数
            const router = new VueRouter({
                routes: routes
            })

            //4.创建和挂载根实例
            // 要通过'router'配置参数注入路由，从而让整个应用都有路由功能
            const app = new Vue({
                router: router
            }).$mount("#test55")
        </script>
    </body>

</html>
```

![](/assets/1.13.4.14-1.png)

### &lt;router-link&gt;相关属性

#### to

表示目标路由的链接。当被点击后，内部会立刻把to的值传到router.push\(\)，所以这个值可以使一个字符串或者是描述目标位置的对象

```
<!-- 字符串 -->
<router-link to="home">Home</router-link>
<!-- 渲染结果 -->
<a href="home">Home</a>

<!-- 使用 v-bind 的 JS 表达式 -->
<router-link v-bind:to="'home'">Home</router-link>

<!-- 不写 v-bind 也可以，就像绑定别的属性一样 -->
<router-link :to="'home'">Home</router-link>

<!-- 同上 -->
<router-link :to="{ path: 'home' }">Home</router-link>

<!-- 命名的路由 -->
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>
```

#### replace

设置replace属性的话，当点击时，会调用router.replace\(\)而不是router.push\(\)，导航后不会留下history记录

```
<router-link :to="{path:'/abc'}" replace></router-link>
```

#### append

设置append属性后，则在当前\(相对\)路径前添加基路径

例如，从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

```
<router-link :to="{ path: 'relative/path'}" append></router-link>
```

#### tag

有时候想要&lt;router-link&gt;渲染成某种标签，使用tag prop类指定何种标签，同样它还是会监听点击，触发导航

```
<router-link to="/angle" tag="li">foo</router-link>
<!-- 渲染结果 -->
<li>foo</li>
```

#### active-class

设置 链接激活时使用的css类名。可以通过以下代码代替

```
        <style>
            ._active{
                background: red;
            }
        </style>

<router-link to="/angle" active-class="_active">go to Angle</router-link>
```

注意这里 class 使用 active\_class="\_active"

#### exact-active-class

配置当链接被精确的时候应该激活的class

```
<router-link to="/angle" exact-active-class="_active">go to Angle</router-link>
```

### event

声明可以用来触发导航的事件，可以是一个字符串或是一个包含字符串的数组

```
<router-link v-bind:to = "{ path: '/route1'}" event = "mouseover">Router Link 1</router-link>
```

以上代码设置了 event 为 mouseover ，及在鼠标移动到 Router Link 1 上时导航的 HTML 内容会发生改变

### NPM路由实例

接下来我们演示了一个使用 npm 简单的路由实例，开始前，请先下载该实例源代码：

[路由实例](http://static.runoob.com/download/vue-2.0-simple-routing-example-master.zip)

你也可以在 Github 上下载：[https://github.com/chrisvfritz/vue-2.0-simple-routing-example](https://github.com/chrisvfritz/vue-2.0-simple-routing-example)

下载完后，解压该目录，重命名目录为 vue-demo，vu 并进入该目录，执行以下命令：

```
# 安装依赖，使用淘宝资源命令 cnpm

cnpm install


# 启动应用，地址为 localhost:8080

cnpm run dev
```

如果你需要发布到正式环境可以执行以下命令：

```
cnpm run build
```

执行成功后，访问 http://localhost:8080 即可看到如下界面：

![](http://www.runoob.com/wp-content/uploads/2017/01/30646E50-8956-47F0-9DBE-4A2023B873E7.jpg)




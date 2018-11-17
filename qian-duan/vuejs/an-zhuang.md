### Vue.js 安装

#### 1、独立版本

我们可以在 Vue.js 的官网上直接下载 vue.min.js 并用**&lt;script&gt;**标签引入。

[下载 Vue.js](http://vuejs.org/js/vue.min.js)

---

#### 2、使用 CDN 方法

以下推荐国外比较稳定的两个 CDN，国内还没发现哪一家比较好，目前还是建议下载到本地。

* **Staticfile CDN（国内）**:[https://cdn.staticfile.org/vue/2.2.2/vue.min.js](https://cdn.staticfile.org/vue/2.2.2/vue.min.js)

* **unpkg**：[https://unpkg.com/vue/dist/vue.js](https://unpkg.com/vue/dist/vue.js), 会保持和 npm 发布的最新的版本一致。

* **cdnjs**:[https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js](https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js)

---

#### 3、NPM 方法

由于 npm 安装速度慢，本教程使用了淘宝的镜像及其命令 cnpm，安装使用介绍参照：[使用淘宝 NPM 镜像](http://www.runoob.com/nodejs/nodejs-npm.html#taobaonpm)。

npm 版本需要大于 3.0，如果低于此版本需要升级它：

```
# 查看版本
$ npm -v
2.3.0

#升级 npm
cnpm install npm -g


# 升级或安装 cnpm
npm install cnpm -g
```

在用 Vue.js 构建大型应用时推荐使用 NPM 安装：

```
# 最新稳定版

$ cnpm install vue
```

---

#### 命令行工具

Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。

```
# 全局安装 vue-cli
$ cnpm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
$ vue init webpack my-project
# 这里需要进行一些配置，默认回车即可
This will install Vue 2.x version of the template.

For Vue 1.x use: vue init webpack#1.0 my-project

? Project name my-project
? Project description A Vue.js project
? Author runoob <test@runoob.com>
? Vue build standalone
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Setup unit tests with Karma + Mocha? Yes
? Setup e2e tests with Nightwatch? Yes

   vue-cli · Generated "my-project".

   To get started:

     cd my-project
     npm install
     npm run dev

   Documentation can be found at https://vuejs-templates.github.io/webpack
```

进入项目，安装并运行：

```
$ cd my-project
$ cnpm install
$ cnpm run dev
 DONE  Compiled successfully in 4388ms

> Listening at http://localhost:8080
```

成功执行以上命令后访问 [http://localhost:8080/，输出结果如下所示：](http://localhost:8080/，输出结果如下所示：)

![](http://www.runoob.com/wp-content/uploads/2017/01/56219E04-D156-43EC-AC59-BFE7E38A62C3.jpg)

> **注意：**Vue.js 不支持 IE8 及其以下 IE 版本。

---

#### 在 Cloud Studio 中运行 Vue.js

下面我们介绍如何在 Cloud Studio 中安装、使用 Vue.js：

* step1：访问[Cloud Studio](https://studio.coding.net/)，注册/登录账户。

* step2：在右侧的运行环境菜单选择：`"Node.js"`

* step3：在左侧代码目录中新建 html 目录，编写你的HTML代码，例如 index.html

  ![](https://dn-coding-net-production-pp.qbox.me/212a55fb-94b6-4e66-b410-35863605d7a4.jpg)

* step4: 我们推荐链接到一个你可以手动更新的指定版本号：

  ```
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
  ```

  你可以在[cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue/)浏览 NPM 包的源代码。 Vue 也可以在[cdnjs](https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js)上获取 \(cdnjs 的版本更新可能略滞后\)。

* step5：在用 Vue 构建大型应用时推荐使用 NPM 安装:

  ```
  # 最新稳定版

  $ npm install vue
  ```

* step6：Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。

  ```
  # 全局安装 vue-cli
  $ cnpm install --global vue-cli
  # 创建一个基于 webpack 模板的新项目
  $ vue init webpack my-project
  # 这里需要进行一些配置，默认回车即可
  ```

  进入项目，安装并运行：

  ```
  $ cd my-project
  $ cnpm install
  $ cnpm run dev
   DONE  Compiled successfully in 4388ms

  > Listening at http://localhost:8080
  ```

* step6：点击最右侧的【访问链接】选项卡，在访问链接面板中填写端口号为：8080（和刚才配置文件中的端口号一致），点击创建链接，即可点击生成的链接访问我们刚刚编写的代码，查看 Vue.js 效果。

  ![](http://www.runoob.com/wp-content/uploads/2017/01/56219E04-D156-43EC-AC59-BFE7E38A62C3.jpg)




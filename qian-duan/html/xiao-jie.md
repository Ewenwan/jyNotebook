## html

全称“hyperTextmarkuplanguage”

### 基础标签

* 标签由一对`<>和</>`包括
  * 例如:
    * `<html>和</html>`
* 中文乱码问题
  * 在head标签中添加`<meta charset="utf-8"/>`
  * 在html中添加属性值,例如:`<html lang="en">`
    * lang告诉搜索引擎爬虫，网站是关于什么内容的
      * en:英文
      * zh:中文
      * ...
  * 编码集:
    * gb2312
    * gbk
    * Unicode
    * utf-8
    * ...
* title标签:标题
* meta标签
  * content:内容，name:关键字
* p标签:段落标签
* h标签
  * h1
  * h2
  * h3
  * h4
  * h5
  * h6
  * strong标签:加粗
* em标签:斜体
* del标签:删除线，例如:`<del>12元</del>`显示为~~12元~~
* address标签:一般用于地址
* div标签:差不多效果与p标签差不多，用于布局
* span标签
* div和span:充当容器，便于分块，结构化，便于维护

### 高级标签

* html编码:以&开头";"结尾
  * 空格:`&nbsp;`
  * 小于:`&lt;`
  * 大于:`&gt;`
  * 水平线:`<hr/>`
* 有序列表ol

  * 默认排序

    ```
            <ol>
                <li>喜羊羊</li>
                <li>Fate</li>
                <li>绝对双刃</li>
            </ol>
    ```

    ![](/assets/14.1.8-01.png)

  * 类型:type

    * A

      ```
      <ol type="A">
          <li>喜羊羊</li>
          <li>Fate</li>
          <li>绝对双刃</li>
      </ol>
      ```

      ![](/assets/14.1.8-02.png)

    * a

    * i:罗马数字

    * ..

  * 倒序:reversed

    ```
    <ol type="A" reversed="reversed">
        <li>喜羊羊</li>
        <li>Fate</li>
        <li>绝对双刃</li>
    </ol>
    ```

    ![](/assets/14.1.8-03.png)

  * 定义从第几开始计数

    ```
    <ol type="1" start=2>
        <li>喜羊羊</li>
        <li>Fate</li>
        <li>绝对双刃</li>
    </ol>
    ```

    ![](/assets/14.1.8-04.png)

* 无序列表ul（可以用于导航栏）

  * 类型::type
    * square:方块
    * circle:空心圆

```
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <title></title>

        <style>

            *{
                margin: 0;
                padding: 0;
            }

            ul{
                list-style: none;
            }

            li{
                margin: 0 10px;
                float: left;
                color: #f40;
                font-weight: bold;
                font-size: 14px;
                height: 25px;
                line-height: 25px;
                padding: 0 5px;
            }

            li:hover{
                background-color: #f40;
                color:#fff;
                border-radius: 15px;
            }

        </style>

    </head>
    <body>
        <ul type="circle">
            <li>天猫</li>
            <li>聚划算</li>
            <li>天猫超市</li>
        </ul>
    </body>
</html>
```

![](/assets/14.1.8-05.png)

* img标签:引用图片
  * src:图片的资源地址
    * 网络上的url
    * 本地的绝对路径
    * 本地的相对路径
  * alt:图片占位符，在url不存在时，或者显示不出图片时进行提示
  * title:图片提示符，鼠标移到图片位置进行提示

```
<img src="xx.png" alt="占位" title="提示"/>
```

* a标签\(anchor -- 锚\):超链接

  * href
  * target
    * \_blank:在新页面打开超链接
  * 功能:

    * 超链接

    ```
    <a href="https://www.baidu.com"></a>
    ```

    * 锚点:调到指定id的位置

    ```
    <div id="id"></div>

    <a href="#id"></a>
    ```

    * 打电话

    ```
    <a href="tel:1555xxxxx"></a>
    ```

    * 发邮件

    ```
    <a href="mailto:xxx@qq.com"></a>
    ```

    * 协议限定符
      * 执行JavaScript代码

    ```
    <a href="javascript:alert(1)">click</a>
    ```

* form表单:发送数据

  * method:发送方式

    * get

    * post

  * action:发送数据的位置

  * 组件

    * input标签

      * type

        * text:文本

        * password:密码

        * button:普通按钮

        * submit:提交按钮

        * radio:单选框

          * name属性值一样

        * checkbox:复选框

          * name属性值一样

          * checkd属性值

            * `<input type="checkbox" checkd="checkd">`

      * onblur:失去焦点

      * onfocus:鼠标聚焦

    * select标签:选择

    ```
    <select name="province">
     <option>a</option>
     <option>b</option>
     <option>c</option>
     <option>d</option>
    </select>
    ```

    * 




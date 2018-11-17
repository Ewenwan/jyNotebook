# 2.3.3 javascript渲染的页面

有时候我们在用 Urllib 或 Requests 抓取网页时，得到的源代码实际和浏览器中看到的是不一样的。

这个问题是一个非常常见的问题，现在网页越来越多地采用 Ajax、前端模块化工具来构建网页，整个网页可能都是由 JavaScript 渲染出来的，意思就是说原始的 HTML 代码就是一个空壳，例如：

```text
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>This is a Demo</title>
    </head>
    <body>
        <div id="container">
        </div>
    </body>
    <script src="app.js"></script>
</html>
```

body 节点里面只有一个 id 为 container 的节点，但是注意到在 body 节点后引入了一个 app.js，这个便负责了整个网站的渲染。

在浏览器打开这个页面时，首先会加载这个 HTML 内容，接着浏览器会发现其中里面引入了一个 app.js 文件，然后浏览器便会接着去请求这个文件，获取到该文件之后便会执行其中的 JavaScript 代码，而 JavaScript 则会改变 HTML 中的节点，向内添加内容，最后得到完整的页面。

但是在用 Urllib 或 Requests 等库来请求当前页面时，我们得到的只是这个 HTML 代码，它不会帮助我们去继续加载这个 JavaScript 文件，这样也就看不到浏览器中看到的内容了。

这也解释了为什么有时我们得到的源代码和浏览器中看到的是不一样的。

所以使用基本 HTTP 请求库得到的结果源代码可能跟浏览器中的页面源代码不太一样。对于这样的情况，我们可以分析其后台 Ajax 接口，也可使用 Selenium、Splash 这样的库来实现模拟 JavaScript 渲染，这样我们便可以爬取 JavaScript 渲染的网页的内容了


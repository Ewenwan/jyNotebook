## CSS3 动画

通过 CSS3，我们能够创建动画，这可以在许多网页中取代动画图片、Flash 动画以及 JavaScript。

## @ketframes规则

@keyframes 规则用于创建动画。在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。

```
@keyframes myfirst
{
    from(background:red;)
    to{background:blue;}
}

@-moz-keyframes myfirst/*firefox*/
{
    from(background:red;)
    to{background:blue;}
}

@-webkit-keyframes myfirst/*safari和chrome*/
{
    from(background:red;)
    to{background:blue;}
}

@-o-keyframes myfirst/*opera*/
{
    from(background:red;)
    to{background:blue;}
}
```

---

## CSS3 动画

当您在 @keyframes 中创建动画时，请把它捆绑到某个选择器，否则不会产生动画效果。

通过规定至少以下两项 CSS3 动画属性，即可将动画绑定到选择器：

* 规定动画的名称
* 规定动画的时长

实例:

把"myfirst"动画捆绑到div元素，时长5秒

```
div{
    animation（动画）:myfirst 5s;
    -moz-animation:myfirst 5s;/*firefox*/
    -webkit-animation:myfirst 5s;/*safari和chrome*/
    -o-animation:myfirst 5s;/*opera*/
}
```

---

## 什么是 CSS3 中的动画？

动画是使元素从一种样式逐渐变化为另一种样式的效果。

您可以改变任意多的样式任意多的次数。

请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%。

0% 是动画的开始，100% 是动画的完成。

实例:

根据百分比完成度，来改变背景色

```
@keyframes myfirst
{
    0% (background:red;)
    %25 {background:blue;}
    %50 {backgrouond:pink;}
    %100 {background:black;}
}

@-moz-keyframes myfirst/*firefox*/
{
    0% (background:red;)
    %25 {background:blue;}
    %50 {backgrouond:pink;}
    %100 {background:black;}
}

@-webkit-keyframes myfirst/*safari和chrome*/
{
    0% (background:red;)
    %25 {background:blue;}
    %50 {backgrouond:pink;}
    %100 {background:black;}
}

@-o-keyframes myfirst/*opera*/
{
    0% (background:red;)
    %25 {background:blue;}
    %50 {backgrouond:pink;}
    %100 {background:black;}
}
```

## CSS3 动画属性

下面的表格列出了 @keyframes 规则和所有动画属性：

| 属性 | 描述 |
| :--- | :--- |
| [@keyframes](http://www.w3school.com.cn/cssref/pr_keyframes.asp) | 规定动画。 |
| [animation](http://www.w3school.com.cn/cssref/pr_animation.asp) | 所有动画属性的简写属性，除了 animation-play-state 属性。 |
| [animation-name](http://www.w3school.com.cn/cssref/pr_animation-name.asp) | 规定 @keyframes 动画的名称。 |
| [animation-duration](http://www.w3school.com.cn/cssref/pr_animation-duration.asp) | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。 |
| [animation-timing-function](http://www.w3school.com.cn/cssref/pr_animation-timing-function.asp) | 规定动画的速度曲线。默认是 "ease"。 |
| [animation-delay](http://www.w3school.com.cn/cssref/pr_animation-delay.asp) | 规定动画何时开始。默认是 0。 |
| [animation-iteration-count](http://www.w3school.com.cn/cssref/pr_animation-iteration-count.asp) | 规定动画被播放的次数。默认是 1。 |
| [animation-direction](http://www.w3school.com.cn/cssref/pr_animation-direction.asp) | 规定动画是否在下一周期逆向地播放。默认是 "normal"。 |
| [animation-play-state](http://www.w3school.com.cn/cssref/pr_animation-play-state.asp) | 规定动画是否正在运行或暂停。默认是 "running"。 |
| [animation-fill-mode](http://www.w3school.com.cn/cssref/pr_animation-fill-mode.asp) | 规定对象动画时间之外的状态。 |

```
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:100px;
background:red;
position:relative;
animation-name:myfirst;
animation-duration:5s;
animation-timing-function:linear;
animation-delay:2s;
animation-iteration-count:infinite;
animation-direction:alternate;
animation-play-state:running;
/* Firefox: */
-moz-animation-name:myfirst;
-moz-animation-duration:5s;
-moz-animation-timing-function:linear;
-moz-animation-delay:2s;
-moz-animation-iteration-count:infinite;
-moz-animation-direction:alternate;
-moz-animation-play-state:running;
/* Safari and Chrome: */
-webkit-animation-name:myfirst;
-webkit-animation-duration:5s;
-webkit-animation-timing-function:linear;
-webkit-animation-delay:2s;
-webkit-animation-iteration-count:infinite;
-webkit-animation-direction:alternate;
-webkit-animation-play-state:running;
/* Opera: */
-o-animation-name:myfirst;
-o-animation-duration:5s;
-o-animation-timing-function:linear;
-o-animation-delay:2s;
-o-animation-iteration-count:infinite;
-o-animation-direction:alternate;
-o-animation-play-state:running;
}

@keyframes myfirst
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

@-moz-keyframes myfirst /* Firefox */
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

@-webkit-keyframes myfirst /* Safari and Chrome */
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

@-o-keyframes myfirst /* Opera */
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}
</style>
</head>
<body>


<div></div>

</body>
</html>
```




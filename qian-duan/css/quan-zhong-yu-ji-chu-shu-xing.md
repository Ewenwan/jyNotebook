### 权重\(256进制\)

* !important:Infinity
* 行间样式:1000
* id:100
* class\|属性\|伪类:10
* 标签\|伪元素:1
* 通配符:0

### 选择器

* 父子选择器/派生选择器

```
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="utf-8" />
        <title></title>
        <style type="text/css">
            div strong em{
                background: red;
            }
        </style>
    </head>

    <body>
        <div><strong><em>angle</em></strong></div>
    </body>

</html>
```

![](/assets/14.2.10.2-01.png)

* 直接子元素选择器

```
section>(div>(p>a>span)+ul>(li>(a>span>em)+p)+li)+a>(p>em)+div
```

```
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="utf-8" />
        <title></title>
        <style type="text/css">
            section div ul li a em{
                background-color: red;
            }
        </style>
    </head>

    <body>
        <section>
            <div>
                <p><a href=""><span></span></a></p>
                <ul>
                    <li>
                        <a href=""><span><em>1</em></span></a>
                        <p></p>
                    </li>
                    <li></li>
                </ul>
            </div>
            <a href="">
                <p><em>2</em></p>
                <div></div></a>
        </section>
    </body>

</html>
```

* 并列选择器：相同的计算机权重

```
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="utf-8" />
        <title></title>
        <style type="text/css">
            #only{
                background: red;
            }

            div{
                background: green;
            }
        </style>
    </head>

    <body>
        <div id="only">1</div>
        <div class="oo">2</div>
    </body>

</html>
```

* 分组选择器:通过使用逗号，可以减少代码耦合度

```
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="utf-8" />
        <title></title>
        <style type="text/css">
            #only,a{
                background: red;
            }

            div{
                background: green;
            }
        </style>
    </head>

    <body>
        <div id="only">1</div>
        <a class="oo">2</a>
    </body>

</html>
```

### 属性

* font-weight：字体粗细

  * lighter
  * normal
  * bold,相当于700
  * bolder
  * 100-900

* font-style:字体样式

  * italic:斜体

* font-size:字体大小

  * px

* font-famity:字体
* color
  * rgb
    * 00-ff：\#00ff00
    * 每两位相同可以简写:
      * \#ff4400
      * \#f40
    * rgb\(0,0,0\)
* width:宽度
* height:高度
* border:边框

  * border-left-color:左边颜色
  * border-top-color:顶部颜色border:100px solid black;

    * transparent:透明度

```
# 利用border画出三角形

<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="utf-8" />
<title></title>
<style type="text/css">
div{
    width:0px;
    height: 0px;
    border: 100px solid black;
    border-left-color: transparent;
    border-top-color: transparent;
    border-right-color:transparent;
}

</style>
</head>

<body>
<div id="only"></div>
</body>

</html>
```

![](/assets/14.2.10.2-03.png)


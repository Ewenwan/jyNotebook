## transform\(转型\)属性

学习地址:[http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/](http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)

## 2D转换方法

* translate\(\)
* rotate\(\)
* scale\(\)
* skew\(\)
* matrix\(\)

---

## translate\(\)方法

通过translate\(\)方法，元素从其当前位置移动，根据给定的left\(x坐标\)和top\(y坐标\)位置参数:

```
div{
    transform:translate(50px,100px);
    -ms-transform:translate(50px,100px);/*IE9*/
    -webkit-transform:translate(50px,100px);/*Safari and Chrome*/
    -o-transform:translate(50px,100px);/*Opera*/
    -moz-transform:translate(50px,100px);/*Firefox*/
}
```

值translate\(50px,100px\)把元素从左侧移动50像素，从顶端移动100像素

---

## rotate\(\)方法

通过rotate\(\)方法，元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转

```
div{

    transform:rotate(30deg);
    -ms-transform:rotate(30deg);/*IE9*/
    -webkit-transform:rotate(30deg);/*Safari and Chrome*/
    -o-transform:rotate(30deg);/*Opera*/
    -moz-transform:rotate(30deg);/*Firefox*/
}
```

值rotate\(30deg\)把元素顺时针旋转30度

---

## scale\(\)方法

通过scale\(\)方法，元素的尺寸会增加或减少，根据给定的宽度\(X轴\)和高度\(Y轴\)参数

```
div{
    transform:scale(2,4);
    -ms-transform:scale(2,4);/*IE9*/
    -webkit-transform:scale(2,4);/*Safari和Chrome*/
    -moz-transform:scale(2,4);/*Firefox*/
    -o-transform:scale(2,4);/*opera*/
}
```

值scale\(2,4\)把宽度转换为原始尺寸的2倍，把高度转换为原始高度的4倍

---

## skew\(\)方法

通过skew\(\)方法，元素翻转给定的角度，根据给定的水平线\(X轴\)和垂直线\(Y轴\)参数

```
div{
    transform:skew(30deg,20deg);
    -ms-transform:skew(30deg,20deg);
    -webkit-transform:skew(30deg,20deg);
    -o-transform:skew(30deg,20deg);
    -moz-transform:skew(30deg,20deg);
}
```

值skew\(30deg,20deg\)围绕x轴把元素翻转30度，围绕y轴翻转20度

---

## matrix\(\)方法

matrix\(\)方法把所有2D转换方法组合在一起

matrix\(\)方法需要6个参数，包含数学函数，允许：旋转、缩放、移动、倾斜元素

实例:如何使用matrix方法将div元素旋转30度

```
div
{
transform:matrix(0.866,0.5,-0.5,0.866,0,0);
-ms-transform:matrix(0.866,0.5,-0.5,0.866,0,0);        /* IE 9 */
-moz-transform:matrix(0.866,0.5,-0.5,0.866,0,0);    /* Firefox */
-webkit-transform:matrix(0.866,0.5,-0.5,0.866,0,0);    /* Safari and Chrome */
-o-transform:matrix(0.866,0.5,-0.5,0.866,0,0);        /* Opera */
}
```

matrix\(a,b,c,d,e,f\)

![](/assets/matrix.png)

ax+cy+e为变换后的水平坐标，bx+dy+f表示变换后的垂直位置

例如

## 平移

matrix\(1,0,0,1,30,30\)

中心为\(0,0\)，x=0，y=0

变换后的x坐标为:ax+cy+e=1\*0+0\*0+30=30

变换后的y坐标为:bx+dy+f=0\*0+1\*0+30=30

tips：matrix\(a,b,c,e,水平偏移距离,垂直偏移距离\)

## 缩放

matrix\(s,0,0,s,0,0\);

x1 = ax+cy+e = s\*x+\*y+0=s\*x;

y1 = bx+dy+f = 0\*x+s\*y+0=s\*y;

matrix\(sx,0,0,sy,0,0\)等价于scale\(sx,sy\);

## 旋转\(rotate\)

方法以及参数使用\(假设角度为α\)

matrix\(cosα,sinα,-sinα,cosα,0,0\)

结合矩阵公式有:

x1 = x\*cosα-y\*sinα+0=x\*cosα-y\*sinα;

y1 = x\*sinα+y\*cosα+0=x\*sinα+y\*cosα;

学习地址:[http://www.zhangxinxu.com/study/201206/css3-transform-matrix-rotate.html](http://www.zhangxinxu.com/study/201206/css3-transform-matrix-rotate.html)

```
CSS代码：
.matrix_box {
    width: 150px;
    height: 150px;
    line-height: 130px;
    background-color: #a0b3d6;
    font-size: 60px;
    text-align:center;
    text-shadow:1px 1px #fff;
}
HTML代码：
<p id="matrixDetail">目前属性值为：matrix(1,0,0,1,0,0)</p>
<p>请输入角度(0~360)：<input type="text" id="matrixRotate" value="0" min="0" max="360" autocomplete="off" /></p>
<div id="matrixBox" class="matrix_box">↑</div>
JS代码：
(function() {
   var $ = function(selector) {
      return document.querySelector(selector);
   };
   var $css3Transform = function(element, value) {
      // 应用transform属性值，与之前demo雷同，略……
   };
   var eleDetail = $("#matrixDetail"),
      eleRotate = $("#matrixRotate"),
      eleBox = $("#matrixBox");

   if (eleDetail && eleRotate && eleBox) {
      eleRotate.addEventListener("change", function() {
         var maxVal = this.getAttribute("max"), minVal = this.getAttribute("min"), value = this.value;
         if (value < minVal) {
            value = minVal;
            this.value = minVal;
         }
         if (value > maxVal) {
            value = maxVal;
            this.value = maxVal;
         }
         var cosVal = Math.cos(this.value * Math.PI / 180), sinVal = Math.sin(this.value * Math.PI / 180);
         var valTransform = 'matrix('+ cosVal.toFixed(6) +','+ sinVal.toFixed(6) +','+ (-1 * sinVal).toFixed(6) +','+ cosVal.toFixed(6) +',0,0)'
         eleDetail.innerHTML = '目前属性值为：' + valTransform;
         $css3Transform(eleBox, valTransform);
      });   
   }    
})();
```

## 拉伸\(skew\)

matrix\(1,tan\(αy\),tan\(αx\),1,0,0\)

公式:

x = x+y\*tan\(αx\)+0=x+y\*tan\(αx\)

y = x\*tan\(αy\)+y+0 = x\*tan\(αy\)+y

其中,αx表示x轴倾斜的角度，αy表示y轴

学习地址:[http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/](http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)

```
CSS代码：
.matrix_box {
    width: 150px;
    height: 150px;
    line-height: 130px;
    background-color: #a0b3d6;
    font-size: 60px;
    text-align:center;
    text-shadow:1px 1px #fff;
}
HTML代码：
<p id="matrixDetail">目前属性值为：matrix(1,0,0,1,0,0)</p>
<p>请输入角度(0~360)：<input type="text" id="matrixRotate" value="0" min="0" max="360" autocomplete="off" /></p>
<div id="matrixBox" class="matrix_box">↑</div>
JS代码：
(function() {
   var $ = function(selector) {
      return document.querySelector(selector);
   };
   var $css3Transform = function(element, value) {
      // 应用transform属性值，与之前demo雷同，略……
   };
   var eleDetail = $("#matrixDetail"),
      eleRotate = $("#matrixRotate"),
      eleBox = $("#matrixBox");

   if (eleDetail && eleRotate && eleBox) {
      eleRotate.addEventListener("change", function() {
         var maxVal = this.getAttribute("max"), minVal = this.getAttribute("min"), value = this.value;
         if (value < minVal) {
            value = minVal;
            this.value = minVal;
         }
         if (value > maxVal) {
            value = maxVal;
            this.value = maxVal;
         }
         var cosVal = Math.cos(this.value * Math.PI / 180), sinVal = Math.sin(this.value * Math.PI / 180);
         var valTransform = 'matrix('+ cosVal.toFixed(6) +','+ sinVal.toFixed(6) +','+ (-1 * sinVal).toFixed(6) +','+ cosVal.toFixed(6) +',0,0)'
         eleDetail.innerHTML = '目前属性值为：' + valTransform;
         $css3Transform(eleBox, valTransform);
      });   
   }    
})();
```

## 镜像对称

轴围绕的那个点就是CSS3中transform变换的中心点，自然，镜像对称也不例外。因为该轴永远经过原点，因此，任意对称轴都可以用y=k\*x表示。则matrix表示就是：

```
matrix((1-k*k) / (1+k*k), 2k / (1 + k*k), 2k / (1 + k*k), (k*k - 1) / (1+k*k), 0, 0)
```

学习地址:[http://www.zhangxinxu.com/study/201206/css3-transform-matrix-mirror.html](http://www.zhangxinxu.com/study/201206/css3-transform-matrix-mirror.html)

```
HTML代码：
<p id="matrixDetail">目前属性值为：matrix(1,0,0,1,0,0)</p>
<div class="matrix_image">
   <div id="matrixLine" class="matrix_line"></div>
    <input type="text" id="matrixInput" class="matrix_input" autocomplete="off" placeholder="输入角度确定镜像对称轴" />
   <img id="matrixImage" src="/image/study/s/s256/mm1.jpg" width="256" height="191" />
</div>
JS代码：
(function() {
   var $ = function(selector) {
      return document.querySelector(selector);
   };
   var $css3Transform = function(element, value) {
      var arrPriex = ["O", "Ms", "Moz", "Webkit", ""], length = arrPriex.length;
      for (var i=0; i < length; i+=1) {
         element.style[arrPriex[i] + "Transform"] = value;
      }
   };
   var eleDetail = $("#matrixDetail"), eleInput = $("#matrixInput"),
      eleLine = $("#matrixLine"), eleImage = $("#matrixImage");

   if (eleDetail && eleInput && eleImage) {
      eleInput.addEventListener("change", function() {
         var value = parseInt(this.value, 10);
         if (value) {
            $css3Transform(eleLine, "rotate("+ value +"deg)");
            // 确认对称线
            var k = Math.tan( -1 * value * Math.PI / 180),
               ux = 1 / Math.sqrt(1 + k * k), uy = k / Math.sqrt(1 + k * k);

            if (k > 1000000) {
               ux = 0, uy = 1;
            } else if (k < -1000000) {
               ux = 0, uy = -1;
            }            

            var valTransform = "matrix("+ (2*ux*ux-1).toFixed(6) +","+ (2*ux*uy).toFixed(6) +","+ (2*ux*uy).toFixed(6) +","+ (2*uy*uy-1).toFixed(6) +",0,0)";
            eleDetail.innerHTML = '目前属性值为：' + valTransform;
            $css3Transform(eleImage, valTransform);
         } else {
            this.value = "";   
         }
      });
   }
   }   
})();
```

---

## 新的转换属性

下面的表格列出了所有的转换属性：

| 属性 | 描述 |
| :--- | :--- |
| transform | 向元素应用 2D 或 3D 转换。 |
| transform-origin | 允许你改变被转换元素的位置。 |

## 2D Transform 方法

| 函数 | 描述 |
| :--- | :--- |
| matrix\(n,n,n,n,n,n\) | 定义 2D 转换，使用六个值的矩阵。 |
| translate\(x,y\) | 定义 2D 转换，沿着 X 和 Y 轴移动元素。 |
| translateX\(n\) | 定义 2D 转换，沿着 X 轴移动元素。 |
| translateY\(n\) | 定义 2D 转换，沿着 Y 轴移动元素。 |
| scale\(x,y\) | 定义 2D 缩放转换，改变元素的宽度和高度。 |
| scaleX\(n\) | 定义 2D 缩放转换，改变元素的宽度。 |
| scaleY\(n\) | 定义 2D 缩放转换，改变元素的高度。 |
| rotate\(angle\) | 定义 2D 旋转，在参数中规定角度。 |
| skew\(x-angle,y-angle\) | 定义 2D 倾斜转换，沿着 X 和 Y 轴。 |
| skewX\(angle\) | 定义 2D 倾斜转换，沿着 X 轴。 |
| skewY\(angle\) | 定义 2D 倾斜转换，沿着 Y 轴。 |




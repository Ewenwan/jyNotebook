## html
全称“hyperText markup language”


### 基础标签
* 标签由一对```<>```和```</>```包括 
	* 例如:
	 * <html >和< /html>
* 中文乱码问题 
	* 在head标签中添加```<meta charset="utf-8"/>```
	* 在html中添加属性值,例如:```<html lang="en">```
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
* del标签:删除线，例如:```<del>12元</del>```显示为<del>12元</del>
* address标签:一般用于地址
* div标签:差不多效果与p标签差不多，用于布局
* span标签
* div和span:充当容器，便于分块，结构化，便于维护

### 高级标签
* html编码:以&开头";"结尾
 * 空格:```&nbsp;```
 * 小于:	```&lt;```
 * 大于:```&gt;```
 * 水平线:```<hr/>```
* 有序列表
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
   * a
   * ..
  
  ```
  <ol type="A">
	<li>喜羊羊</li>
	<li>Fate</li>
	<li>绝对双刃</li>
  </ol>
  ```


<ol type="A">
  <li>喜羊羊</li>
  <li>Fate</li>
  <li>绝对双刃</li>
</ol>
 	
 

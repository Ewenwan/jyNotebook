# 2.2.3 节点树及节点间的关系

在 HTML DOM 中，所有事物都是节点。DOM 是被视为节点树的 HTML。

## DOM 节点

根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点：

* 整个文档是一个文档节点
* 每个 HTML 元素是元素节点
* HTML 元素内的文本是文本节点
* 每个 HTML 属性是属性节点
* 注释是注释节点

## HTML DOM 节点树

HTML DOM 将 HTML 文档视作树结构。这种结构被称为_节点树_：

### HTML DOM Tree 实例

![HTML DOM Node Tree](http://www.w3school.com.cn/i/ct_htmltree.gif)

通过 HTML DOM，树中的所有节点均可通过 JavaScript 进行访问。所有 HTML 元素（节点）均可被修改，也可以创建或删除节点。

## 节点父、子和同胞

节点树中的节点彼此拥有层级关系。

父（parent）、子（child）和同胞（sibling）等术语用于描述这些关系。父节点拥有子节点。同级的子节点被称为同胞（兄弟或姐妹）。

* 在节点树中，顶端节点被称为根（root）
* 每个节点都有父节点、除了根（它没有父节点）
* 一个节点可拥有任意数量的子
* 同胞是拥有相同父节点的节点

下面的图片展示了节点树的一部分，以及节点之间的关系：

![DOM &#x8282;&#x70B9;&#x5173;&#x7CFB;](http://www.w3school.com.cn/i/dom_navigate.gif)

本段参考:[http://www.w3school.com.cn/htmldom/dom\_nodes.asp](http://www.w3school.com.cn/htmldom/dom_nodes.asp)


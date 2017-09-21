---
title: CSS系列——盒模型
date: 2017-09-20 14:53:13
tags:
    - CSS系列
    - 盒模型
    - CSS
---

CSS盒子模型是网页布局的基础——每一个元素都被表示成一个矩形框，盒子的内容、填充、边框和边缘都是像洋葱的层次一样互相叠起来的。当浏览器呈现一个WEB页面布局时，它会计算出什么样式应用于每个框的内容、周围的洋葱有多大，以及这些盒子之间的位置。在了解了CSS盒模型之后，我们就能够更好的用CSS对页面进行布局了。

#### 1. 盒模型包括那些内容
每个盒子包括如下几个部分：
* 外边距（margin）
* 边框（border）
* 内边距（padding）
* 内容（width）

**外边距(margin)**——用空白区域扩展边框外部的透明部分，以分开相邻的元素
**边框(border)**——围绕在内边距和内容外的边框
**内边距(padding)**——是位于边框和内容中间的那片空白区域（如果设置的话）
**内容(width)**——又被有些地方称为content area是包含元素真实内容的区域，它通常包含背景、颜色或者图片等，位于内边距的内部。

如下图：
![盒模型](https://leohxj.gitbooks.io/front-end-database/html-and-css-basic/assets/box-model.svg)

#### 2. 几种不同的盒模型和它们计算实际大小的形式
以现代浏览器是否支持box-sizing属性为分界点，来谈谈不同的盒模型和它们的计算方式

**在box-sizing支持前**

盒模型被定义为两种类型：
1. W3C标准盒模型
2. IE盒模型

**W3C标准盒模型**
也是我们通常说的盒模型，计算盒模型实际占据的区域大小是这样的：
> 实际宽度 = margin(left+right) + border(left+right) + padding(left+right) + width(定义的值)
> 实际高度 = marging(top+bottom) + border(top+bottom) + padding(top+bottom) + height(定义的值)

通过margin调整两个元素之间的距离，用padding调整内容和元素边框之间的距离，这种计算盒模型的方式是**W3C标准盒模型**，也是其它地方说的**Box盒模型**。

**IE盒模型**

思考这样一个问题，当我们为元素定义了一个固定的宽度（高度）值后，如果修改padding，元素在页面上所占的宽度（高度）也会随着padding的值的变化而变化。同理当想要调整padding的值，而希望保持元素在页面上所占的宽度（高度）固定，还需要修改元素的width。

在日常生活中的盒子，当我们定义它的大小时，绝对不会使用盒子中存放的物品的尺寸来定义盒子的大小。对于这个盒子来说，外围的挡板可以看成border，防止物品破损的填充物可以看成padding，在现实中，当我们说一个盒子有多大时，指的就是它的实际大小，也就是 “border+padding+contentWidth”。

可能IE是考虑到了上面的问题，所以IE盒模型实际计算占据的区域大小是：
> 实际宽度 = margin(left+right) + width(定义的值，该值包含了border左右和padding左右的大小)
> 实际高度 = margin(top+bottom) + height(定义的值，该值包含了border上下和padding上下的大小)

IE盒模型计算盒模型的方式依然和标准盒模型一样：内容+内边距+边框+外边距，只不过在IE盒模型当中内容大小其实已经包含了内边距和边框，也就是说：width = border(left+right) + padding(left+right) + contentWidth(内容大小)；

**在box-sizing支持后**
box-sizing是CSS3添加用来改变计算盒模型的方式的一个属性，属性值有：
1. content-box
2. padding-box
3. border-box

**content-box**——也是box-sizing的默认值，计算盒模型的方式和"W3C标准盒模型"一样

> 布局所占宽度Width：
> Width = width + padding-left + padding-right + border-left + border-right + margin-left + margin-right  

> 布局所占高度Height:
> Height = height + padding-top + padding-bottom + border-top + border-bottom + margin-left + margin-right


**padding-box**
> 布局所占宽度Width：
> Width = width(包含padding-left + padding-right) + border-top + border-bottom + margin-left + margin-right  

> 布局所占高度Height:
> Height = height(包含padding-top + padding-bottom) + border-top + border-bottom + margin-left + margin-right

**border-box**——计算盒模型实际的大小方式和"IE盒模型”一样
> 布局所占宽度Width：
> Width = width(包含padding-left + padding-right + border-left + border-right) + margin-left + margin-right  

> 布局所占高度Height:
> Height = height(包含padding-top + padding-bottom + border-top + border-bottom) + margin-left + margin-right

#### box-sizing属性

#### 盒模型不同的表现

#### margin外边距叠加
在CSS中，两个或多个毗邻（父子元素或兄弟元素）的普通文档流的款元素垂直方向上的margin会发生叠加。这种方式形成的外边距即可称为外边距叠加（collapsed margin）

> 何为毗邻：是指没有被非空内容，padding、border或clear分隔开。
> 何为普通流：除浮动（float）、绝对定位(position)外的代码即为普通流。

**一般来说， 垂直外边距叠加有三种情况：**

*1.元素自身叠加*：当元素没有内容（即空元素）、内边距、边框时，它的上下边距就相遇了，即会产生叠加（垂直方向）。当为元素添加内容、内边距、边框任何一项，就会取消叠加。

*2.相邻元素叠加*：相邻的两个元素，如果它们的上下边距相遇，即会产生叠加。

*3.包含（父子）元素叠加*：包含元素的外边距隔着父元素的内边距和边框，当这两项都不存在的时候，父子元素垂直外边距相邻，产生叠加。

1.父子外边距叠加
![父子](http://7b1evr.com1.z0.glb.clouddn.com/illustration%5CCollapsingct_css_margin_collapsing_example_2.gif)  


2.兄弟元素
![兄弟](http://7b1evr.com1.z0.glb.clouddn.com/illustration%5CCollapsingct_css_margin_collapsing_example_1.gif)  


3.空元素
![空](http://7b1evr.com1.z0.glb.clouddn.com/illustration%5CCollapsingct_css_margin_collapsing_example_3.gif)  


4.以上三种混合
![混合](http://7b1evr.com1.z0.glb.clouddn.com/illustration%5CCollapsingct_css_margin_collapsing_example_4.gif)


叠加发生了，肯定不是我们希望的情况，那如何避免呢？  
其实只要破坏上面讲到的四个条件中的任何一个即可：毗邻、两个或多个、普通流和垂直方向。

> 不叠加

* 浮动元素不会与任何元素发生叠加，也包括它的子元素
* 创建了 BFC 的元素不会和它的子元素发生外边距叠加
* 绝对定位元素和其他任何元素之间不发生外边距叠加，也包括它的子元素
* inline-block 元素和其他任何元素之间不发生外边距叠加，也包括它的子元素

> 叠加

* 普通流中的块级元素的margin-bottom永远和它相邻的下一个块级元素的 margin-top 叠加，除非相邻的兄弟元素 clear
* 普通流中的块级元素的margin-top和它的第一个普通流中的子元素发生margin-top叠加
* 普通流中的块级元素和它的最后一个普通流中的子元素发生 margin-bottom叠加
* 如果一个元素的 min-height 为0、没有 border、没有padding、高度为0或者auto、不包含子元素，那么它自身的外边距会发生叠加

**参考**
<http://geekplux.com/2014/03/14/collapsing_margins.html>
<http://justcode.ikeepstudying.com/2016/07/css-%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3bfc%E5%92%8Cmargin-collapse-margin%E5%8F%A0%E5%8A%A0%E6%88%96%E8%80%85%E5%90%88%E5%B9%B6%E5%A4%96%E8%BE%B9%E8%B7%9D/>
<http://www.hujuntao.com/web/css/css-margin-overlap.html>
<https://segmentfault.com/a/1190000010346113>

#### 盒模型应用


#### 受影响的盒模型



#### 参考
<https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model>
---
title: CSS系列——浏览器默认样式
date: 2017-09-20 15:23:00
tags: 
    - CSS
    - CSS默认样式
    - CSS系列
---

了解HTML标签在各浏览器当中的默认样式，可以让我们了解，为什么会要写Reset.css，Reset.css当中要怎么写样式最合理。
试着思考下面的问题：
* 为什么会有默认样式？
* 每个浏览器的默认样式有什么不同？
* Reset.css具体怎么写，每个浏览器展示的效果才会一致？

#### 默认样式
这里说的默认样式其实是每个浏览器自己的默认样式，我们通常使用style或者link的形式应用的样式内容被成为“用户样式”。  
浏览器加载完一个页面之后的工作流程大概如下：
1、转换
2、令牌化
3、词法分析
4、DOM树构建
5、CSSOM树构建
6、DOM树与CSSOM树合并后形成渲染树
7、通过布局计算每个对象显示的位置和大小
8、绘制页面

按照上面的流程，浏览器会查看文档当中是否有“用户样式”，如果没有就使用浏览器的默认样式，如果有就会用“用户样式”，就使用用户样式覆盖“浏览器默认样式”进行后面的渲染

#### 隐藏元素
我们知道HTML标签当中的head，title，meta,link,style,script元素默认是不展示的，就是因为浏览器的默认样式当中定义了display:none属性。
```
head,meta,title,link,style,script{
    display:none;
}
```
您可以通过定义如下代码在浏览器当中查看下效果
```
head{
    display:block;
    width:80px;
    height:80px;
    background:#f00;
}
```
#### 块元素


#### 行内元素


#### 参考
[GitHub仓库](https://github.com/sw4/revert.css)

[Chrom-blink](https://chromium.googlesource.com/chromium/blink/+/master/Source/core/css/html.css)
[Chrom-webkit](http://trac.webkit.org/browser/trunk/Source/WebCore/css/html.css)
[Opera-10.51](https://web.archive.org/web/20161031005401/http://www.iecss.com/opera-10.51.css)
[Internet Explorer](https://web.archive.org/web/20170122223926/http://www.iecss.com/)
[HTML4](https://www.w3.org/TR/CSS2/sample.html)
[HTML5](https://www.w3.org/TR/html5/rendering.html)
[浏览器渲染](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=zh-cn)
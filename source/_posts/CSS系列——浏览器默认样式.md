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
#### block元素
块元素的特点：
>1. 每个块元素都是从新的一行开始（独占一行）
2. 可以设置width,height,margin,border,padding
3. 可以嵌套其它标签元素
4. 默认块元素的宽度等于父元素的宽度
5. 可以通过定义display:block，把元素设置为块元素

HTML标签当中，那些被称为块元素的标签之所以有块元素的属性，是因为浏览器默认给它定义了display:block  
而不是因为是块元素才会有display:block属性。

**所有定义了display:block的元素，都是块元素**


```
html,
body,
p,
div,
layer,
article,aside,footer,header,hgroup,main,nav,section,
address,
blockquote,
figure,
center,
hr,
ol,ul,menu,dir,dd,dl,form,legend,fieldset,frameset,frame,details,summary
h1,h2,h3,h4,h5,h6{
    display:block;
}
```

#### inline元素
行内元素的特点：
>1. 和其它元素在同一行
2. width，height，margin-top,margin-bottom不可以控制元素的展现形式（定义无效）
3. margin-left,margin-right,和padding可以定义
4. 默认宽度是它所容纳内容的宽度
5. 通过定义display:block,可以把行内元素设置为块元素

所有的元素默认都是行内元素，也就是display:inline

```
q,
map,
area,
output
{
    display:inline;
}
```
#### display属性
html标签在浏览器当中是以那种布局形式展示，都是因为display属性的定义，display属性包含以下值：

```
基本值：    none | inline | block | list-item | inline-block
table系列： table | inline-table | table-caption | table-cell | table-row | table-row-group | table-column | table-columen-group | table-footer-group | table-header-group
css3新增： box | inline-box | flexbox | inline-flexbox | flex | inline-flex | run-in
```

**基本值**

>* none  隐藏元素
* inline    设置为行内元素
* block     设置为块元素
* inline-block  设置为inline-block
* list-item     设置为list-item

li标签默认定义的display:list-item，尝试定义如下的代码，在浏览器中查看：

```
    html
        <div class="list">
            <span class="item">1</span>
            <span class="item">2</span>
            <span class="item">3</span>
        </div>
    CSS
        .item{
            display:list-item;
        }        
```

**table系列**

>* table                 块元素的表格
* inline-table          行内元素的表格
* table-caption         定义表格头
* table-cell            表格单元格
* table-row             表格单元行
* table-row-group       单元行组
* table-column          表格列
* table-column-group    表格列组
* table-footer-group    表格底
* table-header-group    表格头

看下面一段代码
```
    <table>
        <caption>年龄列表</caption>
        <thead>
             <tr>
                <th>姓名</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tfoot>
            <tr>
                <td>年龄综合</td>
                <td>27</td>
            </tr>
        </tfoot>
        <tbody>
            <tr>
                <td>张三</td>
                <td>12</td>                
            </tr>
            <tr>
                <td>李四</td>
                <td>15</td>
            </tr>
        </tbody>        
    </table>
```
当我们使用thead定义表头的时候，默认显示的样式就是因为thead标签定义了display:table-header-group;
同样，tfoot就是因为定义了display:table-footer-group;
caption 就是因为定义了display:table-caption;

关于table系列，我们简单了解两个问题：
1. display:table和display:block的区别
2. display:table-cell如何做多列布局

block和table的区别
1、block宽度默认撑满父元素
2、table宽度根据内容而定

table-cell的多列布局
```
    <div class="main">
        <div class="left"></div>
        <div class="middle"></div>
        <div class="right"></div>
    </div>

    .main{ 
        width:500px;
        display:table;
    }
    .left,.middle,.right{
        display:table-cell;
        height:100px;
    }
    .left{
        width:20%;
        background:#ff0;
    }
    .middle{
        background:green;  
    }
    .right{
        width:10%;
        background:red;
    }

```
[在线查看](https://jsbin.com/roxelok/edit?html,css,output)

**CSS3系列**，主要定义了弹性布局相关的内容

>* box           弹性伸缩盒版本1
* inline-box    内联块弹性伸缩盒版本1
* flexbox       弹性伸缩盒版本2
* inline-flexbox内联块弹性伸缩盒版本2
* flex          弹性伸缩盒版本3
* inline-flex   内联块缩盒版本3
* run-in        根据上下文定义对象是内联还是块级

弹性伸缩盒以后我们有机会详细聊聊，这里说说几个点
1、box和inline-box，flexbox和inline-flexbox，flex和inline-flex之间的差异
2、run-in是如何根据上下文作用的

*第一个问题*

在需要有固定宽度的情况下的弹性布局使用flex，  
如果元素的宽度不固定，里面的标签还需要弹性布局的话，就是用inline-flex

我们通过以下代码来了解
[flex布局](https://jsbin.com/xacope/edit?html,css,output);
[inline-flex布局](https://jsbin.com/xuyadir/edit?html,css,output)



*第二个问题*

[这里](http://www.zhangxinxu.com/wordpress/2012/03/tip-css-multiline-display/)有详细的解释



#### 其它

**块元素**
![块](http://upload-images.jianshu.io/upload_images/3087126-f97fd0d8e6a4316c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**行内元素**
![行内](http://upload-images.jianshu.io/upload_images/3087126-8293f7598b1a5f90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**可变元素**
![可变](http://upload-images.jianshu.io/upload_images/3087126-e7a40d92f5d8c7a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

文章七七八八，扯了很多东西，有点乱，让看官们受累了

#### 参考
[GitHub仓库](https://github.com/sw4/revert.css)

[Chrom-blink](https://chromium.googlesource.com/chromium/blink/+/master/Source/core/css/html.css)
[Chrom-webkit](http://trac.webkit.org/browser/trunk/Source/WebCore/css/html.css)
[Opera-10.51](https://web.archive.org/web/20161031005401/http://www.iecss.com/opera-10.51.css)
[Internet Explorer](https://web.archive.org/web/20170122223926/http://www.iecss.com/)
[HTML4](https://www.w3.org/TR/CSS2/sample.html)
[HTML5](https://www.w3.org/TR/html5/rendering.html)
[浏览器渲染](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=zh-cn)
[解读默认样式](http://www.cnblogs.com/wangfupeng1988/p/4280801.html)
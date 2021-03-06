---
title: Markdown语法简要说明
date: 2017-09-13 15:24:47
tags: 
    - Markdown
    - 工具类
    - 编辑器
---
#### 什么是Markdown?
markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容有一定的格式——摘自百度百科。

简单理解就是，通过一种特有的写法，能够让普通的文本有一种更加优雅展现的语法，我们在各种编辑器里面能够用markdown语法，说明，该编辑器支持markdown语法，例如：有道云，vsCode，WebStrom，Atom，印象笔记(EverNote)等编辑器都支持markdown语法。  

markdown是为那些需要经常码字或者进行文字排版，对码字手速和排版顺畅度有要求的人群设计的。他们希望用键盘把文字内容打出来之后就已经排版好了，通常这部分人包括码弄、博客写手、网站编辑、出版业人士等等。

#### 语法介绍
markdown语法很简单，这里只说明一些简单的语法，也就是日常使用最频繁的内容，主要包括如下内容：

* 标题 
* 段落和换行
* 链接
* 列表
* 代码块
* 引用
* 其它

> 标题

```
    # 标题（一级标题）
    ## 标题 （二级标题）
    ### 标题 （二级标题）
    #### 标题 （二级标题）
    ##### 标题 （二级标题）    
```

> 段落和换行

```
    段落
    一个markdown短链是由一个或者多个连续的文本行组成，在文本的前后空行，就可以表示段落

    换行
    两个英文空格+回车键，就可以在段落当中进行换行了
```

> 链接

```
    [百度](http://www.baidu.com/)

    或者

    [百度][]
    [百度]:http://www.baidu.com/;
    
```


> 列表

```
    无需列表

    第一种：
    * 上海
    * 背景
    * 深圳
    * 北京
    
    第二种：
    + 上海
    + 背景
    + 深圳
    + 北京


    第三种：
    - 上海
    - 背景
    - 深圳
    - 北京
    
    有序列表
    1. 上海
    2. 背景
    3. 深圳
    4. 北京
    
```

> 代码块

```
    第一种：
    使用pre和code标签

    第二种：
    使用三个英文反点号
```

> 引用

```
    使用英文的左尖括号">"

```

> 其它

```
    图片：
    在链接的使用方法前面添加感叹号，例如：
    ![图片的alt说明文章](图片的地址)
    ![美女](https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo_top_ca79a146.png)

    或者

    ![美女][]
    [美女]:https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo_top_ca79a146.png

    自动链接：
    <http://example.com/>
    markdown会转成：<a href="http://example.com/">http://example.com/</a>


    反斜杠：
    \* 你好 \* 表示：* 你好 *

    强调：
    * 强调的文章 *
    - 强调的内容 -

    ** strong 标签的强调 **
    -- strong 标签的强调 --

```

#### 其它
写这份文章的目的，其实主要是为了更加的了解和熟悉markdown语法，因为自己工作的原因，经常会要码字。同时也是为了加深自己对markdown的理解，它还有一些高级的使用部分，如果您有兴趣还可以继续探索!

文章的大部分内容和观点参考如下网站：
<http://wowubuntu.com/markdown/basic.html>
<http://wowubuntu.com/markdown/index.html>

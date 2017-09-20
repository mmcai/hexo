---
title: HTTP,HTTP2.0,SPDY,HTTPS你应该知道的一些事
date: 2017-09-19 13:04:36
tags:
---
> 本文转载于：[HTTP,HTTP2.0,SPDY,HTTPS你应该知道的一些事](http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/)

作为一个经常和web打交道的程序员，了解这些协议是必须的，本文就向大家介绍一下这些协议的区别和基本概念，文中可能不局限于前端知识，还包括一些运维，协议方面的知识，希望能给读者带来一些收获，如有不对之处还请指出

#### 1. web始祖HTTP
全称：超文本传输协议(HyperText Transfer Protocol) 伴随着计算机网络和浏览器的诞生，HTTP1.0也随之而来，处于计算机网络中的应用层，HTTP是建立在TCP协议之上，所以HTTP协议的瓶颈及其优化技巧都是基于TCP协议本身的特性，例如tcp建立连接的3次握手和断开连接的4次挥手以及每次建立连接带来的RTT延迟时间。

#### 2.HTTP与现代化浏览器
早在HTTP建立之初，主要就是为了将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器。也是说对于前端来说，我们所写的HTML页面将要放在我们的web服务器上，用户端通过浏览器访问url地址来获取网页的显示内容，但是到了WEB2.0以来，我们的页面变得复杂，不仅仅单纯的是一些简单的文字和图片，同时我们的HTML页面有了CSS，Javascript，来丰富我们的页面展示，当ajax的出现，我们又多了一种向服务器端获取数据的方法，这些其实都是基于HTTP协议的。同样到了移动互联网时代，我们页面可以跑在手机端浏览器里面，但是和PC相比，手机端的网络情况更加复杂，这使得我们开始了不得不对HTTP进行深入理解并不断优化过程中。 
![HTTP协议发展流程](http://tenny.qiniudn.com/timeline.png)

#### 3.HTTP的基本优化
影响一个HTTP网络请求的因素主要有两个：带宽和延迟。
* **带宽：**如果说我们还停留在拨号上网的阶段，带宽可能会成为一个比较严重影响请求的问题，但是现在网络基础建设已经使得带宽得到极大的提升，我们不再会担心由带宽而影响网速，那么就只剩下延迟了。

* **延迟：**
1. **浏览器阻塞（HOL blocking）**：浏览器会因为一些原因阻塞请求。浏览器对于同一个域名，同时只能有 4 个连接（这个根据浏览器内核不同可能会有所差异），超过浏览器最大连接数限制，后续请求就会被阻塞。

2. **DNS 查询（DNS Lookup）**：浏览器需要知道目标服务器的 IP 才能建立连接。将域名解析为 IP 的这个系统就是 DNS。这个通常可以利用DNS缓存结果来达到减少这个时间的目的。

3.  **建立连接（Initial connection）**：HTTP 是基于 TCP 协议的，浏览器最快也要在第三次握手时才能捎带 HTTP 请求报文，达到真正的建立连接，但是这些连接无法复用会导致每次请求都经历三次握手和慢启动。三次握手在高延迟的场景下影响较明显，慢启动则对文件类大请求影响较大。


![TCP3次握手](http://tenny.qiniudn.com/3woshou.png)

#### 4.HTTP1.0和HTTP1.1的一些区别
HTTP1.0最早在网页中使用是在1996年，那个时候只是使用一些较为简单的网页上和网络请求上，而HTTP1.1则在1999年才开始广泛应用于现在的各大浏览器网络请求中，同时HTTP1.1也是当前使用最为广泛的HTTP协议。**主要区别主要体现在：**
1. 缓存处理，在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。
2. 带宽优化及网络连接的使用，HTTP1.0中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1则在请求头引入了range头域，它允许只请求资源的某个部分，即返回码是206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。
3. 错误通知的管理，在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。
4. Host头处理，在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应消息都应支持Host头域，且请求消息中如果没有Host头域会报告一个错误（400 Bad Request）。
5. 长连接，HTTP 1.1支持长连接（PersistentConnection）和请求的流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启Connection： keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点。以下是常见的HTTP1.0：

![区别1](http://tenny.qiniudn.com/host1.png)

![区别2](http://tenny.qiniudn.com/http11.png)

**区别用一张图来体现**
![HTTP1.0和HTTP1.1的区别](http://tenny.qiniudn.com/DIF12.png)

#### HTTP1.0和现存的一些问题
1. 上面提到过的，HTTP1.x在传输数据时，每次都需要重新建立连接，无疑增加了大量的延迟时间，特别是在移动端更为突出。
2. HTTP1.x在传输数据时，所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份，这在一定程度上无法保证数据的安全性。
3. HTTP1.x在使用时，header里携带的内容过大，在一定程度上增加了传输的成本，并且每次请求header基本不怎么变化，尤其在移动端增加用户流量。
4. 虽然HTTP1.x支持了keep-alive，来弥补多次创建连接产生的延迟，但是keep-alive使用多了同样会给服务端带来大量的性能压力，并且对于单个文件被不断请求的服务(例如图片存放网站)，keep-alive可能会极大的影响性能，因为它在文件被请求之后还保持了不必要的连接很长时间。

#### 6.HTTPS应声而出
为了解决以上问题，网景在1994年创建了HTTPS，并应用在网景导航者浏览器中。 最初，HTTPS是与SSL一起使用的；在SSL逐渐演变到TLS时（其实两个是一个东西，只是名字不同而已），最新的HTTPS也由在2000年五月公布的RFC 2818正式确定下来。简单来说，HTTPS就是安全版的HTTP，并且由于当今时代对安全性要求更高，chrome和firefox都大力支持网站使用HTTPS，苹果也在ios 10系统中强制app使用HTTPS来传输数据，由此可见HTTPS势在必行。

#### 7.HTTPS与HTTP的一些区别
1. HTTPS协议需要到CA申请证书，一般免费证书很少，需要交费。

2. HTTP协议运行在TCP之上，所有传输的内容都是明文，HTTPS运行在SSL/TLS之上，SSL/TLS运行在TCP之上，所有传输的内容都经过加密的。

3. HTTP和HTTPS使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。

4. HTTPS可以有效的防止运营商劫持，解决了防劫持的一个大问题。

![7-1](http://tenny.qiniudn.com/HTTPQUBIE2.png)

#### 8.HTTPS改造
**如果一个网站要全站由HTTP替换成HTTPS，可能需要关注以下几点：**
1. 安装CA证书，一般的证书都是需要收费的，这边推荐一个比较好的购买证书网站：1）Let's Encrypt，免费，快捷，支持多域名（不是通配符），三条命令即时签署+导出证书。缺点是暂时只有三个月有效期，到期需续签。2Comodo PositiveSSL，收费，但是比较稳定。

2. 在购买证书之后，在证书提供的网站上配置自己的域名，将证书下载下来之后，配置自己的web服务器，同时进行代码改造。

3. HTTPS 降低用户访问速度。SSL握手，HTTPS 对速度会有一定程度的降低，但是只要经过合理优化和部署，HTTPS 对速度的影响完全可以接受。在很多场景下，HTTPS 速度完全不逊于 HTTP，如果使用 SPDY，HTTPS 的速度甚至还要比 HTTP 快。

4. 相对于HTTPS降低访问速度，其实更需要关心的是服务器端的CPU压力，HTTPS中大量的密钥算法计算，会消耗大量的CPU资源，只有足够的优化，HTTPS 的机器成本才不会明显增加。

推荐一则[淘宝网改造HTTPS](http://velocity.oreilly.com.cn/2015/ppts/lizhenyu.pdf)的文章。  
#### 9.使用SPDY加快你的网站速度
2012年google如一声惊雷提出了SPDY的方案，大家才开始从正面看待和解决老版本HTTP协议本身的问题，SPDY可以说是综合了HTTPS和HTTP两者有点于一体的传输协议，主要解决：
1. 降低延迟，针对HTTP高延迟的问题，SPDY优雅的采取了多路复用（multiplexing）。多路复用通过多个请求stream共享一个tcp连接的方式，解决了HOL blocking的问题，降低了延迟同时提高了带宽的利用率。

2. 请求优先级（request prioritization）。多路复用带来一个新的问题是，在连接共享的基础之上有可能会导致关键请求被阻塞。SPDY允许给每个request设置优先级，这样重要的请求就会优先得到响应。比如浏览器加载首页，首页的html内容应该优先展示，之后才是各种静态资源文件，脚本文件等加载，这样可以保证用户能第一时间看到网页内容。

3. header压缩。前面提到HTTP1.x的header很多时候都是重复多余的。选择合适的压缩算法可以减小包的大小和数量。

4. 基于HTTPS的加密协议传输，大大提高了传输数据的可靠性。

5. 服务端推送（server push），采用了SPDY的网页，例如我的网页有一个sytle.css的请求，在客户端收到sytle.css数据的同时，服务端会将sytle.js的文件推送给客户端，当客户端再次尝试获取sytle.js时就可以直接从缓存中获取到，不用再发请求了。SPDY构成图：

![9-1](http://tenny.qiniudn.com/SPDY.png)

SPDY位于HTTP之下，TCP和SSL之上，这样可以轻松兼容老版本的HTTP协议(将HTTP1.x的内容封装成一种新的frame格式)，同时可以使用已有的SSL功能。

![9-2](http://tenny.qiniudn.com/sodyuse.png)

#### 10. HTTP2.0的前世今生
顾名思义有了HTTP1.x，那么HTTP2.0也就顺理成章的出现了。HTTP2.0可以说是SPDY的升级版（其实原本也是基于SPDY设计的），但是，HTTP2.0 跟 SPDY 仍有不同的地方，主要是以下两点：
* HTTP2.0 支持明文 HTTP 传输，而 SPDY 强制使用 HTTPS
* HTTP2.0 消息头的压缩算法采用 HPACK，而非 SPDY 采用的 DEFLATE
#### 11.
#### 12.HTTP2.0的升级改造
**对比HTTPS的升级改造，HTTP2.0或许会稍微简单一些，你可能需要关注以下问题：**
1. 前文说了HTTP2.0其实可以支持非HTTPS的，但是现在主流的浏览器像chrome，firefox表示还是只支持基于 TLS 部署的HTTP2.0协议，所以要想升级成HTTP2.0还是先升级HTTPS为好。

2. 当你的网站已经升级HTTPS之后，那么升级HTTP2.0就简单很多，如果你使用NGINX，只要在配置文件中启动相应的协议就可以了，可以参考NGINX白皮书，NGINX配置HTTP2.0官方指南。

3. 使用了HTTP2.0那么，原本的HTTP1.x怎么办，这个问题其实不用担心，HTTP2.0完全兼容HTTP1.x的语义，对于不支持HTTP2.0的浏览器，NGINX会自动向下兼容的。

#### 后记
1. 以上就是关于HTTP,HTTP2.0,SPDY,HTTPS的一些基本理论，有些内容没有深入讲解，大家可以跟进参考连接具体查看。

2. 关于HTTP1.x的一些优化方式，例如文件合并压缩，资源cdn，js，css优化等等同样使用与HTTP2.0和HTTPS，所以web前端的优化，还是要继续进行。

3. 其实WEB发展如此迅速的今天，有些技术是真的要与时俱进的，就像苹果宣布ios 10必须使用HTTPS开始，关于web协议革新就已经开始了，为了更好的性能，更优越的方式，现在就开始升级改造吧

#### 参考
<https://ye11ow.gitbooks.io/http2-explained/content/>
<https://developers.google.com/web/fundamentals/performance/http2/?hl=zh-cn>
<https://github.com/creeperyang/blog/issues/23>
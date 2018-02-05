## 关于缓存优化的杂谈

### 引言

这篇文章还没整理完善，很多地方需要补充，这里的内容我只是暂时用于类似于画重点给我自己看，等有空会整理，浏览的朋友不要喷哦。

app端
-

	app端的话一般有脚本（css，js），图片，音像多媒体
	
pc端、web端
-
	常用手段就是服务器端配置HTTP的Expires（有效时长）和Cache-Control（是否缓存）

**http叙述：**

	http（超文本传输​​协议）是用于传输诸如HTML的超媒体文档的应用层协议。它被设计用于Web浏览器和Web服务器之间的通信，但它也可以用于其他目的。
	
	HTTP是一种能够获取如 HTML 这样的网络资源的 protocol(通讯协议)。它是在 Web 上进行数据交换的基础，是一种 client-server 协议，也就是说，请求通常是由像浏览器这样的接受方发起的。一个完整的Web文档通常是由不同的子文档拼接而成的，像是文本、布局描述、图片、视频、脚本等等。
	
![客户端于服务端交互](1.png)
	
**获取数据的叙述：**

	从服务端获取数据最常用的方式还是通过HTTP请求，给服务器发请求的时候有请求头，接受服务器响应的时候有响应头，客户端和服务器端互相沟通需要的信息都是通过这些“头”来传送，这些信息是一些类似key:value的键值对
	
**关于Cache-Control：**
	
	常见的值有有private、public、no-store、no-cache、must-revalidate、max-age等。
	no-cache、must-revalidate值，如：
		Cache-Control: no-cache
		Cache-Control: max-age=60, must-revalidate
		
+ no-cache: 告诉浏览器、缓存服务器，不管本地副本是否过期，使用资源副本前，一定要到源服务器进行副本有效性校验。

+ must-revalidate：告诉浏览器、缓存服务器，本地副本过期前，可以使用本地副本；本地副本一旦过期，必须去源服务器进行有效性校验。

可参考链接：[web性能优化之：no-cache与must-revalidate深入探究](https://segmentfault.com/a/1190000007317481)

**关于前端请求头及缓存设置：**

1.可参考：[Meta http-equiv属性与HTTP头的Expires中（Cache-control）](httpMeta.md)

2.js和css更新都可以通过更改文件名达到更新的目的；

3.可参考[前端必备HTTP技能之HTTP请求头响应头中常用字段详解](https://www.jianshu.com/p/6e86903d74f7)

**关于缓存更新**

可参考:

1.[浅谈前端性能优化（一）——Expires和Cache-Control](http://blog.csdn.net/zhouziyu2011/article/details/71312452)

2.[前端必须知道的http缓存](https://segmentfault.com/a/1190000009652182)

3.[HTTP 缓存的四种风味与缓存策略](https://segmentfault.com/a/1190000006689795#articleHeader10)

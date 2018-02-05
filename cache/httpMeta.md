### Meta http-equiv属性与HTTP头的Expires中（Cache-control）

1、Expires(期限) 

	说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。 
	用法：
	＜meta http-equiv="expires" content="Wed, 20 Jun 2007 22:33:00 GMT"＞
	注意：必须使用GMT的时间格式。 
	
2、Pragma(cache模式) 

	说明：是用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出 
	用法：
	＜meta http-equiv="Pragma" content="no-cache"＞
	注意：这样设定，访问者将无法脱机浏览。
	
3、Refresh(刷新)

	说明：自动刷新并指向新页面。 
	用法：
	＜meta http-equiv="Refresh" content="2；URL=http://www.net.cn/"＞
	注意：其中的2是指停留2秒钟后自动刷新到URL网址。

4、Set-Cookie(cookie设定)

	＜meta http-equiv="Set-Cookie" content="cookievalue=xxx;expires=Wednesday, 20-Jun-2007 22:33:00 GMT； path=/"＞
	注意：必须使用GMT的时间格式。
	
5、Window-target(显示窗口的设定) 

	说明：强制页面在当前窗口以独立页面显示。 
	用法：
	＜meta http-equiv="Window-target" content="_top"＞
	注意：用来防止别人在框架里调用自己的页面。
	
6、content-Type(显示字符集的设定) 

	说明：设定页面使用的字符集。 
	用法：
	＜meta http-equiv="content-Type" content="text/html; charset=gb2312"＞

7、Pics-label(网页等级评定) 

	用法：
	<meta http-equiv="Pics-label" contect="">
	说明：在IE的internet选项中有一项内容设置，可以防止浏览一些受限制的网站，而网站的限制级别就是通过meta属性来设置的。
	
8、Page_Enter、Page_Exit 

	设定进入页面时的特殊效果
	<meta http-equiv="Page-Enter" contect="revealTrans(duration=1.0,transtion=12)">
	Duration的值为网页动态过渡的时间，单位为秒。  
	Transition是过渡方式，它的值为0到23，分别对应24种过渡方式。如下表：  
	0    盒状收缩    1    盒状放射  
	2    圆形收缩    3    圆形放射  
	4    由下往上    5    由上往下  
	6    从左至右    7    从右至左  
	8    垂直百叶窗    9    水平百叶窗  
	10    水平格状百叶窗    11垂直格状百叶窗  
	12    随意溶解    13从左右两端向中间展开  
	14从中间向左右两端展开    15从上下两端向中间展开  
	16从中间向上下两端展开    17    从右上角向左下角展开  
	18    从右下角向左上角展开    19    从左上角向右下角展开  
	20    从左下角向右上角展开    21    水平线状展开  
	22    垂直线状展开    23    随机产生一种过渡方式  
	
9、清除缓存（再访问这个网站要重新下载！）

	<meta http-equiv="cache-control" content="no-cache">
	
	1 数据包中的格式：
	 2 
	 3 Cache-Control: cache-directive
	 4 
	 5 cache-directive可以为以下：
	 6 
	 7 request时用到：
	 8 
	 9 | "no-cache"
	10 | "no-store"
	11 | "max-age" "=" delta-seconds
	12 | "max-stale" [ "=" delta-seconds ]
	13 | "min-fresh" "=" delta-seconds
	14 | "no-transform"
	15 | "only-if-cached"
	16 | "cache-extension"
	17 response时用到：
	18 
	19 | "public"
	20 | "private" [ "=" <"> field-name <"> ]
	21 | "no-cache" [ "=" <"> field-name <"> ]
	22 | "no-store"
	23 | "no-transform"
	24 | "must-revalidate"
	25 | "proxy-revalidate"
	26 | "max-age" "=" delta-seconds
	27 | "s-maxage" "=" delta-seconds
	28 | "cache-extension"
	29 部分说明：
	30 根据是否可缓存分为
	31 Public 指示响应可被任何缓存区缓存。
	32 Private 指示对于单个用户的整个或部分响应消息，不能被共享缓存处理。这允许服务器仅仅描述当用户的
	33 部分响应消息，此响应消息对于其他用户的请求无效。
	34 no-cache 指示请求或响应消息不能缓存（HTTP/1.0用Pragma的no-cache替换）
	35 根据什么能被缓存
	36 no-store 用于防止重要的信息被无意的发布。在请求消息中发送将使得请求和响应消息都不使用缓存。
	37 根据缓存超时
	38 max-age 指示客户机可以接收生存期不大于指定时间（以秒为单位）的响应。
	39 min-fresh 指示客户机可以接收响应时间小于当前时间加上指定时间的响应。
	40 max-stale 指示客户机可以接收超出超时期间的响应消息。如果指定max-stale消息的值，那么客户机可以
	41 接收超出超时期指定值之内的响应消息。
	42 Expires 表示存在时间，允许客户端在这个时间之前不去检查（发请求），等同max-age的
	43 效果。但是如果同时存在，则被Cache-Control的max-age覆盖。
	44 格式：
	45 Expires = "Expires" ":" HTTP-date
	46 例如
	47 Expires: Thu, 01 Dec 1994 16:00:00 GMT （必须是GMT格式）
	48 
	49 2.应用
	50 通过HTTP的META设置expires和cache-control
	51 <meta http-equiv="Cache-Control" content="max-age=7200" />
	52 <meta http-equiv="Expires" content="Mon, 20 Jul 2009 23:00:00 GMT" />
	53 上述设置仅为举例，实际使用其一即可。这样写的话仅对该网页有效，对网页中的图片或其他请求无效，并不会做任何cache。
	54 这样客户端的请求就多了，尽管只是检查Last-modified状态的东西，但是请求一多对浏览速度必定有影响。
	55 如果要对文件添加cache可以通过apache的mod_expire模块，写法为
	56 <IfModule mod_expires.c>
	57 ExpiresActive On
	58 ExpiresDefault "access plus 1 days"
	59 </IfModule>
	60 记得ExpiresActive设为On，我起先没设置On，似乎怎样YSlow都查不到缓存机制。这样添加的话就是默认所有的。
	61 如果要针对个别MIME类型则可以：
	62 ExpiresByType image/gif "access plus 5 hours 3 minutes"
	63 见 Apache Module mod_expires
	64 另外，当点击浏览器上的刷新，客户端发送的请求中均是max-age=0，表示validate操作，发送请求到服务器
	65 要求检查cache，再更新cache，一般得到的是304 Not Modified，表示没变动。
	具体用法
	
10、设定网页的到期时间 

	<meta http-equiv="expires" content="0">

11、关键字,给搜索引擎用的 

	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">

12.页面描述 

	<meta http-equiv="description" content="This is my page">

## 关于前端的一些杂谈

叙述
-
**为什么要写这些呢?**

* 更好地促进代码实践、管理、移植和维护
* 总结经验方便下次遗忘后查找

关于css
-

**css规则**

项目代码库结构
-

**以vue-cli项目作为结构示意图：**

	project root
		└── src
		     ├── styles
		            ├── bootstrap-custom
		            ├── custom
		            ├── font
		            ├── img
		            ├── variables
		            └── styles.scss
		     ├── demos
		     └── components
		            ├── alerts       
		                  └── alert.scss   // alert组件的自定义样式。每个组件都有自己的样式表，可以定制它，防止代码臃肿和样式泄露
			 ├── fonts
			 		├── iconfont.scss
			 		├── iconfont.ttf
			 		└── iconfont.woff
			 ├── assets
			 ├── base-pages
			 		├── home
			 			  ├── home.vue
			 		├── login
			 			  ├── login.vue
			 		├── register
			 			  ├── register.vue
			 ├── campaign-pages
			 		├── home
			 			  ├── home-adv.vue
			 		├── store
			 			  ├── store-adv.vue
			 ├── vconsole
			 		├── vconsole.vue
			 ├── routers
			 		├── index.js
			 		├── router.js
			 		└── children.js
			 ├── plugins
			 ├── libs
			 ├── apis
			 		├── index.js
			 		└── api.js
			 ├── stores
			 		├── index.js
			 		└── modules
			 			  ├── getter.js
				 		  ├── actions.js
				 		  └── mutation.js
			 ├── utils
			 		├── toolkit.js
			 		├── regEx.js
			 ├── config
			 		├── index.js
			 		├── oauth.js
			 		
**代码库结构叙述：**

* 做好每个css文件内代码注释

* “styles”文件夹是存放样式，这里的样式应该在应用的任何地方都可用：

	* 基础要用的css都在style.scss里@import进来
	
	* “bootstrap-custom”文件夹是放覆盖bootstrap基础样式的自定义样式
	
	* “custom”文件夹是放项目自定义样式（对应该项目的样式）
	
	* “fonts”文件夹是常用字体样式
	
	* “img”文件夹是常用图片样式
	
	* “variables”文件夹是自定义主题中使用的变量（比如主题色，按钮颜色，字体大小等）
	
	* “style.scss”文件是全局所有基本样式（清除按钮、列表、标题等的样式，还有设置初始化主题色等）

* “demos”文件夹是放演示样式和交互的示例

* “components”文件夹是用来存放组件的css（也可以用.vue文件集合在一起，不单独放出来），例如：alert，button，toast

* “fonts”用于存放字体库图标的文件（iconfont的文件）

* “assets”用于存放资源文件（常见就是音像图）

* “base-pages”用于存放基础页面

* “campaign-pages”用于存放相关页面的促销活动页，如：home页面的home-adv.vue

* “vconsole”用于页面显示调试结果（层级最高，配合vuex使用）

* “router”用于存放路由配置等

* “plugins”用于存放插件（swiper等）

* “lib”用于存放第三方库（iscroll，jq，zepto和bootstrap等）

* “api”用于存放接口、ajax（axios）拦截器等请求配置
	
	* “index.js”用于配置请求，拦截器等基础配置
	* “api.js”存放接口

* “store”用于存放vuex配置等
	
	* modules用于存放每个路由模块的子路由配置等

* “utils”用于存放一些实用的功能

	* “toolkit.js”用于存放常用功能代码块，如:1.判断数组里是否包含某个元素;2.倒计时.
	
	* “regEx.js”用于存放常用正则表达式验证
	
* “config”用于全局页面的逻辑
	
	* oauth.js用于登陆访问权限的验证逻辑
	* index.js用于蒙版、弹出框、登陆访问权限等的弹出

Note：文件夹中有index等多个文件，则一般其他文件最后都是应用在该文件夹的index文件里，这是为了其他地方方便统一管理



关于app方面
-

所有的页面最好统一初始化都是正在加载中的加载方式，等该页面的显示区域的数据请求完毕后显示

**启动页加载（splash）：**

作用：

* 用于给底层api和sdk等的加载提供缓冲时间，最好是图片logo和加载的动画效果就可以了，简洁突出，降低启动加载时间并提升用户体验

**引导页首屏显示(guide)**

作用：

* 用于引导用户介绍使用app（常用滑动切换页面）或是三秒钟广告页显示，也可以不用，具体根据业务需求

**首页**

作用：

* 用于显示app具体内容，常见是用tab方案来做首页内容切换，tab方案又有两种实现方式：

	* webview方案，如果有引导页，则所有tab页面都可以初始化请求数据出来，如果没有，则初始化显示第一个页面（没有引导页则第一个页面就是首屏页面）
	
	* H5方案，可以使用路由的方式，使用vue也是不错的选择

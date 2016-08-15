#css
##less、sass、stylus
```javascript
1.变量声明：less使用@声明变量，sass使用$，stylus使用$或者直接定义
2.使用规范：sass、less不用缩进，stylus也可以不用缩进，使用花括号，也可以缩进，但是缩进一定要匹配。
3.宿主问题：less、stylus、是nodejs的东西，sass搜riby的
4.条件判断：sass和stylus有if判断，less只有when
5.难度：sass<less<stylus      //>
6.函数:都有大量函数、mixins
```

##css3
```css
1.边框：border-radius,box-shadow,border-image
2.背景：background-size，background-origin（可以设置content、padding、border这三种）
3.文本效果：text-shadow、word-wrap
4.字体：可以使用font-face自定义，将自定义的名字和路径定义在font-face中即可
5.2D转换：translate移动（给定横纵坐标），rotate旋转（顺时针转，负数为逆时针），  scale缩放（横纵缩放的倍数，字体也跟着缩放），skew翻转（围绕x和y轴翻转角度），
  matrix（把所有2D转换方法组合在一起，没有研究） 
6.3D转换：每个2D方法都可以放到XYZ轴进行3D转换
7.过渡：transition，ie9及以下不支持，chrome25及之早的需要添加前缀-webkit-
  实现动画：①需要把效果添加到哪个css②规定效果的时长 （chrome如果多个属性中只想一个有过渡，需要添加-webkit-，使用默认的会导致所有改变的属性都有过渡效果。）  
8.动画
9.多列：column-count,column-gap,column-rule
10.用户界面：resize（可自由改变大小），box-sizing（border、content）,outline-offset（轮廓），nav-index（tab控制顺序）
```

##css兼容浏览器
###针对内核
针对谷歌内核
```
@media screen and (-webkit-min-device-pixel-ratio:0){/*样式*/}
针对IE6
*HTML .searchBox{/*样式*/}
针对firefox浏览器
@-moz-document url-prefix(){/*样式*/}
```
###调试浏览器的
```
只让ie6看到：*html
会让ie7看到：*+html
只让ff看到：root body
只让ff、ie8看到：html>/**/body
如果只是不让ie6看到：html>body
如果不让ff、ie8看到：*body
```

###针对具体属性
```
只让ie6看到在属性前加_  {_color:#000;}
只让ie7看到使用+和_ {+color:#f00;!;_color:#000;/*ie6还是000*/}
```

##hack
```
\9 例：margin:0px auto\9;   ie6-10识别
*color  /*ie6、7*/
_color /*ie6*/
判断语句
<!--[if IE]>IE浏览器显示的内容 <![endif]-->
<!--[if lt IE 6]>只在IE6-显示的内容 <![endif]-->
“-″减号是IE6专有的hack
“\9″ IE6/IE7/IE8/IE9/IE10都生效
“\0″ IE8/IE9/IE10都生效，是IE8/9/10的hack
“\9\0″ 只对IE9/IE10生效，是IE9/10的hack
```

###浏览器bug
```
1.bug：ie6双边距，当元素浮动并且有margin的时候，ie6下会双边距
  解决办法：添加属性display:inline即可
2.bug：奇数宽高bug。外层宽高为奇数宽高的时候，里面使用绝对定位的时候会有1px间隔（我这没有这情况使用ie5）
  解决办法：将外层设置为偶数宽高
3.bug：ie6不能使用fixed
  解决办法：使用js表达式
4.bug：ie6下高度小于10px不能正确显示高度
  解决办法：ie6下有默认行高，设置font-size:0;overflow:hidden;
5.bug：ie6最小（大）高（宽）度
  解决办法：ie6下有默认行高，①用js表达式②用hack写法.minHeight{height:auto !important;height:100px;min-height:100px;};
6.bug：ie6下div无法遮盖select
  解决办法：ie6下select视为窗口元素，其他元素无论设置z-index 多高也无法覆盖，这时在div添加一个空的iframe  
7.文字溢出bug
8.bug：ff内部div使用margin-top会成为外部的margin-top
  解决办法：display:inline-block; 或者 overflow:hidden;
9.bug:margin塌陷
  解决办法：创建BFC
```

####BFC布局规则
```
内部的Box会在垂直方向，一个接一个地放置。
Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
BFC的区域不会与float box重叠。
BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
计算BFC的高度时，浮动元素也参与计算
```

##响应式
###媒体查询media query
```
判断 分辨率精细的媒体device-pixel-ratio
```

###flexbox布局
```
flex-direction  //方向
flex-wrap       //换行
flex-flow       //方向和换行
justify-content //主轴对齐方式
align-items     //交叉轴对齐方式
align-content   //多跟轴线对齐方式
```

##动画
```css
    keyframes 定义一个动画名字及过程，使用animation调用动画并且传递时间，需要加浏览器前缀
    @keyframes myfirst{
        0%   {background: red;}
        25%  {background: yellow;}
        50%  {background: blue;}
        100% {background: green;}
    } 
    div{
        animation: myfirst 5s/*花费时间*/ linear/*速度曲线*/ 2s/*延时*/          infinite/*无限次播放，也可以设置为特定次数*/ alternate/*动画轮流反向播放*/ 
    }
```

#html
##html5新特性、语义化
```
1.声明改变 doctype
2.语义化标签 header\footer利于SEO，简洁，方便阅读和维护
3.引号标签可以不加不闭合，节省服务器渲染的字节量
4.placeholders
5.contentditable可编辑属性
6.localstorage、sessionstorage、cookie，licalstorage拥挤存储，sessionstorage浏览器关闭就消失，cookie看cookie保存时间
7.audio、video
8.autofocus聚焦到输入框
还有很多
```

#js
##闭包、原型链
```
闭包就是在函数内部的函数，作用是让变量常驻内存，让外部可以访问函数内部的变量和方法。
原型链是每个对象都有一个属性是__proto__指向创建它的函数的 propotype， 实现继承 的一种方式。
```

##promise

##AMD、CMD
```
AMD异步加载，然后使用，CMD使用的时候再异步加载。
```

#webpack
##css插件
```
使用autoprefixer插件运行在postcs上。自动添加前缀
```

#安全
##跨域
```
防止XSS攻击
方法：
1.document.domain+frame设置，解决主域相同二级域名不同的情况。
2.利用iframe和location.hash通过监听hash变化做处理
3.window.name
4.postMessage 也需要iframe，往iframe里postMessage，iframe监听message做处理
5.jsonp，动态添加标签
5.html5的CORS，请求头添加Orgin，包含页面的头部（协议、域名、端口），服务器判断是否允许，可以设置限制域。
```
##安全问题
###客户端脚本安全（前端）
```
1.跨站脚本攻击（XSS）黑客通过html注入篡改网页，插入了恶意脚本，获取用户的信息，控制用户浏览器。最常见的是获取cookie对象，从而发起“cookie劫持”。
解决办法：a.输入检查，过滤掉敏感的关键字；b.将cookie和用户ip绑定；c.为Cookie植入HttpOnly，js就不能操作Cookie了，发送ajax的时候会被放在浏览器头中发送。
2.跨站点请求伪造（CSRF）
  解决办法：输入验证码
```

###服务器端应用安全
```
1.SQL注入
解决办法：①参数拼接的方式查sql②关闭web服务器的错误回显功能③数据库自身使用最小权限原则，不同数据库用不同账户
2.文件上传
解决办法：①通过后缀来判断格式②读取文件前两个字符和格式进行判断③如果为图片则应该有高度宽度属性
```

##安全扫描工具
```
Acunetix Web Vulnerability Scanner 下载地址http://www.91ri.org/4020.html
可以检查各种漏洞
```

#性能
##方法
###减少请求数量
```
1.将小图标合并成sprite图或者iconfont字体
2.用base64减少不必要的网络请求，将小图片使用base64编码载入页面
3.图片延迟加载，先加载首屏
4.js/css按需打包
5.延迟加载ga统计（百度统计）在script里动态引入另一个js，或者加上setTimeout动态引入
```

###减少请求大小
```
1.js/css/html压缩
2.gzip压缩
3.js/css按需加载
4.图片压缩，jgp优化
5.webp优化，srcset优化（响应式图片）
```

###具体
```
1.合并图标可以使用gulp.spritesmith插件，不适合做移动端，iconfont纯色图标
2.base64使用cssnano压缩css时可能会有误伤，直接把data:img改为data:image即可
3.图片延迟加载，固定好高度宽度防抖动，同时要设置个加载中的图片，可以使用 lazysizes.js，然后修改相应样式达到最优化
4.js/css按需打包，使用webpack可以通过commonsChunkPlugin插件抽离出通用代码， 便于缓存。
5.延迟加载，html5中引入了defer和async，带有async的script标签，会在浏览器解析的时候立即下载脚本并且不阻塞后续渲染和加载事件；带有defer的和async一样，并且可以附带一个onload事件，async下载完成后无序进行加载，defer按顺序加载（依赖）。由于兼容性问题，所以通过js手动添加script标签。
6.js压缩，使用webpack的UglifyJsPlugin插件，同事做些代码检测。
7.css压缩，使用cssnano压缩，同时使用postcss做一些自动化处理。
8.html压缩，使用htmlmin压缩，同时纠正不规范的html写法。
9：gzip，服务器端开启，但是不要过度压缩，托管到自己服务器的图片不建议开启gzip压缩。
10.webpack按需加载，使用require.ensure达到按需加载
11.压缩图片，jpg优化：手动处理的话可以去tinypng效果较好，gulp子任务处理的话可以使用gulp-imagemin插件，自动化处理。可以转成jpg的就不用png大小查8倍！
12.webp优化&srcset优化：判断webp支持度，然后替换成webp的图片格式
```

##缓存
###缓存类型
```
1.浏览器缓存
2.代理服务器缓存
3.网关缓存
```

###缓存方法
```
1.应用程序实现的动态页面缓存，直接从服务器加载对应的缓存文件，增加了查找缓存文件时间。
2.使用反向代理服务器的缓存，利用类似nginx的反向代理服务器，用反向代理实现了类似第一种的缓存实现。
3.客户端浏览器缓存，在头部添加，Last-Modified,If-modified-Since,Expires,Cache-Control等标识，和服务器进行协商
①通过Last-Modified,If-Modified-Since方式和服务器通信，客户端发出http请求中包含 If-Modified-Since，如果服务器没有修改，服务器返回304想用代码客户端则直接用本机缓存内容显示结果。
②通过Expires,Cache-Control控制，客户端发现如果上次请求的页面还未到期，通过Expires或者Cache-Control进行辨别，则直接显示本机缓存，不与服务器通信。
```

###总结
```
1.一般高并发的应用程序，都在web蹭上采用了集中缓存，一般静态资源（图片， js，css）都会采用nginx反向代理+客户端缓存来实现。
2.对于门户网站，尤其是首页的新闻，一般都会缓存起来，可以通过反向代理也可以通过应用程序缓存实现方式
3 对于下载或者视频网站，由于数据传输比较大，直接采用浏览器本地缓存实现。
```

#其他
##搭建企业cnpm库
```
使用mysql 、linux
实例地址 [搭建企业内部cnpm](http://blog.csdn.net/wyc_cs/article/details/51568925 "链接")
```


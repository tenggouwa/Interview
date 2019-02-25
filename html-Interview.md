HTML
===
(1)什么是<!DOCTYPE>？
---
    DOCTYPE是html5标准网页声明，且必须声明在HTML文档的第一行。来告知浏览器的解析器用什么文档标准解析这个文档。
    文档解析类型有：
    BackCompat：怪异模式，浏览器使用自己的怪异模式解析渲染页面。（如果没有声明DOCTYPE，默认就是这个模式）
    CSS1Compat：标准模式，浏览器使用W3C的标准解析渲染页面。

(2)meta标签
---
    提供给页面的一些元信息（名称/值对），有助于SEO。
    属性值：
    name：名称/值对中的名称。author、description、keywords、generator、revised、others。 把 content 属性关联到一个名称。
    http-equiv：没有name时，会采用这个属性的值。content-type、expires、refresh、set-cookie。把content属性关联到http头部
    content ： 名称/值对中的值， 可以是任何有效的字符串。 始终要和 name 属性或 http-equiv 属性一起使用
    scheme ： 用于指定要用来翻译属性值的方案

(3)HTML语义化
---
    用正确的标签做正确的事情。
    html语义化让页面的内容结构化，结构更清晰，便于对浏览器，搜索引擎解析；
    即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的；
    搜索引擎的爬虫也依赖于HTML标记确定上下文和各个关键字的权重，利于SEO;
    使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

(4)常见的浏览器内核
---
    Trident内核：IE,MaxThon,TT,The Word,360,搜狗浏览器等。
    Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等；
    Presto内核：Opera7及以上。[现为：Blink]
    Webkit内核：Safari,Chrome等。[Chrome的:Blink(Webkit的分支)]

(5)简单介绍对浏览器内核的理解
---
    主要分成两部分：渲染引擎和JS引擎。
    渲染引擎：将代码转换成页面。负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等）、以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其他需要编辑、显示网络内容的应用程序都需要内核。
    JS引擎：解析和执行javascript来实现网页的动态效果。
    最开始渲染引擎和JS引擎并没有区分得很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。
(6)HTML5有哪些新特性，移除了哪些元素？如何处理HTML5新标签的浏览器兼容问题？
---

    新特性：
    (1) 用于绘画的canvas元素；
    (2) 用于媒介回放的video和audio元素；
    (3) 对本地离线存储有更好的支持，localStorage长期存储数据，浏览器关闭后数据不丢失；sessionStorage的数据在浏览器关闭后自动删除；
    (4) 语意化更好的内容元素，比如header,nav,section,article,footer；
    (5) 新的表单控件：calendar,date,time,email,url,search；
    (6) 新的技术webworker,websockt、Geolocation；
    移除元素：
    (1) 纯表现的元素：basefont,big,center,font,s,strike,tt,u;
    (2) 对可用性产生负面影响的元素：frame,frameset,noframes;
    处理兼容性问题：
    IE8/IE7/IE6支持document.createElement方法产生的标签，可以利用这一特性让这些浏览器支持HTML5新标签，浏览器支持新标签后，还需要添加标签默认的样式。

(7)src和href的区别
---
    src是指向外部资源的位置，指向的内容会嵌入到文档中当前标签所在的位置，在请求src资源时会将其指向的资源下载并应用到文档内，如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，知道将该资源加载、编译、执行完毕，所以一般js脚本会放在底部而不是头部。
    href是指网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。

(8)defer和async的区别
---
    defer要等到整个页面在内存中正常渲染结束（DOM结构完全生成，以及其他脚本执行完成），才会执行。多个defer脚本会按照它们在页面出现的顺序加载。==“渲染完再执行”==
    async一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。多个async脚本是不能保证加载顺序的。==“下载完就执行”==

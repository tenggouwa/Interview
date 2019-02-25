CSS
===

(1)css盒模型
---
    IE盒模型 box-sizing:border-box;（怪异模式）；
    W3C标准盒模型 box-sizing:content-box;（标准模式）。
    应用场景：
    （1）表单：
    表单中有一些input元素其实还是展现的是传统IE盒模型，带有一些默认的样式，而且在不同平台或者浏览器下的表现不一，造成了表单展现的差异。此时我们可以通过box-sizing属性来构建一个风格统一的表单元素。
    （2）设置子类元素的margin或者border时，可能会撑破父层元素的尺寸，这时我就需要使用box-sizing: border-box来将border包含进元素的尺寸中，这样就不会存在撑破父层元素的情况了。

(2)行内元素和块级元素的区别？行内块级元素的兼容性使用？（IE8以下）
---

    块级元素：div,p,h1,form,ul,li
    （1）各占一行，垂直方向排列；
    （2）可以包含其他块级或者行内元素；
    （3）高度、行高以及外边距和内边距都可控制；
    （4）默认宽度是它本身父容器的100%（和父元素的宽度一致），与内容无关。
    行内元素：span,a,label,input,img,strong,em
    （1）水平方向排列，不会自动换行；
    （2）不可以包含块级元素，但是可以包含其他行内元素或者文本；
    （3）行内元素设置width、height无效(可以设置line-height)，margin和padding上下无效；
    （4）宽度就是它的文字和图片的宽度，不可改变。
    行内块级元素在IE8以下的兼容性（块元素模拟inline-block）

(3)页面导入样式时，使用link和@import有什么区别？
---

    （1）link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
    （2）link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。
    （3）link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器（IE5以下）不支持。
    （4）link支持使用Javascript控制DOM去改变样式；而@import不支持。

(4)清除浮动有哪些方式？
---

    （1）在浮动元素下方添加一个非浮动元素
```
<div>
    <div style="float:left;width:45%;"></div>
    <div style="float:right;width:45%;"></div>
    <div style="clear:both;"></div>
</div>
```
    父容器现在必须考虑非浮动子元素的位置，而后者肯定出现在浮动元素下方，所以显示出来，父容器就把所有子元素都包括进去了。这种方法比较简单，但是要在页面中增加冗余标签，违背了语义网的原则。

    （2）将父容器也改成浮动定位

```
<div style="float:left;">
    <div style="float:left;width:45%;"></div>
    <div style="float:right;width:45%;"></div>
</div>
```
    这种方法不用修改HTML代码，但是缺点在于父容器变成浮动以后，会影响到后面元素的定位，而且有时候，父容器是定位死的，无法变成浮动。

    （3）父容器设置overflow: hidden或者auto。（开启BFC）
```
<div style="overflow: hidden;">
    <div style="float:left;width:45%;"></div>
    <div style="float:right;width:45%;"></div>
</div>
```
    缺点：一个是IE6不支持，另一个是一旦子元素的大小超过父容器的大小，就会出显示问题。

    （4）利用:after伪选择符，在父容器的尾部自动创建一个子元素 ==（推荐这种）== 
```
.clearfix:after {
    content: "";
    display: block;
    clear: both;
}
//兼容ie6：激活父元素的"hasLayout"属性，让父元素拥有自己的布局
.clearfix {
    zoom: 1;  //或者height：1%；
}
```

(5)怎么实现水平垂直居中
----

(1）行内元素的水平居中 
```
text-align: center;
line-height: 100px;
```
（2）块级元素水平居中

```
margin: 0 auto;
```
（3）已知高度宽度元素的水平垂直居中

利用绝对定位和负边距实现
```
.container{
    width: 600px;
    height: 600px;
    position: relative;
}
.center{
    width: 300px;
    height: 300px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin: -150px 0 0 -150px;
}
```
利用绝对定位和margin
```
.container{
    width: 600px;
    height: 600px;
    position: relative;
}
.center{
    width: 300px;
    height: 300px;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
```
（4）未知高度和宽度元素的水平垂直居中

被居中的元素是inline或者inline-block元素
```
.container{
    width: 600px;
    height: 600px;
    display: table-cell;
    text-align: center;
    vertical-align: middle;
}
```
css3的transform属性
```
.container{
    width: 100%;
    height: 600px;
    position: relative;
}
.center{
    position:absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
flex布局
```
.container{
    width: 100%;
    height: 600px;
    display: flex;
    justify-content: center;
    align-items: center;
}
```
最简单的写法：
```
.container{
    display: flex;
    height: 600px;
}
.center{
    margin : auto;
}
```

(6)实现左边定宽，右边自适应布局
---
    （1）左盒子左浮动，右盒子width=100%
    （2）左盒子左浮动，右盒子margin-left=左盒子宽度
    （3）左盒子左浮动，右盒子右浮动，设置width: calc（100% - 左盒子宽度）
    （4）父容器设置display：flex，右盒子flex：1

(7)圣杯布局
---
https://segmentfault.com/a/1190000015950592

(8)css3新特性
---
    颜色：新增RGBA、HSLA模式
    文字阴影(text-shadow)
    边框：圆角（border-radius）边框阴影：box-shadow
    盒子模型：box-sizing
    背景：background-size设置背景图片的尺寸，background-origin设置背景图片的原点，background-clip设置背景图片的裁剪区域，以“，”分隔可以设置多背景，用于自适应布局
    渐变：linear-gradient、radial-gradient
    过渡：transition可实现动画
    自定义动画
    在CSS3中唯一引入的伪元素是::selection
    多媒体查询、多栏布局
    border-image
    2D转换：transform:translate(x,y)rotate(x,y)skew(x,y)scale(x,y)
    3D转换

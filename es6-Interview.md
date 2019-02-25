es6 面试题https://www.cnblogs.com/fengxiongZz/p/8191503.html
===


(1) js基本数据类型
---
    undefined null bool number string

(2)判断数据类型方法
---
    typeof  instanceof 

(3)判断对象还是数组
---
    Array有isArray()方法   isPrototypeOf()判断array是否在object原型链中

(4)null和undefined区别
---
    null为定义了，值为空，，，undefined未定义

(5)数组和对象的常用方法
---
    
	数组：arr.push()  arr.unshift()  arr.pop()  arr.shilt()  arr.slice() arr.splice()  arr.concat()  arr.forEach()  arr.map() arr.filter()  arr.every()  arr.some() 
	对象：Object.assign(first, last) 复制   Object.is(a, b) 判断是否相等   Object.keys(a)输出key名的数组string.prototype.hasOwnProperty(’split’) 判断是否有这个属性 

(6)字符串常用的原生方法
---
    charAt()  concat()  indexOf() match() replace() search() slice() split() substr() substring()

(7)数组的深拷贝
---
    const a1 = [1, 2]           1.const a2 = […a1]   2.const […a2] = a1

(8)数组的浅拷贝
---
    1.arr1.concat(arr2, arr3)  2.[…arr1, …arr2, …arr3]

(9)存储方案  
---
    
	cookie 存储量4k，所有请求都携带，不安全
	session 服务端会话存储 
	sessionStorage 会话关闭失效
	LocalStorage 永久有效

(10)es6新增的异步处理
---
    
	先说Generator：

	简单点可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。
	执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函	数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。
	形式上，Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同的内部状态
	而Generator在适用场景上我们可以把它理解为任务的挂起，在js中我们使用没有任务挂起这个概念的，直到Generator的出现，在Generator的使用上我们通过yield定义不同的状态，执行的时候需要使用next进行不同状态的调用，但是他是从上到下的，也就是只要需要yield就会停止执行后面的语句，调用next后继续执行后面的语句，在实际项目开发中，我经常会遇到这样的需求，填写用户信息的时候一般都是分成几步，这时候我们就可以利用Generator的任务挂起特性进行，不同步骤的数据存储。

	然后就是promise
	promise解决了传统异步操作回调函数更加合理强大，有了promise就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。
	有两个接口A,B, 他们之间有依赖关系，B接口必须等到A接口的值返回成功后，拿到A接口里面的一个属性才能请求，如果利用之前的回调函数形势的话就得是层层嵌套，代码维护比较麻烦，如果利用promise的话我们可以用链式调用的形势直观的表示出这种关系

	而Async是Generator函数的语法糖，Async的出现主要是为了解决另外一个问题，刚刚说了Generator是解决任务的挂起，promise是解决异步回调问题，而async就是吧异步的操作，变成队列模式，
	因为async中使用await做状态的定义，调用的时候不需要next（），自动执行，并且会讲每个await中promise中resolve结果赋值给await的变量上以供后面的步骤使用，每一个await都会等到promise返回结果后才会继续自动往下执行，这样就实现了我在日常生活中排队执行的概念，将所有的异步任务以同步的方式定义，不需要担心那个快那个慢，因为她是一个一个自动向下的

(11)webpack-bundle-analyzer可视化的打包体积

(12) 重绘与重排(回流)区别 
---
    重绘：外观改变，比如颜色   回流：尺寸，位置等改变，

(13)原型链
---
    
	每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。关系：instance.constructor.prototype = instance.__proto__

	特点：
	JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话， 就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
  ```function Func(){}
    Func.prototype.name = "Sean";
    Func.prototype.getInfo = function({
        return this.name;
    }
    var person = new Func();//现在可以参考            var person = Object.create(oldObject);
    console.log(person.getInfo());//它拥有了Func的属性和方法
    //"Sean" 
    console.log(Func.prototype);
    // Func { name="Sean", getInfo=function()}
```

(14)async 和 await
---
    
https://www.cnblogs.com/SamWeb/p/8417940.html     https://www.jianshu.com/p/73b070eebf50

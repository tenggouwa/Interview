常用考点
===
(1)写REACT和VUE为什么要写key
---
    key的作用是为了在diff算法执行时，更快的找到对应的节点，提高对比速度。
(2)['1', '2', '3'].map(parseInt)输出什么？
---
    parseInt('1', 0) //radix为0时，且string参数不以“0x”和“0”开头时，按照10为基数处理。这个时候返回1
    parseInt('2', 1) //基数为1（1进制）表示的数中，最大值小于2，所以无法解析，返回NaN
    parseInt('3', 2) //基数为2（2进制）表示的数中，最大值小于3，所以无法解析，返回NaN
    所以最后返回的是[1, NaN, NaN]
(3)什么是防抖和节流？
---
    防抖: 多次触发函数，只会执行一次，并且总是在最后一次时触发。
```
function debounce(fn) {
  let timeout = null; // 创建一个标记用来存放定时器的返回值
  return function () {
    clearTimeout(timeout); // 每当用户输入的时候把前一个  setTimeout clear 掉
    timeout = setTimeout(() => { // 然后又创建一个新的 setTimeout, 这样就能保证输入字符后的 interval 间隔内如果还有字符输入的话，就不会执行 fn 函数
      fn.apply(this, arguments);
    }, 500);
  };
}
function sayHi() {
  console.log('防抖成功');
}

var inp = document.getElementById('inp');
inp.addEventListener('input', debounce(sayHi)); // 防抖
```
    节流: 多次触发函数，在n秒内执行一次，稀释触发频率
```
function throttle(fn) {
  let canRun = true; // 通过闭包保存一个标记
  return function () {
    if (!canRun) return; // 在函数开头判断标记是否为true，不为true则return
    canRun = false; // 立即设置为false
    setTimeout(() => { // 将外部传入的函数的执行放在setTimeout中
      fn.apply(this, arguments);
      // 最后在setTimeout执行完毕后再把标记设置为true(关键)表示可以执行下一次循环了。当定时器没有执行的时候标记永远是false，在开头被return掉
      canRun = true;
    }, 500);
  };
}
function sayHi(e) {
  console.log(e.target.innerWidth, e.target.innerHeight);
}
window.addEventListener('resize', throttle(sayHi));
```
(4.1)Set 是一个构造函数，里面没有重复的内容，可以用来数组去重
---

```
const set = new Set([1, 2, 3, 4, 4]);
[...set] // [1, 2, 3, 4]
```
    也可以用来去除相同字符
```
[...new Set([1,2,2,2,2,2,3,4,4,5,5,6])].join('')
"123456"
```
    他的方法有set.add(); set.delete(); set.has(); set.clear();
    set.keys(); set.values(); set.entries(); set.forEach();
    Array.from方法可以将 Set 结构转为数组。
    这样就提供了数组去重的另一种方式
```
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1, 1, 2, 3]) // [1, 2, 3]
```
(4.2)WeakSet和Set类似，但是它的成员只能是对象
---
    WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。
(4.3)Map
---
    map对应的方法 map.size(); map.set(); map.get(); map.has(); map.delete(); map.clear();
    map.keys(); map.values(); map.entries(); map.forEach();
(4.4)WeakMap
---
    WeakMap与map类似，但是只接受对象作为键名，
    其次，WeakMap的键名所指向的对象，不计入垃圾回收机制。

(5)深度优先遍历，广度优先遍历
---
    深度优先遍历，纵向遍历
    广度优先遍历，横向遍历

(6)ES5和ES6的继承，除了写法之外还有什么区别？
---
    1.class 声明会提升，但不会初始化赋值。Foo 进入暂时性死区，类似于 let、const 声明变量
    2.class 声明内部会启用严格模式。
    3.class 的所有方法（包括静态方法和实例方法）都是不可枚举的。
    4.class 的所有方法（包括静态方法和实例方法）都没有原型对象 prototype，所以也没有[[construct]]，不能使用 new 来调用。
    5.必须使用 new 调用 class。
(8)setTimeOut, Promise, async/await的区别？
---
    https://www.jianshu.com/p/9060fcd27cd7
(9)编写一个程序将数组扁平化去并除其中重复部分数据，最终得到一个升序且不重复的数组
---
    var arr = [ [1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10];
    思路：先扁平化，使用flat方法，去重使用Array.from(new Set())   升序使用sort方法
    Array.from(new Set(arr.flat(Infinity))).sort((a,b)=>{ return a-b})
(10)npm安装原理
---
    发出npm install命令
    查询node_modules目录之中是否已经存在指定模块
    若存在，不再重新安装
    若不存在
    npm 向 registry 查询模块压缩包的网址
    下载压缩包，存放在根目录下的.npm目录里
    解压压缩包到当前项目的node_modules目录
(11)重绘和重排(回流)的定义，以及如何优化？
---
    回流必定会发生重绘，重绘不一定会引发回流。
    优化：
    1.使用 transform 替代 top
    2.使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局
    3.避免使用table布局，可能很小的一个小改动会造成整个 table 的重新布局。
    4.尽可能在DOM树的最末端改变class，回流是不可避免的，但可以减少其影响。尽可能在DOM树的最末端改变class，可以限制了回流的范围，使其影响尽可能少的节点。
    5.避免设置多层内联样式，CSS 选择符从右往左匹配查找，避免节点层级过多。
    6.将动画效果应用到position属性为absolute或fixed的元素上
    7.避免使用CSS表达式
    8.将频繁重绘或者回流的节点设置为图层
    9.CSS3 硬件加速（GPU加速）

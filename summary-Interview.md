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
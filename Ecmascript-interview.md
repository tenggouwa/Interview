Ecmascript特性
===
 **WTF? es10的草案已经出来了，甚至chrome已经支持了部分内容？**

## 一、ES6
 + 类 (class)
 ```
 class Animal {
    // 构造函数，实例化的时候将会被调用，如果不指定，那么会有一个不带参数的默认构造函数.
    constructor(name,color) {
      this.name = name;
      this.color = color;
    }
    // toString 是原型对象上的属性
    toString() {
      console.log('name:' + this.name + ',color:' + this.color);
    }
  }
 var animal = new Animal('dog','white');//实例化Animal
 animal.toString();

 console.log(animal.hasOwnProperty('name')); //true
 console.log(animal.hasOwnProperty('toString')); // false
 console.log(animal.__proto__.hasOwnProperty('toString')); // true
 class Cat extends Animal {
  constructor(action) {
    // 子类必须要在constructor中指定super 函数，否则在新建实例的时候会报错.
    // 如果没有置顶consructor,默认带super函数的constructor将会被添加、
    super('cat','white');
    this.action = action;
  }
  toString() {
    console.log(super.toString());
  }
 }

 var cat = new Cat('catch')
 cat.toString();

 // 实例cat 是 Cat 和 Animal 的实例，和Es5完全一致。
 console.log(cat instanceof Cat); // true
 console.log(cat instanceof Animal); // true
 ```

+ 模块化
  +  模块化主要由import和export组成
  +  export可以导出变量，常量，函数，导出多个可以用{}；
  +  import可以在export之后进行导入；

+ 箭头函数
  + 箭头函数主要学this的指向 https://blog.csdn.net/liwusen/article/details/70257837

+ 函数参数可以添加默认值
  + 默认值
  ```
  function foo(height = 50, color = 'red'){}
  //不使用情况
  function foo(height, color)
  {
      var height = height || 50;
      var color = color || 'red';
  }
  ```

+ 模板字符串
  + ES6中只需要将变量放入${}中既可完成字符串的拼接
  + 
  ```
  //不使用
  var name = 'Your name is ' + first + ' ' + last + '.'
  //使用
  var name = `Your name is ${first} ${last}.`
  ```

+ 解构赋值
  + 解构
  ``` 
      const {liubo} = this.women    // es6
      const liubo = this.women.liubo    // es5
  ```
+ 扩展操作符 ```[...new Set()]```
+ Promise
+ let const

## 二、ES7

+ includes()判断数组是否存在某个值
  ```
  const Tenggouwa = ['Aj12', 'Aj13', 'Aj14'];
  Tengouwa.includes('Aj13'); // true
  Tengouwa.includes('Aj15'); // false
  ```
* 指数运算符 ** 
  ```
  2 ** 4 = 16 
  ```

## 三、ES8

+ async/await **(出门左转，javascript那章)**
+ padStart()和padEnd()，**填充字符串达到当前长度**
+ Object.values() **返回属性值**
   + 例如
      ```
      const obj = {a: 1, b: 2, c: 3};
      //不使用
      const vals=Object.keys(obj).map(key=>obj[key]);
      console.log(vals);//[1, 2, 3]
      //使用
      const values=Object.values(obj1);
      console.log(values);//[1, 2, 3]
      ```
+ Object.entries() **返回一个给定对象自身可枚举属性的键值对的数组。**
  +  例如
      ```
      //不使用
      Object.keys(obj).forEach(key=>{
          console.log('key:'+key+' value:'+obj[key]);
      })
      //key:a value:1
      //key:b value:2
      //key:c value:3

      //使用
      for(let [key,value] of Object.entries(obj1)){
          console.log(`key: ${key} value:${value}`)
      }
      //key:a value:1
      //key:b value:2
      //key:c value:3
      ```
+ Object.getOwnPropertyDescriptors() **来获取自身属性的描述符**
  + 例如
    ```
    const obj2 = {
        name: 'Jine',
        get age() { return '18' }
    };
    Object.getOwnPropertyDescriptors(obj2)
    // {
    //   age: {
    //     configurable: true,  //结构
    //     enumerable: true,   //可列举的
    //     get: function age(){}, //the getter function
    //     set: undefined
    //   },
    //   name: {
    //     configurable: true,
    //     enumerable: true,
    //      value:"Jine",
    //      writable:true
    //   }
    // }
    ```

## 四、ES9

+ 可以在循环中调用异步函数
+ Promise.finally()
    
      可以在then(),在catch()后，指定最终逻辑
+ Rest/Spread 属性
+ 正则表达式相关

## 五、ES10

+ BigInt，新的原始类型， 支持任意精度整数
    ```
    10n === BigInt(10);
    ⇨ true
    10n == 10;
    ⇨ true
    ```
+ string.prototype.matchAll() **返回多个选中内容**
    ```
    let string = "Hello";
    let ret = string.match(/l/g); // (2) [“l”, “l”];
    ```

+ 动态导入 **可以把import的内容赋值给变量**
    ```
    element.addEventListener('click', async() => {
      const module = await import(`./api-scripts/button-click.js`);
      module.clickEvent();
    })
    ```
+ 数组扁平化 Array.flat()
    ```
    let multi = [1,2,3,[4,5,6,[7,8,9,[10,11,12]]]];
    multi.flat();               // [1,2,3,4,5,6,Array(4)]
    multi.flat().flat();        // [1,2,3,4,5,6,7,8,9,Array(3)]
    multi.flat().flat().flat(); // [1,2,3,4,5,6,7,8,9,10,11,12]
    multi.flat(Infinity);       // [1,2,3,4,5,6,7,8,9,10,11,12]
    ```
+ Array.flatMap()
    ```
    let array = [1, 2, 3, 4, 5];
    array.flatMap(v => [v, v * 2]);
    [1, 2, 2, 4, 3, 6, 4, 8, 5, 10]
    ```
+ Object.fromEntries() **将键值对列表转换为对象:**
    ```
    let obj = { apple : 10, orange : 20, banana : 30 };
    let entries = Object.entries(obj);
    entries;
    (3) [Array(2), Array(2), Array(2)]
    0: (2) ["apple", 10]
    1: (2) ["orange", 20]
    2: (2) ["banana", 30]
    let fromEntries = Object.fromEntries(entries);
    { apple: 10, orange: 20, banana: 30 }
    ```
+ String.trimStart() 与 String.trimEnd() **去掉字符串前后空格**
    ```
    let greeting = "  Space around  ";
    greeting.trimEnd();   // "  Space around";
    ```
+ Array.prototype.sort() **排序更稳定**
+ try/catch 中的catch不需要变量
    ```
    try {
        JSON.parse(text);
        return true;
    }
    catch
    {
        return false;
    }
    ```
+ globalThis 标准化 (获取全局对象)
    ```
    var getGlobal = function () {
        if (typeof self !== 'undefined') { return self; }
        if (typeof window !== 'undefined') { return window; }
        if (typeof global !== 'undefined') { return global; }
        throw new Error('unable to locate global object');
    };
    或者 (0, eval)('this')
    ==============》
    // 访问全局数组构造函数
    globalThis.Array(0, 1, 2);
    ⇨ [0, 1, 2]

    // 类似于 ES5 之前的 window.v = { flag: true }
    globalThis.v = { flag: true };

    console.log(globalThis.v);
    ⇨ { flag: true }
    ```
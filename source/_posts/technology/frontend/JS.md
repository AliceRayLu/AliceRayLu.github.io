---
title: 【前端八股】JavaScript
date: 2024-02-27
category: [Technology,Frontend]
toc_number: false
---


# 1 数据类型

## 1.1 let/const/var
用于声明变量

- `var`：函数作用域，存在提升现象，在全局定义时会变成window对象的属性
- `let`：块作用域，作用域更小，不允许冗余（重复）声明
- `const`：const基本与let相同，但是声明时必须初始化且不能修改（如果const指向一个对象，可以修改对象内部属性值）

【var/let迭代变量现象】
```js
for(var i = 0;i < 5;++i){
    setTimeout(() => console.log(i),0) // 输出5,5,5,5,5
}

for(let i = 0;i < 5;++i){
    setTimeout(() => console.log(i),0) // 输出0,1,2,3,4
}
```

## 1.2 基本数据类型

- `Undefined`
- `Null`：表示一个空对象指针
- `Boolean`
- `Number`：8进制-0o______，16进制-0x____，浮点数（IEEE754），科学计数法（e）
- `String`：string类型不可变
- `Symbol`(ES6新增)

以上是6种基本数据类型，以下是引用数据类型。

- `Object`
- `Array`
- `Function`

基本数据类型存储在栈中，直接存储对应值，引用数据类型存储在堆中，在栈中存放关于这个对象的引用。

### 1.2.1 undefined
声明但是没有初始化

请注意**未声明报错**和undefined区别

```js
let mess = undefined // 显式undefined初始化（不必要：默认）
console.log(mess == undefined) //true

if(mess){
    //不执行
}
if(!mess) // 执行

console.log(null == undefined) // true
console.log(null === undefined) // false
```

【null VS undefined】
使用null初始化空值，undefined表明未定义。undefined从null中派生，null是指向空对象的引用。

### 1.2.2 boolean
`true`和`false`区分大小写，只有全小写是bool值，其他形式都是标识符。

【其他类型布尔值等价形式】
| true            |          false|
| :--:            |     :--:      |
| 非空string      | ""(empty string) |
|非零数值         | 0，NaN           |
| 任意对象         | null          |
| N/A(不存在)      | undefined      |


### 1.2.3 NaN
Nan任何操作始终返回NaN
```js
console.log(NaN == NaN) // false
isNaN(NaN) // true
isNaN(10) // false
isNaN("10") //false，可以转化为数值
isNaN("blue") // true 不可以转化为数值
isNaN(true) // false 可以转化为1
```

### 1.2.4 string操作

#### 1.2.4.1 模板字符串
`包括的字符串是模板字符串，允许**换行**，**嵌入变量**
```js
let val = `hi
hither`;
let jas = `${val} use`
```

#### 1.2.4.2 修改
- `+`/`concat()`/`${}`都可以用于拼接字符串
- `slice(start,end)`/`substring(start,end)`：获取[start,end)副本
- `substr(start,len)`：获取从start开始长度为len的字符串副本
- `trim()`/`trimLeft()`/`trimRight()`：删除指定位置空格
- `repeat(n)`：字符串重复n次
- `padStart(len,char)`/`padEnd(len,char)`：当字符串长度不满len时，使用char填充到指定位置
- `toLowerCase()`/`toUpperCase()`：全小写，全大写

#### 1.2.4.3 查询
- `chatAt(pos)`
- `indexOf(string)`
- `startWith(string)`
- `includes(string)`

#### 1.2.4.4 匹配
基于正则表达式
- `match(pattern)`：返回一个匹配的字符串数组
- `search(pattern)`：返回找到的位置下标
- `replace(old,new)`：替换字符串中匹配的位置，返回替换后的结果字符串

#### 1.2.4.5 转化
- `split(char)`：按照char分割字符串，返回字符串数组

### 1.2.5 Object常用方法


## 1.3 类型转换
- Number()
- parseInt() / parseInt(object,base)[指定底数]
- parseFloat()
- toString() / toString(base)[数值转换字符串指定底数]
- valueOf()
- String()

### 1.3.1 显式类型转换

### 1.3.2 隐式类型转换



## 1.4 相等性比较与拷贝

### 1.4.1 == 与 ===
两边类型不同的时候，`==`会先进行类型转换再进行比较，但是`===`会同时检查类型和值

`Object.is(a,b)`行为基本上与`===`一致，除了正负0判断和NaN判断

```js
+0 === -0;           // true
Object.is(+0, -0)    // false

NaN === NaN          // false
Object.is(NaN, NaN)  // true
```

### 1.4.2 深拷贝和浅拷贝

#### 1.4.2.1 浅拷贝
拷贝时只拷贝一层，即基本类型拷贝一份精确复制，对于引用对象类型拷贝一份内存地址，深层的引用共享相同的内存地址。

```js
function shallowCopy(obj){
    var newobj = {};
    for(let prop in obj){
        if(obj.hasOwnProperty(prop)){
            newobj[prop] = obj[prop];
        }
    }
    return newobj;
}
```

【存在浅拷贝现象的方法】
- `Object.assign`：将源对象赋值合并给目标对象，并返回合并后目标对象的值
    ```js
    Object.assign(target, ...sources)
    ```
- `Array.prototype.slice()`, `Array.prototype.concat()`
- 使用拓展运算符实现的复制
    ```js
    let arr = [1,2,3];
    let narr = [...arr];
    narr[1] = 5;
    console.log(narr);
    console.log(arr);
    ```

#### 1.4.2.2 深拷贝
开辟一个栈，把所有属性都严格拷贝一份。因此改变一个对象的属性值不会影响另一个对象的属性值。

【实现方式】

- `_.cloneDeep()`
    ```js
    const _ = require('lodash');
    const obj1 = {
        //属性
    };
    const obj2 = _.cloneDeep(obj1);
    ```
- `jQuery.extend()`
- `Json.stringify()`
- 手写
    ```js
    function deepCopy(obj){
        //只拷贝对象
        if(!obj || typeof obj !== 'object')return;
        let newobj = Array.isArray(obj)?[]:{};
        for(let prop in obj){
            if(obj.hasOwnProperty(prop)){
                newobj = (typeof obj[prop] === 'object')?deepCopy(obj[prop]):obj[prop];
            }
        }
        return newobj;
    }
    ```


## 1.5 判断数据类型

### 1.5.1 typeof
typeof会返回以下字符串：
- `undefined`
- `boolean`
- `number`
- `string`
- `object`
- `function`：函数理论上是一种特殊的对象，但是要区分函数和普通对象，因此有function
- `symbol`

`typeof null`会返回object，认为null是一个对空对象的引用 

typeof是**操作符**而不是函数，不需要参数，可以使用参数。

```js
let message = "ssss";
console.log(typeof message); // string
console.log(typeof(message)) // string
console.log(typeof 95) // number

typeof {} // object
typeof [] // object
```

### 1.5.2 instanceof
instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

一般格式为`object instanceof constructor`

```js
let Car = function() {}
let benz = new Car()
benz instanceof Car // true
let car = new String('xxx')
car instanceof String // true
let str = 'xxx'
str instanceof String // false
```

实现原理：在原型链上依次查找是否由该constructor构建

```js
function instanceof(left,right){
    if(left === null || typeof left !== 'object')return false;
    let proto = Object.getPrototypeOf(left);
    while(true){
        if(proto === null) return false;
        if(proto === right.prototype) return true;
        proto = Object.getPrototypeOf(proto);
    }
}
```

【typeof和instanceof的区别】
- typeof返回字符串，告知对象类型，instanceof返回布尔值
- instanceof用于判断引用对象类型，不能用于判断基础数据类型
- typeof用于判断基础数据类型和function引用对象类型，无法判断具体的复杂引用对象类型

通用方法：`Object.prototype.toString()`

# 2 数据结构
## 2.1 set
- `add(a)`
- `delete(a)`
- `has(a)`
- `clear()`
keys()：返回键名的遍历器
values()：返回键值的遍历器
entries()：返回键值对的遍历器
forEach()：使用回调函数遍历每个成员

### weakset

## 2.2 map
size 属性
set(key,value)
get()
has()
delete()
clear()

### weakmap

## 2.3 json

## 2.4 array

### 2.4.1 数组修改操作
- `push(a,b,...)`：在末尾追加任意多个值
- `unshift(a,b,...)`：在开头插入任意多个值（开头保持unshift参数顺序）
- `concat(a,b,...)`：将数组拼接在一起，返回拼接后的新数组，不影响原来的数组
- `pop()`：删除数组的最后一项
- `shift()`：删除数组的第一项

【splice和slice】
- `slice(start,end)`：对原数组不产生影响，返回[start,end)这一段的数组，如果不指定end，默认到数组结尾
- `splice(start,len,a,b,...)`：对原数组产生影响，从start位置开始，删除掉len个元素，然后在该位置继续插入后续的元素。返回被移除的元素数组。

### 2.4.2 数组查询操作
- `indexOf(a)`：返回某个数的下标，如果不存在返回-1
- `includes(a)`：是否包含某个元素，返回true/false
- `find(func)`：返回满足func的第一个元素
    ```js
    let arr = [1,2,43,24];
    arr.find((el)=>el > 28);
    ```

### 2.4.3 排序
- `reverse()`：对数组进行翻转
- `sort(func)`：按照提供的规则进行函数排序
    ```js
    function cmp(value1,value2){
        if(value1 < value2){
            return -1;
        }else if(value1 > value2){
            return 1;
        }else{
            return 0;
        }
    }
    ```

### 2.4.4 遍历

- `some(func)`：如果有元素满足func条件，返回true
- `every(func)`：如果所有元素满足func条件，返回true
- `forEach(func)`：对每一个元素运行函数，没有返回值
- `filter(func)`：返回满足筛选函数的数组
- `map(func)`：返回每个函数经过func操作后的数组

### 2.4.5 Array.prototype方法重写

#### 2.4.5.1 flat

```js
Array.prototype.flat = function(deep = 1) {
    let res = [];
    deep--;
    for(const val of this){
        if(Array.isArray(val) && deep >= 0){
            res = res.concat(val.flat(deep));
        }else{
            res.push(val);
        }
    }
    return res;
}
```

#### 2.4.5.2 map
```js
Array.prototype.map = function(callback){
    let res = [];
    for(let i = 0;i < this.length;i++){
        res.push(callback(this[i],i,this));
    }
    return res;
}
```

# 3 control flow

## 3.1 loops & iterators

### for in VS for of

for in 遍历对象中所有属性，包括原型属性。如果是数组的话按照index遍历

for of 遍历数组元素值，不能遍历对象

## 3.2 branches

# 4 函数

## 4.1 普通函数和箭头函数
- 箭头函数都是匿名函数，普通函数可以是匿名函数
- 箭头函数不能用于构造器，不能用于new
- 箭头函数没有this，箭头函数中的this都指向函数上下文，使用call，bind，apply也没有办法改变指向
- 箭头函数中不含有arguments形参数组，但是可以使用上下文中的形参数组

## 4.2 参数

### 4.2.1 剩余参数
使用`...`，将传入不定数量的元素集合成一个数组
```js
function func(v1,v2,...arr){

}
```

剩余参数必须是最后一个参数。

### 4.2.2 arguments数组
arguments和函数的参数同步，修改函数参数值就是修改arguments对应元素。

如果不传参，默认为undefined


## 4.3 闭包

一个函数被其引用的状态包围在一起，函数被引用包围

### 4.3.1 优缺点

【优点】保护函数内变量的安全，封装降低耦合

【缺点】容易造成内存泄漏，内存浪费问题

### 4.3.2 适用场景
- 设计一些私有方法和变量
- 延长变量的生命周期

```js
// 柯里化函数

function getArea(width){
    return height => {
        return width * height;
    }
}
let getAreaByTen = getArea(10);
console.log(getAreaByTen(20));
```

```js
// 封装一个计数器counter
var Counter = (function(){
    var privateCount = 0;
    function changeBy(val){
        privateCount += val;
    }
    return {
        increment:function(){
            changeBy(1);
        },
        decrement:function(){
            changeBy(-1);
        },
        value:function(){
            return privateCount;
        }
    }
})

let count1 = Counter();
count1.increment();
count1.increment();
console.log(count1.value()); // 2
```

## 4.4 作用域
块级，函数级，全局作用域级

【作用域链】
从最内部的块级/函数级作用域开始，向外部寻找

# 5 事件

## 5.1 事件与事件流
javascript中的事件，可以理解就是在HTML文档或者浏览器中发生的一种交互操作，使得网页具备互动性， 常见的有加载事件、鼠标事件、自定义事件等

包括事件和事件流。事件流的产生是因为父子结点执行事件存在顺序问题。

【事件流的三个阶段】
1. 事件捕获阶段(capture phase)
2. 处于目标阶段(target phase)/事件处理阶段
3. 事件冒泡阶段(bubbling phase)：从子节点依次上传直到DOM根节点

## 5.2 事件模型

- 原始事件模型（DOM0级）：标签/js直接绑定，绑定速度快，支持冒泡不支持捕获，不能重复绑定（只能绑定一次）
- 标准事件模型（DOM2级）：事件流
    ```js
    var btn = document.getElementById('.btn');
    btn.addEventListener(‘click’, showMessage, false);
    btn.removeEventListener(‘click’, showMessage, false);
    ```
    - 允许绑定多个事件处理器
    - 第三个参数设为true，允许捕获阶段执行，false冒泡阶段执行
- IE事件模型（基本不用）：只有事件处理阶段和冒泡阶段

## 5.3 事件循环
任务分为同步任务和异步任务。

同步任务进入主线程，即主执行栈，异步任务进入任务队列，主线程内的任务执行完毕为空，会去任务队列读取对应的任务，推入主线程执行。

同步异步任务的划分不够精确，可以使用微任务和宏任务

[事件循环详解](https://juejin.cn/post/7020710294083092493)

### 5.3.1 微任务和宏任务

异步任务划分为宏任务和微任务。以下宏任务和微任务的划分是在浏览器中的划分，node.js的划分是不同的。

【宏任务】
- `setTimeout()`
- `setInterval()`

【微任务】
- `promise.then()`
- `async/await`
- `new MutationObserver()`

同步任务执行完毕后，会先查看微任务队列，当微任务队列执行完毕后才会去查看调用宏任务队列。

### 5.3.2 async & await
async就是用来声明一个异步方法，而 await是用来等待异步方法执行


#### 5.3.2.1 async
async函数返回一个promise对象
```js
function f() {
    return Promise.resolve('TEST');
}

// asyncF is equivalent to f!
async function asyncF() {
    return 'TEST';
}
```
#### 5.3.2.2 await
await后面接一个promise对象，返回这个对象的结果

## 5.4 异步&promise
- pending（进行中）
- fulfilled（已成功）
- rejected（已失败）



## 5.4 事件代理
把一个元素响应事件（click、keydown......）的函数委托到另一个元素，在冒泡阶段完成。事件委托，会把一个或者一组元素的事件委托到它的父层或者更外层元素上，真正绑定事件的是外层元素，而不是目标元素

# 6 类

## 6.1 this

### 6.1.1 this对象
this指向函数、类内部对象，运行时自动生成。调用方式决定this对象，谁调用指向谁。

一旦确定，不能被直接更改。

【绑定规则】

- 默认绑定：函数中调用全局变量
- 隐式绑定：作为函数被某个对象调用，绑定到这个对象上
- new绑定：除非函数返回一个对象，否则对函数使用new时将this绑定到赋值对象上
- 显式绑定：使用apply\call\bind改变

new绑定优先级 > 显示绑定优先级 > 隐式绑定优先级 > 默认绑定优先级

### 6.1.2 改变this指向
可以使用`call`, `apply`, `bind`方法

#### 6.1.2.1 call
```js
func.call(obj,1,2);
```

call只生效一次，函数立即执行，传入参数可以不用数组括起来

【手写call】
```js
Function.prototype.myCall = function(context, ...args){
    context = (context === null || context === undefined) ? window : context;
    context.__fn = this;
    let result = context.__fn(...args);
    delete context.__fn;
    return result;
}
```

#### 6.1.2.2 apply

```js
func.apply(obj,[1,2]); // obj是this指向的新对象，传给func的参数必须以数组形式传入
```

apply只生效一次，且是临时生效，函数立即执行，执行完后绑定失效。

如果obj传入null,undefined默认指向浏览器window

【手写apply】
```js
Function.prototype.myApply = function(context,args){
    context = (context === null || context === undefined)? window:context;
    context.__fn = this;
    let result = context.__fn(...args);
    delete context.__fn;
    return result;
}
```

#### 6.1.2.3 bind
```js
let func = oldfunc.bind(obj);
```
bind返回一个绑定永久有效的新函数，参数传递给新函数

```js
Function.prototype.myBind = function(context, ...args1){
    context = (context === null || context === undefined)?window:context;
    let _this = this;
    return function(...args2){
        context.__fn = _this;
        let result = context.__fn(...[...args1,...args2]);
        delete context.__fn;
        return result;
    }
}
```

## 6.2 new

new一个类：
1. 创建一个新对象
2. 将构造函数的作用域赋给新对象（因此this指向了这个新对象）
3. 执行构造函数中的代码（为这个新对象添加属性）
4. 返回新对象

new一个函数：
1. 创建一个新的对象obj
2. 将对象与构建函数通过原型链连接起来
3. 将构建函数中的this绑定到新建的对象obj上
4. 根据构建函数返回类型作判断，如果是原始值则被忽略，如果是返回对象，需要正常处理

【手写new】
```js
function mynew(Func,...args){
    const obj = {};
    obj.__proto__ = Func.prototype;
    let result = Func.apply(obj,args);
    return (typeof result === 'object') ? result : obj;
}
```

## 6.3 原型
原型模式：设计模式，构建一个prototype负责clone新对象

每个对象都拥有一个原型，原型对应的也有自己的原型，一层层向上传递构成原型链

- 一切对象都是继承自Object对象，Object 对象直接继承根源对象null
- 一切的函数对象（包括 Object 对象），都是继承自 Function 对象
- Object 对象直接继承自 Function 对象
- Function对象的__proto__会指向自己的原型对象，最终还是继承自Object对象


## 6.4 继承

- 原型链继承：将子类的prototype设为父类。问题：创建出的子类共享父类属性，修改一个会导致父类修改
- 构造函数继承：使用call将this强行绑定。问题：只能继承父类的实例属性和方法，无法继承prototype方法
- 组合以上两种继承：相当于调用了两次父类，解决以上问题但是导致性能下降
- 原型式继承：使用`Object.create()`，相当于浅拷贝了一份（修改属性会导致原始对象的修改）
- 寄生式继承：封装一个函数，其中仍然使用`Object.create()`创建对象，为这个对象添加一些方法
- 寄生组合式继承

ES6：直接用extends

## 6.5 assign

### 解构赋值

# 7 优化

## 7.1 节流
定义：**n 秒内**只运行一次，若在 n 秒内重复触发，只有一次生效

【手写】

## 7.2 防抖
定义：**n 秒后**在执行该事件，若在 n 秒内被重复触发，则重新计时

【手写】

# 8 ES6 新特性

## 8.1 Generator

## 8.2 Proxy

## 8.3 Module

## 8.4 Decorator

# 9 JS内存机制

## 9.1 引用
每个对象拥有一个关于原型的隐式引用，以及关于属性的显式引用

如果使用引用计数法无法解决循环引用导致的内存泄漏问题

## 9.2 垃圾回收
【标记-清除算法】

从全局根开始，将无法被获取访问到的部分内存清除。

## 9.3 内存泄露
程序未能释放且不能再被使用的内存

- 意外的全局变量：在函数中使用全局变量或者用this创建全局变量（解决方案：使用严格模式）
    ```js
    function foo(arg) {
        bar = "this is a hidden global variable";
    }

    function foo() {
        this.variable = "potential accidental global";
    }
    // foo 调用自己，this 指向了全局对象（window）
    foo()
    ```
- 定时器：获取到的元素在dom中被删除，但是定时器仍然存在，定时器拥有的资源不会被释放
    ```js
    var someResource = getData();
    setInterval(function() {
        var node = document.getElementById('Node');
        if(node) {
            // 处理 node 和 someResource
            node.innerHTML = JSON.stringify(someResource);// someResource不会被释放
        }
    }, 1000);
    ```
- 闭包：闭包内使用的引用导致不会释放
    ```js
    function bindEvent() {
        var obj = document.createElement('XXX');
        var unused = function () {
            console.log(obj, '闭包内引用obj obj不会被释放');
        };
        obj = null; // 解决方法
    }
    ```
- 没有清理对dom元素的引用：dom元素在被删除后还存在对其的引用
    ```js
    const refA = document.getElementById('refA');
    document.body.removeChild(refA); // dom删除了
    console.log(refA, 'refA'); // 但是还存在引用能console出整个div 没有被回收
    refA = null; // 解决办法
    console.log(refA, 'refA'); // 解除引用
    ```

# 10 严格模式

## 10.1 设置严格模式的目的
- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

## 10.2 使用方式

```js
"use strict";
```

# 11 DOM

## 11.1 window
高度：innerheight, outerheight

https://zhuanlan.zhihu.com/p/141845423


# Q & A

1. let/const/var区别
    见1.1节
2. js有哪些数据类型
    见1.2节
3. 数据类型判断
    - 1.2.1节typeof

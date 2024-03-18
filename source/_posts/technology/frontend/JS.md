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

#### 1.2.4.3 查询

#### 1.2.4.4 匹配

#### 1.2.4.5 转化

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



## 1.5 判断数据类型

### 1.5.1 typeof
typeof会返回：
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


# 2 数据结构
## 2.1 set

## 2.2 map

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



# 3 control flow

## 3.1 loops & iterators

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

# 5 异步

# 6 类

## 6.1 this

### call, bind, apply

## 6.2 new

## 6.3 原型

## 6.4 继承

## 6.5 assign

### 解构赋值

# 7 优化

## 7.1 节流

## 7.2 防抖

# 8 ES6 新特性

## 8.1 Generator

## 8.2 Proxy

## 8.3 Module

## 8.4 Decorator


# Q & A

1. let/const/var区别
    见1.1节
2. js有哪些数据类型
    见1.2节
3. 数据类型判断
    - 1.2.1节typeof

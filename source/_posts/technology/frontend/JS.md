---
title: 【前端八股】Javascript
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
共8种基本数据类型

- `Undefined`
- `Null`：表示一个空对象指针
- `Boolean`
- `Number`：8进制-0o______，16进制-0x____，浮点数（IEEE754），科学计数法（e）
- `String`
- `Symbol`(ES6新增)
- `Object`

### 1.2.1 typeof
typedef会返回：
- `undefined`
- `boolean`
- `number`
- `string`
- `object`
- `function`：函数理论上是一种特殊的对象，但是要区分函数和普通对象，因此有function
- `symbol`

`typedef null`会返回object，认为null是一个对空对象的引用 

typedef是**操作符**而不是函数，不需要参数，可以使用参数。

```js
let message = "ssss";
console.log(typeof message); // string
console.log(typeof(message)) // string
console.log(typeof 95) // number

typeof {} // object
typeof [] // object
```

### 1.2.2 undefined
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
```

### 1.2.3 boolean
`true`和`false`区分大小写，只有全小写是bool值，其他形式都是标识符。

【其他类型布尔值等价形式】
| true            |          false|
| :--:            |     :--:      |
| 非空string      | ""(empty string) |
|非零数值         | 0，NaN           |
| 任意对象         | null          |
| N/A(不存在)      | undefined      |


### 1.2.4 NaN
Nan任何操作始终返回NaN
```js
console.log(NaN == NaN) // false
isNaN(NaN) // true
isNaN(10) // false
isNaN("10") //false，可以转化为数值
isNaN("blue") // true 不可以转化为数值
isNaN(true) // false 可以转化为1
```

### 1.2.5 类型转换
- Number()
- parseInt() / parseInt(object,base)[指定底数]
- parseFloat()
- toString() / toString(base)[数值转换字符串指定底数]
- valueOf()
- String()

### 1.2.6 模板字符串
`包括的字符串是模板字符串，允许**换行**，**嵌入变量**
```js
let val = `hi
hither`;
let jas = `${val} use`
```

# 2 DOM


# Q & A

1. let/const/var区别
    见1.1节
2. js有哪些数据类型
    见1.2节
3. 数据类型判断
    - 1.2.1节typeof

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
- `Null`
- `Boolean`
- `Number`
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

`typedef null`会返回object，认为null是一个空对象 

# 2 DOM




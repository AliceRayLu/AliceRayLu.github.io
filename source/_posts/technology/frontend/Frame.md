---
title: 【前端八股】Frameworks
date: 2024-03-05
category: [Technology,Frontend]
toc_number: false
---

面试时经常喜欢提问对比性问题，比如列表元素，在vue中不加key的反应和react中不加key的反应，涉及到框架底层的渲染机制

# Vue

## 渲染流程
1. 解析模板
2. 生成渲染函数
3. 执行渲染函数
4. 对比新旧虚拟dom树：根据diff算法决定需要更新的内容
5. 更新dom

## 生命周期hooks

### 常规hooks

### 父子组件渲染顺序

### keep-alive
在**组件切换**过程中，将组件的状态保存在内存中，防止重复渲染dom。

组件就没有beforeDestroyed和destroyed的生命周期钩子函数，会被替换成activated,beforeactivate

## 双向绑定

MVVM原理

数据劫持（object.defineProperty）+ 发布-订阅模式

### 手写发布-订阅模式

### 数据劫持

使用object.defineProperty的缺点：通过下标方式修改数组数据或者给对象新增属性，这都不能触发组件的重新渲染。

vue2解决方案：重写函数；vue3解决方案：使用proxy监听

### MVVM，MVC，MVP

**MVVM**：model，view，viewmodel，双向绑定，通过viewmodel进行model和view的更新

**MVC**：model，view， controller。view的交互触发controller调用，修改model，触发view更新【观察者模式】

**MVP**：model，view，presenter。解耦view和model，在 Presenter 中将 Model 的变化和 View 的变化绑定在一起，以此来实现 View 和 Model 的同步更新

### watch
支持异步和开销比较大

### computed
缓存，不支持异步；更多的是观察作用触发回调函数

### methods
每次数据更新都会触发method执行

## 语法糖

### 指令系统

#### v-if、v-show
v-if通过操作dom树，v-show改变css的display属性值

#### v-if、v-for优先级

### slot
获取传进`<></>`之间的值

## axios


## 单屏

## 组件通信方式

## 虚拟dom

### diff算法

### key


### vue3优化
增加一些静态标记，对静态节点不进行重复的渲染

## Vue3和Vue2

Vue3的优化：
- 更小：移除一些不常用api
- 更快：编译速度更快
- 支持ts
- 使用proxy替代defineProperty进行数据劫持
- tree shaking: 只有需要的包才会被打包使用



## Vuex

# React

## hooks

### state和props

### useState useEffect useCallback useMemo

## 函数式组件和类式组件

## 虚拟dom

## 组件通信

## diff算法

## 生命周期


# Vue VS React

React特点总结：
- JSX：使用javascript写html
- functional programming
- lifecycle hooks
- react native for mobile devices

Vue特性：
- html、js、css集成在一个文件中
- syntatic sugar: v-if v-for
- slot

【相同点】
- 都有组件化思想
- 都支持服务器端渲染
- 都有Virtual DOM（虚拟dom）
- 数据驱动视图
- 都有支持native的方案：Vue的weex、React的React native
- 都有自己的构建工具：Vue的vue-cli、React的Create React App
【区别】
- 数据流向的不同。react从诞生开始就推崇单向数据流，而Vue是双向数据流
- 数据变化的实现原理不同。react使用的是不可变数据，而Vue使用的是可变的数据
- 组件化通信的不同。react中我们通过使用回调函数来进行通信的，而Vue中子组件向父组件传递消息有两种方式：事件和回调函数
- diff算法不同。react主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。Vue 使用双向指针，边对比，边更新DOM

# 前端性能优化

## 优化思路
浏览器 -> 资源加载（图片） -> 代码

## 评价指标

- 白屏时间
- 页面渲染时间
- 最大内容加载时间

## 优化白屏

- DNS服务优化
- CDN内容分发网络
- 服务端优化（缓存与分包）

## 优化渲染

- JS：使用防抖优化用户输入
- CSS样式：减少复杂的样式计算和嵌套；避免大的、复杂的布局和布局回流；异步加载非必须css

## 最大内容加载



---
title: 【前端八股】CSS
date: 2024-03-09
category: [Technology,Frontend]
toc_number: false
---

# 1 CSS选择器

id选择器（#box），选择id为box的元素

类选择器（.one），选择类名为one的所有元素

标签选择器（div），选择标签为div的所有元素

后代选择器（#box div），选择id为box元素内部所有的div元素

子选择器（.one>one_1），选择父元素为.one的所有.one_1的元素

相邻同胞选择器（.one+.two），选择紧接在.one之后的所有.two元素

群组选择器（div,p），选择div、p的所有元素

## 1.1 选择器优先级

## 1.2 复合选择器

# 2 预处理器
less sass

# 3 CSS3新特性

# 4 居中对齐

## 4.1 水平居中

## 4.2 垂直居中

# 5 像素大小

## 5.1 px

## 5.2 em/rem

## 5.3 vw/vh

# 6 position

- `relative`：相对于默认位置的偏移
- `absolute`：相对于父级元素的偏移
- `fixed`：相对于浏览器窗口是固定的位置

absolute和fixed会脱离文档流

# 7 布局

## 7.1 两栏布局

- 设置左侧固定宽度，float:left，右栏使用margin-left撑出空间
- 使用flex布局：父元素使用display：flex，左边栏固定宽度，右边栏flex：1

## 7.2 三栏布局
- 两边使用 float，中间使用 margin
- 两边使用 absolute，中间使用 margin
- display: table 实现
- flex实现
- grid网格布局

## 7.3 grid布局

## 7.4 flex

flex-direction

## 7.5 BFC

## 7.6 文字溢出

# 8 回流与重绘

回流：布局引擎会根据各种样式计算每个盒子在页面上的大小与位置

重绘：当计算好盒模型的位置、大小及其他属性后，浏览器根据每个盒子特性进行绘制

# 9 动画

## transition

## transform

## translate

## animation

# 10 性能优化
---
title: c++高级程序设计(22Fall)
date: 2024-02-26
category: [Knowledge,C++]
---

原始的课堂笔记丢了，本文档补充记录一些复习重点。

# c++98/11/14特性

- 98：最初版本的c++，包括STL等
- 11：重大更新，包括auto/for/lambda/智能指针/nullptr/template等
- 14：型 Lambda 表达式、返回类型推导、二进制字面量、数字分隔符、弃用属性
- 17：结构化绑定、if constexpr、std::optional、std::variant、std::string_view、并行算法

# inline & define & template
## inline
实际调用的时候，把inline函数放回原来的位置，不会产生参数的传递，在汇编上也不会有其他的冗余操作，编译系统将为inline函数创建一段代码，在调用点，以相应的代码替换

【作用】
- 增加程序**可读性**
- 提高程序**运行效率**
- 补充宏定义不能进行**类型检查**的缺陷

【问题】
- 增大目标代码
- 病态换页（内存抖动）
- 降低指令快取装置的命中率

【建议】
- 使用**频率高的小代码**内联
- 内联函数定义放在头文件中
- 不含有复杂的结构控制
- 不允许递归做内联函数

## 宏
宏包括`#define`，`#ifndef ... #endif`（避免重复定义头文件）, `#ifdef .. #else .. #endif`(条件宏)，`#undef`取消宏

```cpp
#define MAXT 999
#define add(x,y) x+y
```

## inline和define
- #define没有类型，相当于是泛型，可能导致出现漏洞
- inline类型写死

## template
```cpp
template<typename T>
void swap(T& a,T& b){
    ...
}
```

模板的实例化：显式实例化、隐式实例化、特化

【define与template】
define仅仅是字符串替换，不含类型检查

# const

参考这篇博客的[总结](https://blog.csdn.net/eric_jo/article/details/4138548)

## 常量
`const int t = 1`或者`int const t = 1`是一样的，都表示一个常量，必须声明时赋值

`extended const int t = 1`使用extended可以不进行初始化，变量作用于扩大至全局,编译时会分配内存

## 指针常量和常量指针
`const char* p`：指针指向的内容不可变

`char* const p`：指针本身是常量不可变

`const char* const p`：指针本身不可变且指向的内容不可变

## 函数中使用
```cpp
// as parameter

// as return value
```

## 类中使用

```cpp
// member function with const: can't change any attribute variable

// const class: can't use any not const function
```

## const转为非const类型

# 指针


## 指针和引用
the difference between pointer and reference

- pointer is an address, reference is an alias which is the same as the original variable(sizeof)
- pointers can point to pointers, but reference can't
- pointers can be initialized later, but reference must be initialized while declaring.
- pointers can point to NULL, reference can't
- pointers can be changed, but reference can't

# 左值和右值

# 面向对象

## 普通继承与虚继承

## 析构函数

## 操作符重载

# c++多态

# 虚函数
## 静态/动态绑定

动态绑定：编译器在编译阶段不知道对象的实际类型，在运行时才能确定

## 纯虚函数
```cpp
virtual int f() = 0;
```

## 抽象类
a class that can't be instantiated. Must include at least **one pure virtual function**.
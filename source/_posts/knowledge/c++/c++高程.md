---
title: c++复习总结
date: 2024-02-26
category: [Knowledge,C++]
---

原始的课堂笔记丢了，本文档补充记录一些复习重点。

# c++98/11/14特性

- 98：最初版本的c++，包括STL等
- 11：重大更新，包括auto/for/lambda/智能指针/nullptr/template等
- 14：型 Lambda 表达式、返回类型推导、二进制字面量、数字分隔符、弃用属性
- 17：结构化绑定、if constexpr、std::optional、std::variant、std::string_view、并行算法

# difference between c/c++
- c++ has OOP & template
- c++ use `new` & `delete` instead of `malloc` and `free`
- c++ has smart pointers which are safer
- c++ allows function overload

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

在编译阶段进行简单的文本替换

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
int func(const int& t)

// as return value
const int func(int t)
const int* func(int t)
```

## 类中使用

```cpp
// const attribute: can't change
class A{
    const int t;
    A(int x):t(x){
        // can only be initialized this way
    }

    void func()const;// member function with const: can't change any attribute variable & can't use non-const function & can access const attribute
}


// const class: can't use any not const function
const A aaa;
aaa.func(); //correct
```

## const转为非const类型
```cpp
const_cast<int*>(p);// 通常用于指针
```
# 指针


## 指针和引用
the difference between pointer and reference

- pointer is an address, reference is an alias which is the same as the original variable(sizeof)
- pointers can point to pointers, but reference can't
- pointers can be initialized later, but reference must be initialized while declaring.
- pointers can point to NULL, reference can't
- pointers can be changed, but reference can't

## 智能指针

RAII：Resource Acquisition Is Initialization

# 左值和右值

# 面向对象

## 普通继承与虚继承

## 构造函数

### 拷贝构造函数

### explicit
forbid implicit type conversion

## 析构函数

## 操作符重载



## 覆盖与重载

【覆盖】

子类中重写覆盖父类中的方法，必须严格继承父类方法的名字、参数类型、返回值。

【重载】

仅仅函数名相同，参数类型不同。重载的函数必须在同样的范围中。

# c++多态

分为**静态多态**和**动态多态**

【静态多态】主要表现为**函数重载**，编译时即确定函数类型

【动态多态】主要表现为**虚函数**，在程序运行时才确定参数类型（相关概念：纯虚函数、抽象类）


# 虚函数
## 静态/动态绑定

动态绑定：编译器在编译阶段不知道对象的实际类型，在运行时才能确定

## 纯虚函数
```cpp
virtual int f() = 0;
```

## 抽象类
a class that can't be instantiated. Must include at least **one pure virtual function**.

# stack & heap
【栈】

由编译器自动分配管理释放，用来存储函数参数和局部变量，从高地址向低地址增长。栈的大小是有限的。

【堆】

由程序员管理分配和释放，用来存放程序中的动态内存，程序结束由操作系统自动回收，从低地址向高地址生长。堆的大小相对较大，内存分配方式比较灵活。但是容易产生内存碎片。

# struct

## struct & class

## struct内存

## struct & union

# how to optimize performance

- compile options: `-O2` `-O3`
- avoid useless memory operation like `new` `delete`
- choose better data structure and algorithm
- use multi-thread
- use inline function and const expression
- use smart pointer


# static

- hide global variable or global function：make it only visible in the source file
- keep variable longer
- In Class: 
    - static variable: shared among all the instances
    - static member function: can be accessed without instanciate a class(can only visit static variables)
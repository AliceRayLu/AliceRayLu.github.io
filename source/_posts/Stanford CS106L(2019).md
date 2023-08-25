---
title: Stanford CS106L(2019)
date: 2022-10-24
category: Stanford Lecture Notes
---


建议先学完cs106B/或者相对应的c++基础再来上手这门课程，光有c的基础看起来有点吃力

[CS 106L Fall 2019 - Lecture 0 - Introduction (Screencast)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1yJ411m7CE?p=1&vd_source=63731e51187044a6065a97ae72adb12e)

这是当时能找到的最新版本，其他版本暂时没有公开视频，2019年的作业也没有过期，可以也拿出来做一做，2022的作业还要配环境烦死了

[CS 106L: Standard C++ Programming (stanford.edu)](http://web.stanford.edu/class/cs106l/)

课程网站（2022spring）

## std::pair

```cpp
std::pair<int, string> numSuffix = {1,"st"};
cout << numSuffix.first << numSuffix.second;
//prints 1st
```

## auto

ask the compiler to deduce the type

```cpp
auto a = 3;
auto b = 4.3;
auto c = ‘X’;
auto d = “Hello”;
auto e = std::make_pair(3, “Hello”)
// int, double, char, char* (a C string), std::pair<int, char*>
```

## Lecture 1-2

### stringstream

```cpp
ostringstream oss("hello",stringstream::ate);
//establish an output stream, the pointer ends at the end.
ostringstream oss1("hello");//the pointer points at the start
std::cout << oss.str() << endl;
oss << 16 << " hi" ;//start input string or others at the pointer

fpos p = oss.tellp() + streamoff(3);
//the number can be negative: streamoff(-3) move in another direction
//take the current pointer 3 spaces off 
oss.seekp(p);

istringstream iss(oss.str());
int i;
string s;
iss >> i >> s;//in iss divide by space
iss.tellg();//tell the position
iss.seekg(2);//set the position
```

**usage: use stringstream to seperate a line(or to say split)**

### getline

```cpp
string name;
getline(cin,name,'\n')

cin.ignore();
```

### std::ws

![](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/assets/image-20221024215329-otyq0b8.png?raw=true)

忽略下一个换行

## Lecture 3

### STL(Standard Template Library)

### std::vector<type>

![](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/assets/image-20220906214443-tv83pni.png?raw=true)

`v[i]` notation will not check the boundary!!!

`v.at()` will check and call the error

### std::deque<type>

a double ended queue(see cs61b-lab1 for review)

### careful initialization

```cpp
std::vector<int> vec1(3,5); 
// makes {5, 5, 5}, not {3, 5}!
std::vector<int> vec2{3,5};
// makes {3, 5}
```

## Lecture 4-5

### iterator

```cpp
std::set<int> container;
std::set<int>::iterator iter = container.begin();
while(iter != container.end()){
    *iter += 1;//must visit elements with * 
    ++iter;
}
```

**note**: why use prefix `++`: `++iter` returns the value after being incremented! `iter++` returns the previous value and then increments it. (wastes just a bit of time)

### functions using iterator

```cpp
vector<int> v = {3,4,1,5};

std::sort(v.begin(),v.end());
//then v will be {1,3,4,5}

auto iter = std::find(v.begin(),v.end(),5);
//auto should be type iterator, find will return a pointer pointing at the //position of 5
if(iter == v.end()) cout << "not found" << endl;

auto p1 = v.lower_bound(4);
//return an iterator pointing at 5(the smallest element that is bigger than 4
auto p2 = v.upper_bound(4);
//return an iterator pointing at 4(the smallest element that is 
//equal or bigger
```

### iterator types

**common**:

* can be created by existing iterators(copyable) ==[warning: not all types are copyable!!! streams can't be copied like cout...]== pass by reference
* can be advanced using `++`
* can be compared using `==` and `!=`

**different types**:

1. **input**: single-pass, read only(can only be dereferenced on right side of expression) e.g.`find` and `count`, `inputstream`
2. **output**: single-pass, write only(dereferenced only on the left side of enpression) e.g. `copy`, `output streams`
3. **forward**: multi-pass, can do both read and write(if not `const` iterator) e.g.`replace`,`forward_list`
4. **bidirectional**: same as forward, and this one can use `--` to move backwards e.g.`reverse`, `std::set`,`std::map`,`std::list`
5. **random access**: same as bidirectional, but also can be incremented or decremented by arbitary amount of steps like `iter = iter +3` e.g.`std::vector`,`std::deque`,`std::string`

## Assignment 1（2022）

### setup

依据assignment 0 配置过后运行`./setup.sh`会有很多报错，要先给Ubuntu安装cmake，然后git clone下载cpr库，按照网上教程安装，再次运行setup命令

还是报错，配环境真的老大难。然后有个`undefined reference to cpr::Session::session()`,github上有一个老哥直接硬链接加文件，这样总算可以运行了，走一步看一步吧。。。结果报了bad_alloc错，找半天也不知道怎么解决

### std::ifstream

## Lecture 6

### Templates

```cpp
template <typename T,typename U...>//can be multi-type
std::pair<T,T> myFunc(T a,T b){
    ...
}

auto [min,max] = myFunc<int>(3,5);//explicit instantiation
auto [min1,max1] = myFunc(3.2,24.4);//this is also valid
```

if pass in different types: 

* use different typename

* use explicit instantiation(which will convert it automatically)

* convert it manually in parameters

### Templates with iterators

```cpp
template <typename Collection,typename T>
int countVal(const Collection<T>& list,T val){
    int count = 0;
    for(auto iter = list.begin();iter != list.end();++iter){
        if(*iter == val)count++;
    }
    return count;
} 
```

if we want special range in collection

```cpp
template<typename InputIterator, typename T>
int countVal(InputIterator begin,InputIterator end,T val){
    int count = 0;
    for(auto iter = begin;iter != end;++iter){
        if(*iter == val)++count;
    }
    return count;
}
```

## Assignment 1 (2019)

## Lecture 7

### explicit interface: named requirements on template types

```cpp
template<typename It,typename Type>
    requires Input_Iterator<It> && Iterator_of<It> && 
        Equality_comparable<Value_type<It>,Type>
int count_occurences(It begin,It end,Type val){
    int count = 0;
    for(auto it = begin;it != end;++it){
        if(*it == val)count++;
    }
    return count;
}
```

### predicate

defination: takes in some parameters and returns a boolean value

```cpp
template<typename It,typename UniaryPredicate>
int count_occurences(It begin,It end,UniaryPredicate predicate){
    int count = 0;
    for(auto it = begin;it != end;++it){
        if(predicate(*it))count++;
    }
    return count;
}
```

### lambda functions

```cpp
int limit = 3;
vector<int> grades;
auto func = [limit](auto val){return val >= limit;}
count_occurences(grades.begin(),grades.end(),func);
//the function mentioned above
```

two different ways to pass reference or pass value

```cpp
auto func = [=,&teas](parameters){
    //body
}//pass every parameter by value except that teas is passed by reference

auto func = [&,banned](parameters){
    //body
}//pass every parameter by reference except banned
```

## Lecture 8-9

### std::minmax_element

header: `#include<algorithm>`

`minmax_element(ForwardIt begin,ForwardIt end,Compare cmp)`

take in two parameters(forward iterator) and a compare function(tells about comparison between undefined type parameters) , then return a pair of `{min,max}`

example code 1: (default comparison)

```cpp
list<int> numbers;
auto [min,max] = minmax_element(numbers.begin(),numbers.out());
cout << "the min number is" << *min << endl;
```

example code 2: (undefined type)

```cpp
struct student{
    string name;
    int age;
    double average;
}Student;

vector<Student> students;
auto compare_student = [](Student& s1,Student& s2){
    return s1.average < s2.average;
}
auto [minStudent,maxStudent] = minmax_element(students.begin(),
    students.end(), compare_student);
```

### std::accumulate

header:`#include<numeric>`

usage: `accumulate(InputIt begin,InputIt end, T init)`

add everything between the iterator, return the value + init value(type T)

### std::nth_element

put every element smaller of the chosen one 

### std::any_of

`any_of(It begin,It end,Predicate predicate)`

find if the collection has one element which satisfy the predicate sentence(return a boolean)

### stream adaptor

`ostream_iterator<T>(cout,'\n')`

creates an iterator of stream (adapter can automatically expand space)

## Lecture 10

### std::search

`search(s.begin(),s.end(),elem.begin(),elem.end())`

Find elem in s. return an iterator which tells the postion of first found, if not found return `s.end()`

### dotproduct

计算两个向量的点乘(cos),使用vector做容器

【numeric库中还有accumulate】

```cpp
#include<numeric>
#include<vector>

int dotProduct(const vector<int>& vec1,const vector<int>& vec2){
    return std::inner_product(vec1.begin(),vec1.end(),vec2.begin()，0);
}
```

inner_product 最后一个参数是点乘的原始值，一般设为0；不需要传入vec2.end()因为已经保证vec2向量维数（大小）和vec1是一样的。

【取向量的模(magnitude)的巧法】

```cpp
#include<cmath>//the header of sqrt

int mag(const vector<int>& vec){
    return std::sqrt(dotProduct(vec,vec));
}
```

### const

* const pointer

  ```cpp
  int * const p;//a const pointer pointing to a non-const integer
  //it's ok to use (*p)++
  //it's not allowed to use p++

  const int *p;//a non-const pointer pointing to a const integer
  int const *p;//the same as above 

  const int * const p;
  int const * const p;
  ```
* const iterator

  to make an iterator read only(can't change the value the iterator points to), define a new `const_iterator`

  ```cpp
  const vector<int>::iterator iter = v.begin();
  //the same as const pointer
  ++iter;//not allowed
  *iter = 15;//allowed

  vector<int>::const_iterator iter = v.begin();
  *iter = 5;//not allowed
  ++iter;//allowed
  int i = *iter;//allowed
  ```
* const functions: function that can't modify the parameters passed into it, can not call any non-const functions

  ```cpp
  int maxVal(const int a,const int b) const;
  ```
* const object: treat all public members as const, only allow to call

## Lecture 11

### operator defination

![](https://github.com/AliceRayLu/AliceRayLu.github.io/blob/main/source/_posts/assets/image-20221012172946-uq1d9bc.png?raw=true)

```cpp
vector<string> v{"hello","world"};
cout.operator<<(v.operator[](0));//cout << v[0];
v.operator[](1).operator+=("!");

operator<<(cout,operator[](v,0));
operator+=(operator[](v,1),"!");
```

### operator function

```cpp
vector<string>& vector<string>::operator+=(const int& element){
    push_back(element);
    return *this;//this: a pointer to the class self
}

vector<string>& vector<string>::operator+=(const vector<int>& other){
    for(int val:other){
        push_back(element);
    }
    return *this;
}

vector<string> vector<string>::operator+(const vector<string>& other) const{
    vector<string> res = *this;
    for(const std::string& s:other){
        res.push_back(s);
    }
    return result;//make a copy and does not change the original one
}
```

operator as a member function

```cpp
vector<string> operator+(const vector<string>& first,const vector<string>& second){
    vector<string> result = first;
    for(const std::string& s:second){
        result.push_back(s);
    }
    return result;
}
```

operator as non-member function

* `[],(),->,=`必须是成员函数
* `<<,>>`必须是非成员函数

  ```cpp
  class Fraction{
  public:

  private:
      int num;
      int denum;
      friend operator<<(std::ostream& os,const Fraction& f);
  }

  ostream& operator<<(std::ostream& os,const Fraction& f){
      os << f.num << " " << f.denum;
  }
  ```

  使用ostream返回值使得cout等可以叠加使用操作符(cout << a<<b;)

  【在类中使用友元（friend）允许该友元访问类中的私有变量，友元可以是类或者函数】
* unary operators(一元操作符：只有一个变量）like`++,--`必须是成员函数
* 如果操作符是binary operator或者表达式的左值右值都不改变，以非成员函数形式声明，可以是友元
* 如果是binary operator但是左值改变以成员函数形式声明（对私有变量访问方便）

## Lecture 12

### 初始化表

see c++ in nju

### copy constructor

create a new object from existing value(l-value)

```cpp
StringVector::StringVector(const StringVector& other)noexcept:
    logicalSize(other.logicalSize),allocatedSize(other.allocatedSize){
        elems = new std::string[allocatedSize];
        std::copy(other.begin(),other.end(),begin());
}
```

### copy assignment

与copy constructor不同，本质上是=的重载

overwrite existing object with existing value(l-value)

```cpp
StringVector& StringVector::operator=(const StringVector& other){
    if(this != &other){
        delete[] elems;
        allocatedSize = other.allocatedSize;
        logicalSize = other.logicalSize;
        elems = new std::string[allocatedSize];
        std::copy(other.begin(),other.end(),begin());
    }
    return *this;
}
```

use `StringVector&`as return type: v1 = (v2 = v3) 重叠式赋值

【如果显式定义了copy constructor,copy assignment,destructor其中一个，必须同时定义其他两个】

## Lecture 13

### emplace_back

在vector里面的成员函数，往vector里面push一个元素（no copy）：在emplace_back的参数中直接构造一个

### lvalue & rvalue

lvalue: an expression that has a name(can find address using `&` address of operator)

rvalue: doesn't have a name, temporary values(can't find address)

左值可以出现在左右两边，但是右值只能出现在右边（=）

```cpp
auto&& v4 = v1+v2;//v4 is an r-value reference

const auto& ptr3 = ptr+5;//can bind a const l-value reference to rvalue
```

左值可以被copy，但是不可以move;右值都可以

### move

move constructor: create new object from existing **r-value**

```cpp
StrVector::StrVector(StrVector&& other):elems(std::move(other.elems)){//why using move see below
    std::cout << "hello from move constructor" << endl;
    other.elems = nullptr;
}
```

move assignment

```cpp
StrVector& operator=(StrVector&& rhs){//rhs itself is a lvalue,but bind to a r-value
    if(this == &rhs){
        delete[] elems;
        allocatedSize = rhs.allocatedSize;//this is a copy
        elems = rhs.elems;
        rhs.elems = nullptr;
    }
    return *this;
}
```

change: `allocatedSize = std::move(rhs.allocatedSize);` move unconditionally cast the parameter into an r-value

## Lecture 14

### scope resolution

范围解析，example: `std::`

### namespace

解决命名冲突问题

```cpp
namespace Lecture{
int count(iterator begin,iterator end, T elem){
    //...
}
}

int main(){
    cout << Lecture::count(...) << endl;
}
```

可以在namespace中命名类

### interface

```java
interface Drink{
    public void make();
}

class Tea implements Drink{
    public void make(){
        //...
    }
}
```

类似于java中的interface，c++中的实现：

```cpp
class Drink{
    public:
        virtual void make() = 0;//pure virtual function
        virtual void make();//non-pure virtual
};

class Tea: public Drink{
    public:
    void make(){
        //...
    }
};
```

`make() = 0`：任何implements Drink的类必须实现make函数，否则不能编译通过(pure virtual)

c++中没有`interface`关键字，如果想要使一个类成为interface只要使该类中成员函数都是pure virtual即可（interface不能有实例对象）

### abstract class

若某一个class至少包含一个pure virtual函数则这个类被成为抽象类（interface是抽象类的子集）

**抽象类不能被实例化（instantiated）**

### inheritance

继承类如果和被继承的类有重名变量or函数，在继承类中会被隐藏（hide）

发生隐藏时，如果是调用父类则使用父类变量/函数，调子类则使用子类

## Lecture 15

### constructor

继承父类的子类必须要调用父类的constructor

### destructor

如果这个class是可以被继承的，该类的destructor必须是virtual,否则会发生内存泄漏

### protected

类似于private，但是private中的成员只能在这个class里被访问，protected成员可以在该类和继承这个类的子类里面被访问

### inheritance实例

```cpp
#include<iostream>

using std::cout; using std::endl;

class Drink{
public:
    Drink() = default;
    Drink(std::string flavor): _flavor(flavor){}

    virtual void make() = 0;
    /** virtual void make(){
        cout << "make drink from drink class" << endl;
    }*/
    virtual ~Drink() = default;
private:
    std::string _flavor;
};

class Tea: public Drink{
public:
    Tea() = default;
    Tea(std::string flavor):Drink(flavor){}
    virtual ~Tea() = default;

    void make(){
        cout << "make tea from tea class" << endl;
    }
};

int main(){
    Tea t("red");
    t.make();//print from tea's make
    t.Drink::make();//print from drink's make
}
```

### templates

templates are implicit interfaces

【static/dynamic polymorphism: templates是静多态，inheritance是动态多态。静态和动态的区别在于静态的在编译之前就直到要调用哪一个，而动态的只有编译完之后才知道调用的对象】

class can be templates

```cpp
template<class T,class Container = std::vector<T>>//by default,the container is a vector which includes the class T
class Priority_Q{

};
```

## Lecture 16

### smart pointers

* `std::unique_ptr`：uniquely owns its source and delete it when the object is deleted( can't be copied)

  ```cpp
  Node* n = new Node;
  //equals to
  std::unique_ptr<Node> n(new Node);
  ```
* `std::shared_ptr`：resources can be stored in any number of pointers,delete when none of them point to an object

  实现方法使用一个count变量
* `std::weak_ptr`：weak_ptr的对象count不计入weak_ptr

## Table of Content
   1. [ Headers ](#Headers)
   1. [ Function ](#Function)
   1. [  Lambda Expression ](#LambdaExpression)
   1. [ Function Object](#FunctionObject)
   1. [ Bind Expression](#BindExpression)
1. [ Involvement of Pogramming Paradigms](#InvolvementofPogrammingParadigms)
1. [ Shared_ptr](#Shared_ptr)
1. [ Tips to design a class ](#Tipstodesignaclass)
1. [ Use const whenever possible](#Useconstwheneverpossible)
1. [ Initialization ](#Initialization)
1. [  Constructor ](#Constructor)
1. [ Not to call virutal function in constructor](#Nottocallvirutalfunctioninconstructor)
1. [ Copy constructor and assignment](#Copyconstructorandassignment)
1. [ Reference](#Reference)
1. [ Runtime typeinfo](#Runtimetypeinfo)
1. [ STL](#STL)
1. [ Exception](#Exception)
   1. [ [Thread Safty](http://www.boost.org/community/exception_safety.html) -- No Memory Leak](#ThreadSaftyhttpwwwboostorgcommunityexception_safetyhtmlNoMemoryLeak)
   1. [ [The Three Exception Guarantees](http://www.boost.org/community/exception_safety.html)](#TheThreeExceptionGuaranteeshttpwwwboostorgcommunityexception_safetyhtml)
   1. [ Debug an exception](#Debuganexception)
1. [ Behind STL container](#BehindSTLcontainer)
1. [ Copy Elision](#CopyElision)
1. [ string ](#string)
1. [ Polymorphic](#Polymorphic)
1. [ Default Class functions synthesized by compiler](#DefaultClassfunctionssynthesizedbycompiler)


### Headers  <a name="Headers"></a>

*How to determine the number of headers used in a program*:
1. From the perspective of average user, it should not be too many 
2. From the perspective of implementers, multiple headers are unavoidable for functionality partition purpose.
(20191001 from C++ 4rd)_

*Initialization of nonlocal variables*:

global, namespace and class static variables are initialized before main main() is invoked in their defination order. The order are not guaranteed between different compile units.  不要指望不同编译单元的全局变量有什么依赖关系


### Function  <a name="Function"></a>
The most typical form of callable target
```
int fun(int arg1){
    ...
}

typedef int (*FUNC_TYPE)(int); 

FUNC_TYPE funVar = fun;
```

###  Lambda Expression  <a name="LambdaExpression"></a>
https://github.com/garfielder/notes/blob/master/Programming/Cpp11.md#Lamda

### Function Object <a name="FunctionObject"></a>
https://github.com/garfielder/notes/blob/master/Programming/CppTips.md#functionObj

### Bind Expression <a name="BindExpression"></a>
FIXME: pointing to studio/cpp/boost/main.cpp <br>
Return a function object based on an existing function or member functions, with argument bound 

## Involvement of Pogramming Paradigms <a name="InvolvementofPogrammingParadigms"></a>

* Procedural Programming
	* forcus on process  -  the algorithm to perform the desired computation
	* supported by providing functions and returned values
* Mudular Programming
	* A set of related procedures with the data they manaipulate is often call a module
	* Partition the program so that the data is hidden within modules
	* Separation of compilation. each modules can  be compiles in a single .cpp file
* User-Defined Types
	* Decide which type you need, and provide a full set of operations for each type
	* 
* Object-Oriented Programming
	* Decide which class you want
	* Provide a full set of operations for each class
	* Make commonality explict by using inherence
* Generic Programming
	* Decide which algorighms you want:
	* parametererize them so that they work for a variety of suitable types and data structures
	
See more in <<The C++ Programming Languages>>

## Shared_ptr <a name="Shared_ptr"></a>
put a newed pointer into shared_ptr  in a single sentence.  Otherwise exception would cause memory leak 


# Function Object 
<a name="functionObj"></a>
**Function Object** is an object that  looks like a typical function 

```c++
struct TwoOperand
{
    void operator()(int a, int b)
    {
        cout << "sum of a + b is " << a + b << endl;
    }
};

int main()
{
    TwoOperand  add;
    add(3, 4); 
}
```

Compared with funciton, it is more fanstastic compared with function, e.g, it can carry internal state. For example, we can update above program into something below 
```c++

enum OPERATOR{
    ADD, 
    SUB,
    MUL
};

struct TwoOperand
{
    OPERATOR  _opType;
    TwoOperand(OPERATOR opType=ADD){_opType = opType;}
    void operator()(int a, int b)
    {
        if (ADD == _opType)
            cout << " a + b is " << a + b << endl;
        else if (SUB == _opType)
            cout << "a - b is " << a - b << endl;
        else{
            cout << "TODO" << endl;
        }
    }
};

int main()
{
    TwoOperand  add;
    TwoOperand  sub(SUB);
    add(3, 4); 
    sub(10, 4); 
}
```
## Tips to design a class  <a name="Tipstodesignaclass"></a>
* DONOT expected to return an reference
	* It may refer to an local variable, that will be destroied soon
	* Using  `new`ed objects, it is easily to cause memory leak
	* static is not safe in multiple thread environment
* Pefer non-member function to member function
	* The more member functions there are, the more functions there will be to access private member of a class
		* This is bad for encapsulation
	*  Too member function leads to big dependence for  class customer
## Use const whenever possible <a name="Useconstwheneverpossible"></a>

* Before and Afer pointers
   * `const char* pStr; // pointer to a constant string`
   * `chart* const pStr; // a constant pointer, the string is not necessarily constant
* Constant member
   * Not allow to change non-static members
      * can change mutual class member ( page 23 of [1])
* const and non-constant can be overloaded     
      
## Initialization  <a name="Initialization"></a>
* Initialize a class in initialization list, so it can be done before construcor
* There is no guratee of initialization sequence of objects in difference compilization unit (different .o or .obj file)
##  Constructor  <a name="Constructor"></a>
* C++ compiler create default constuctor/copy constructor/copy assignment/descructord 
* Sometime need to stop above default member from being called by setting private and not implemented(stop friend class)
* desctructor should be virutal if a class have virutal members, other wise, delelte the point would only release the base class part.  If no virutal member , it is not supposed to be a base class

## Not to call virutal function in constructor <a name="Nottocallvirutalfunctioninconstructor"></a>
设想班级管理系统中有学生和班干部类，班干部类派生于学生类。 有一虚函数名为报告身份。 构造班干部时，要先构造学生，换句话，若当干部，先当学生。当学生的过程中，他报告身份，依然是学生，他不知道自己未来变成干部

## Copy constructor and assignment <a name="Copyconstructorandassignment"></a>
Copy function should make sure to copy every member including base class part
## Reference <a name="Reference"></a>
[1]: Effective C++

## Runtime typeinfo <a name="Runtimetypeinfo"></a>
```cpp
#include <iostream>
#include <typeinfo>

using namespace std;
struct MyStruct{
	int member;
	int member2;
};

int main( void )
{
	struct MyStruct mystruct = { 3, 5};

	cout << typeid(mystruct).name() << endl;
}

```


## STL <a name="STL"></a>
* iterator
    * It is similar to pointer, which is pointing an objects, can be dereferernced, increase, decresed, comparasion, ...
    * Different type of iterators have different level of functionlity. See [here](http://www.cplusplus.com/reference/iterator/)
    * 
* Stream
    * Stream are something that help searilize objects(int,string...) into strings 
    * Stream are abastration of a a device on which input and output are performed. [link](http://www.cplusplus.com/reference/iolibrary/) 
    * cin/cout are pre-defined ojbect of stream type. ```cout << "li" << "yong"``` is equal to ((cout<< "li") << "yong").  each bracket returns the reference to cout itself.
       * ```cout``` is defined as ```extern ostream cout```  , so it must implemented somewhere 
    * ```ostream_iterator```
        * derived from iterator
        * it points to an item that is supposed to be output.
        * It is a new form of using ```cin```, ```cout```, which works well with ATL container.
* ```boost::any```
   * Represent data of any type
      *  ``` boost::any anyType;  anyType = 18;     cout << any_cast<int>(anytype) << endl;```
      *  expection bad_any_cast returns with any_cast failure
* ```unordered_set```
   * It stores elements not in a particular order, but according to their value. The value itself is its key.
   * They are stored in one of the bullets index by the hash value of their
   * Compared with vector,  it is faster to acess one element, but slow to loop though a range. 
* ```*_if```
   * count_if: return the number of object.  count_if(input_iterator inputBeginItr, input_iterator endItr, cbPredicate)
   * find_if: 
   * copy_if: c++11
* ```boost::function and boost::bind```
   * ```boost::function``` can be used to write a generic function pointer including pointing to member function, while ```boost::bind``` is used to create such a generic function pointer
   ```c++
#include <boost/function.hpp>
#include <boost/bind.hpp>
#include <iostream>

using namespace std;

class Foo {
public:
    Foo(){}
    virtual ~Foo(){}
    virtual void  Bark2(std::string msg) { cout << "wang: " << msg << endl; }
private: 
};

class Child : public Foo {
public: 
    virtual void Bark2(std::string msg) { cout << "Miao: " << msg << endl; } 

};

void Bark2(std::string msg)
{
    cout << "QiuQiu:  " << msg << endl;
}

int main()
{
    Foo foo;

    boost::function<void(string)> f1, f2, f3;

    Child* pFoo = new Child();

    f1 = boost::bind(&Foo::Bark2, &foo, _1);
    f2 = boost::bind(&Foo::Bark2, pFoo, _1);
    f3 = boost::bind(&Bark2, _1);
    f1("can see see me");
    f2("can see see me");
    f3("can see see me");
}
```

## Exception <a name="Exception"></a>

Often, the modules that detects error does not know what action to take. The recovery action  depends on the module that invoked the operation that the module that is performing the operation. \<\<section 2.4.2 of The C++ Programming Language\>\>


* Three keywords 
	* ```try```
	* ```throw```
	* ```catch```
* In the try block, we can use throw statement  through a exception message object. The boject is not mysterious, but can be int, char, string, or any user-defined class
* When run into ```throw```,  current function will execute ```return``` imedediatly, and use destructor to clear local objects. 
* If ```catch``` block is not found in high level funtion, above action will be repeated until find the matched ```catch``` block

What kinds of objects can be thrown? Any type!  It could be int,string, or user-defined class. There are also some user defined exception object (*FIXME*).  Meanwhile, anyobject can be catched. 

### [Thread Safty](http://www.boost.org/community/exception_safety.html) -- No Memory Leak <a name="ThreadSaftyhttpwwwboostorgcommunityexception_safetyhtmlNoMemoryLeak"></a>
RAII --> Resource esource Acquisition Is Initialization .  Use shared_ptr when possible. So, resource can be well released even when exception is throw anywhere even in constructor. 
### [The Three Exception Guarantees](http://www.boost.org/community/exception_safety.html) <a name="TheThreeExceptionGuaranteeshttpwwwboostorgcommunityexception_safetyhtml"></a>
* No-fail guarantee 
	* The user can guratee  the function won't through an exception or can eat all internal exceptions.
* Strong guarantee
	* A function goes out of scope because of an exception, it should not cause memory leak or change program state. Actually an transaction with commit or rollback semantic.  Could be done by "copy and swap "
	"copy and swap" is expensive in memory consumption
* Basic Guarantee
	* When exception happens, no memory leaked and the object is still in a usable state. 

### Debug an exception <a name="Debuganexception"></a>

http://www.sourceware.org/gdb/current/onlinedocs/gdb/Set-Catchpoints.html


# ```inline ```
* It looks like function, without overhead of a funtion call
* It is similar to C-style macro, but with type-safe.
* Since inline leads to code replacement, in some case, it leads to inline expansion.
* It is just a compiler directive, not a requirement
* Functions defined  in class defination is an implicit inline function

#```pragma```
* ```#pragma once``` 
	* Make sure the head is only compiled once
* ```#pragma message("Hello, I am in compiler"); // output in compilation stage```
* * ```#pragma Warning("Hello, I am in compiler"); // warning in compilation stage```

# extern
we can see extern "C" in many place, what is it? <br>
Cpp code defined within {} will be compiled  and linked in a "C" way. For example, a function void foo(int, int), in C, it will be stored as 'foo' in object file. However in CPP, it may become some strange name such "foo_int_int", which is used to handle overloading.
Whey we have to compile our cpp file in a "C" way, it is because there are many excellent and stable c libraries(such as stdio.h), if they want to be used, extern C is needed, or there will be link error.

```c
exern "C"{
/* Code */
}
```

# const 

For class member 
```c++
class A {
public:
	void fun(const Param&  param)  const ;
};
````

The first constant means argument *param* cannot be changed. 
The second const means  *fun* is not allowed to modify any class member 


# Prefer std::copy rather than memcpy

```c++
#include <iostream>
#include <string.h> // for memcpy
#include <algorithm>

using namespace std;

class A{
public:
    A(){}
    A(const A& a){ cout << "in copy constructor (this " << this << ")" << endl;}
    A& operator=(const A& a){ cout << "in copy assignment (this " << this << ")" << endl;}
};

int main()
{
    A  as[] = {A(), A()};
    A  tar[2];

    A a = as[0];

   // memcpy(tar, as, sizeof(as)); // bitwise copy, unsafe, no copy assignment  called
   std::copy(as, as+1, tar);       // safe, copy assignment called

    cout <<  sizeof(A) << endl;

    return 1;
}
~           
```
## Behind STL container <a name="BehindSTLcontainer"></a>

*std::vector* :  actually an array. And we can get the  address iTH elements by ```&vec[0] + i * sizeof(elem)```

*std::list*:  doubled linked list

*std::map & std::set*:  implemented by highly banlanced tree such as AVL  or Red-Black tree.  The worst insert and  find time complexity is O(logn)

*std::unordered_set*:  implemented by hash table,  can be indexed by their value.  The find and insert can be done with O(1) .

## Copy Elision <a name="CopyElision"></a>
```c++
/* atexit example */

#include <iostream>
using namespace std;


class MyClass{
public:
    MyClass() { cout << " In constructor " << endl;}
    ~MyClass() { cout << " In destructor" << endl;}

    MyClass(const MyClass&  other) { cout << " In copy constructor " << endl; }
   
    MyClass& operator= (const  MyClass& other) { cout << "In copy assignment " << endl; }
    
};

MyClass GetClass()
{
    MyClass myclass;
    cout <<" In Get Class, pointer is " << &myclass << endl;
    return myclass;
}

int main(){
    MyClass my = GetClass();
    
    // due to compiler optimization, my is the same object as defined in
    // GetClass, the copy constructor is skipped
    cout << "My is " << &my <<endl; 
}
```
## string  <a name="string"></a>
it is safe to return a c string because string literal is statically allocated 

```c++
const char* error_message(int i)
{
// ...
return "range error";
}
```

## Polymorphic <a name="Polymorphic"></a>

多态是个很广泛的概念。 字面意思是表面看起来的相同的事物，因为内部潜在的差异， 而产生的行为不同。 两兄弟，一个喜欢吃甜，一个喜欢吃咸，同时接到一块糖，表现是不一样的。 C++中的多态有很多具体的表现形式：

   * Pointer
   ```
   void *p = new int;
   p = new float; 
   // p can point to different content although they looks the same 
   ```
   * Call back function
   ```
   typedef  (void)(*Fun)()
   vod fun1() { printf("fun1\n"); }
   vod fun2() { printf("fun2\n"); }
   
   p = Fun1;  p();
   p = Fun2;  p(); 
  ```
  * function overload
  * template
  * virtual fucntion
  
## Default Class functions synthesized by compiler <a name="DefaultClassfunctionssynthesizedbycompiler"></a>
  
  A trival constructor initiaze does not initialize any class member
  A default constructor is non-trival in the following case: 
  
  If a class member have default constructor, the class itself will have a default constructor
  
  If a base class has default constructor, it derived will have a default constructor
  
  If a class has a virtual member in it or in its parent class, it should have a default constructor to construct its vptr
  
  Inside_the_C++_Object_Model.pdf: section 2.1
  
  ## C++ memory layout 
  ```
  class A
  { public:
      A()

       int s;
  };
A::s = 2;

int main()
{
 	A a;
	A* pa = &a;
	a.s = 3;
	pa->s = 4;
}
```
A::s_memeber is unqiue for all class objects and stored in data segment. 
a.s and pa.s are identical in compiler. They access the static variabeble in data segment directly


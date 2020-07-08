
# C++11 New features 

C++11 introduced a few grammar sugars that helps programmer to write less code, such as ```auto```,  ```decel``` . It brings features from mordern languages such as lamda function. It includes more tr1 library as its stardard library. 

The new features put more more workload on compiler. 

## Table of Content
1. [ ```auto```](#auto)
1. [ ```constexpr```](#constexpr)
   1. [ Vs ```const```](#Vsconst)
1. [ ```decltype```](#decltype)
1. [  Lamda function](#Lamdafunction)
1. [ Plain Old Data ](#PlainOldData)
1. [ ```typedef``` Vs  type alias ](#typedefVstypealias)
1. [ In-class member initializers](#Inclassmemberinitializers)
1. [ Constructor Delegation in C++](#ConstructorDelegationinC)
1. [ Copy and Move](#CopyandMove)
1. [ Template](#Template)
   1. [ specialization ](#specialization)
   1. [ concept and constraint](#conceptandconstraint)
1. [ Initialization List](#InitializationList)
   1. [ Four ways for initialization](#Fourwaysforinitialization)
   1. [ uninitialized variable ](#uninitializedvariable)
   1. [ As arguments to a parameter  of ](#Asargumentstoaparameterof)
1. [ explicit ```default```ed  or ```delete```d  special functions](#explicitdefaultedordeletedspecialfunctions)
1. [ Mist ](#Mist)
   1. [ Arrary reference ](#Arraryreference)
1. [ smart pointer ](#smartpointer)
   1. [ shared_ptr](#shared_ptr)
   1. [ unique_ptr](#unique_ptr)
1. [  Use chrono to count time interval ](#Usechronotocounttimeinterval)
1. [ traits](#traits)
   1. [ type traits](#typetraits)
1. [ Differences ](#Differences)
1. [ Reference ](#Reference)

## ```auto``` <a name="auto"></a>
With auto, we don't have to indicate a type explictly because it can be deduced on the right of '=' operator.  So ```for (std::vector<int>::conster itr = vec.begin(); ...```), can be saved as ``` for (auto itr = vec.begin(); ...) ```

## ```constexpr``` <a name="constexpr"></a>
Similar to inline, it tells compilers this experssion can be caculated during compilation time. 

```C++
// https://en.wikipedia.org/wiki/C%2B%2B11
constexpr int get_five() {return 5;}
int some_value[get_five() + 7]; // Create an array of 12 integers. Legal C++11
```
### Vs ```const``` <a name="Vsconst"></a>
* ```constexpr``` is to enalbed and ensure compile-time enavluation
* ```const ``` is simply to specify immutability in interfaces. 

The purpose to have both is t oavoid using literals scatterred around, which is one of the nastiest mantenance hazards. 

## ```decltype``` <a name="decltype"></a>
get the type of variable and return the type. The expression is resolved in compilation
```c++

    vector<int> vec;
    vec.push_back(1);
    vec.push_back(2);
    int m = 1;
    decltype(vec[0]) x = m;

```

##  Lamda function <a name="Lamdafunction"></a>
<a name="Lamda"> </a>
Anonymous  function. The concept is is python for a long time. It provided a fast way of creating functions. 
Python's lambda expression is simple, just remove the function name. But C++ lambda support is a bit difficult, it also has a concept named 'capture list', which are names in local environment

```c++
[capure_list](argument_list){function_body}
```

```c++
     int base = 100;  // name in local environment
    vector<int> vec;
    vec.push_back(1);
    vec.push_back(3);
    vec.push_back(5);
    for_each(vec.begin(), vec.end(), [base](int x){printf("- %d - ", base + x );});
```

## Plain Old Data  <a name="PlainOldData"></a>

Simply speaking, it should be an data type which behaves like C, can be copied  bitwisely.

Precisely speaking, a POD is an object that can be manipulated as `just data` without worrrying about compicatons of class layouts or user-defined semantics for contruction, copy, and move
* Trival . The class has a trival 
    * default constructor
    * default copy constructor
    * default copy assignment operator
    * default destructor
* Standard layout
    * no virutal member  (no vptr)
    * no virutal member in base  (no vptr)
    * all member with same access control
    * all memboer defined in the same on class in the hierarchy so that data layout optimization won't be impacted. 
 
```is_pod``` is introduced to check pod or not

## ```typedef``` Vs  type alias  <a name="typedefVstypealias"></a>

Answer is simple: NO DIFFERENCE <br>
```using TestItem = shared_ptr<Base>;``` <br>
```typedef shared_ptr<Base> TestItem```


## In-class member initializers <a name="Inclassmemberinitializers"></a>

But  the real benefits come in classes with multiple constructors. Often, all constructors use a common initializer for a member: 
```
	class A {
	public:
		A(int x): a(x) {}  // a will override the default value of 7
		int a = 7;
	};
```

## Constructor Delegation in C++ <a name="ConstructorDelegationinC"></a>
One constructor calls another constructor in a class to avoid duplication
```
class A
{
public:
    A(int a) {_a = a; assert(a > 3); }
    A(int a, string b): A(a) {_b = b; assert(b != ""); }


    int _a;
    string _b;
};
```

## rvalue reference


https://www.cprogramming.com/c++11/rvalue-references-and-move-semantics-in-c++11.html

## Copy and Move <a name="CopyandMove"></a>
```c+
x= y;
```
* *Copy* is the conventional meaning, after assignment, x and y  are both equal to y's original value
```c++
 	X(const X&) // Copy constructor
	X& operator=(const X&) // Copy assignment
```
* *Move* leaves ```x``` with ```y```'s former value and ```y``` with some *moved-from* state
    * More efficient
    * move contructor takes xvalue type (see http://en.cppreference.com/w/cpp/language/value_category)
```c++
	X(X&& other); // move constructor
```
        

Stroustrup gave a good example. Suppose A wants to have a car like B's .  Solution one: B give car to A ï¼regardless of the money paid), B find out A's car Information, by a completely new one.   Solution 1 is shadows copy or move, solution 2 is deep copy.


Notice there is no implicit move contructor, if no explict move constructor, it will be copy constructor instead. The reason is that, the compiler does not know how to remove the xvalue. 

## Template <a name="Template"></a>

function template can be deduced by compiler. 

```c++

template <typename T>
void fun2(T a){
    std::cout << "Temp func :" << a << std::endl;
}

fun(18);
fun("string");
fun<int>(18);
fun<int>("string"); // error
```

class template parameters are neverred  decuded, user must put it into \<\> explicitly


 
### specialization  <a name="specialization"></a>
template defines a generic class or function with one or parameters.  <br>
The parameters  can be a type/value/template <br>

Compiler generated differnet implementations of a template based on different arguments. 

specialization is a technique to make one kinds of argument special, which is not follow the template. 

A useful use case , please refert to 25.3 of [link](#cppbook)



### concept and constraint <a name="conceptandconstraint"></a>
This is not C++11, but more modern ideas in C++17<br>

In a typical functions call, we spend some efforcts to validate incomming arguments, if error, we fire an assertion or someother error message. <br>

We need some checking mechanism for template arguments.   ```constraint``` are such checks defined in implementation. It is similar to reguar function argument, the difference is done by compilation-time check such as ```static_assert```

A ```concept``` is a named set of  requirement in the form of something like a function, it is a predicate 

```c++ 
// from http://en.cppreference.com/w/cpp/language/constraints
// variable concept from the standard library (Ranges TS)
template <class T, class U>
concept bool Derived = std::is_base_of<U, T>::value;
 
// function concept from the standard library (Ranges TS)
template <class T>
concept bool EqualityComparable() { 
    return requires(T a, T b) { {a == b} -> Boolean; {a != b} -> Boolean; };
}
```


## Initialization List <a name="InitializationList"></a>

### Four ways for initialization <a name="Fourwaysforinitialization"></a>
```c++
	int a(18);
	int b = 19;  /* c style */
	int c { 20 };  // c++11 new, initialization list
	int d = { 21 }; /*c style */
```

List initialization can wildly be used in more context than other three.  However, it is not as good as '=' when type deduction is needed

empty ```{}``` means default value.  for pionter it is ```nullptr```
```c++
	int a[18]; // uninialized values
	int a[18]{}; // zero values
```

```{}``` does not support narrowing convertation, such as int -\> char
### uninitialized variable  <a name="uninitializedvariable"></a>
for variable stored in data segment ( global/static variable),  uninitialized means ```{}```, which means it is 0. <br>

for variable stored in heap or stack, its value is underdermined. On Windwos, it is a random data, on Linux, it is zero

### As arguments to a parameter  of  <a name="Asargumentstoaparameterof"></a>
* std::initializer<T>
* A type can be initialized with the values in the list (equal to () of the legacy way) 
* A refernce to an array of T. 

See section of 12.2.3  of  [1](#cppbook)


## explicit ```default```ed  or ```delete```d  special functions <a name="explicitdefaultedordeletedspecialfunctions"></a>
C++11 has 6 special class member funcitions.  We can ask compiler explicitly to let it generate or supress an exact functions below. 
```c++
	class MyClass{
	public:
		MyClass()=default;  // default constructor
		~MyClass()=default; // default destructor
		MyClass& MyClass(const MyClass& other) = default ; //default copy constructor
		MyClass& operator=(const MyClass& other)=default;  // default assignment 
		MyClass(MyClass&& other)=default; // default move constructor  
		MyClass& operator=(MyClass&& other)=default ; // default move assignment 
		
	};
```

## Mist  <a name="Mist"></a>
This section contains simple tips

### Arrary reference  <a name="Arraryreference"></a>
```f(T* a)``` or ```f(T a[])``` lost the arrary size information of the argument.   Array reference can solve this problem 

```c++
#include <iostream>
using namespace std;

template<class T, int N>
void f(T(&r)[N])
{
    cout << sizeof(r) << endl;
}

int main(){
    char a[4] = {4, 3, 5, 9};
    f(a);
}
```
## smart pointer  <a name="smartpointer"></a>

Used for RAII. Exception-safe. Avoid memory leaking.

### shared_ptr <a name="shared_ptr"></a>
1. How  initialize:
```c++
	shared_ptr<int> sp(new int(3));
	shared_ptr<int> sp = make_shared<int>(3); // safe way
```
2. It can be copied, this is why it is named _shared_.  Multiple shared pointer can point to the same object instance. 
when the last pointer is deleted, the instance itself is deleted automatically. 

### unique_ptr <a name="unique_ptr"></a>
1. compared with shared_ptr, an object can only be pointed to by a unique pointer. Copying a uniuqe ptr causes compilation error.  But std::move could work. 
2. It is a light-weight smart pointer compared with shared_ptr. 
3. make_unique is also available.

##  Use chrono to count time interval  <a name="Usechronotocounttimeinterval"></a>

```c++
#include <chrono>
 std::chrono::time_point<std::chrono::system_clock> start, end;
 start = std::chrono::system_clock::now();
 // do something 
 end = std::chrono::system_clock::now();
 
    std::chrono::duration<double> elapsed_seconds = end - start;
    std::cout << " elapsed time: " << elapsed_seconds.count() << "s\n";

```

## traits <a name="traits"></a>
### type traits <a name="typetraits"></a>
Defined in standand library <type_traits>. Provided functions to determines the properties of types, genenrate new types. It is primiarily used in compile time.
```
is_pod<X>::value
is_pod<X>()
is_pointer<T>

add_const<X> // try to add const to type X
```

## Differences  <a name="Differences"></a>
| First | second  | comment|
|-------|---------|--------|
|nullptr|NULL|nullptr is type-safe, e.g. it cannot be assigned to a int, NULL is 0L in c++ but (void*)0 in C, it leads confusion when overloadded function takes either a pionter or integer |

## Reference  <a name="Reference"></a>
1. <a name=cppbook> The C++ Programming Language. Fourth Edition. </a>

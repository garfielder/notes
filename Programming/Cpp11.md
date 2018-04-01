# C++11 New features 

C++11 introduced a few grammar sugars that helps programmer to write less code, such as ```auto```,  ```decel``` . It brings features from mordern languages such as lamda function. It includes more tr1 library as its stardard library. 

The new features put more more workload on compiler. 


## ```auto```
With auto, we don't have to indicate a type explictly because it can be deduced on the right of '=' operator.  So ```for (std::vector<int>::conster itr = vec.begin(); ...```), can be saved as ``` for (auto itr = vec.begin(); ...) ```

## ```constexpr```
Similar to inline, it tells compilers this experssion can be caculated during compilation time. 

```C++
// https://en.wikipedia.org/wiki/C%2B%2B11
constexpr int get_five() {return 5;}
int some_value[get_five() + 7]; // Create an array of 12 integers. Legal C++11
```
### Vs ```const```
* ```constexpr``` is to enalbed and ensure compile-time enavluation
* ```const ``` is simply to specify immutability in interfaces. 

The purpose to have both is t oavoid using literals scatterred around, which is one of the nastiest mantenance hazards. 

## ```decltype```
get the type of variable and return the type. The expression is resolved in compilation
```c++

    vector<int> vec;
    vec.push_back(1);
    vec.push_back(2);
    int m = 1;
    decltype(vec[0]) x = m;

```

##  Lamda function
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

## Plain Old Data

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

## ```typedef``` Vs  type alias 

Answer is simple: NO DIFFERENCE <br>
```using TestItem = shared_ptr<Base>;``` <br>
```typedef shared_ptr<Base> TestItem```

## Copy and Move
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
        

Stroustrup gave a good example. Suppose A wants to have a car like B's .  Solution one: B give car to A （regardless of the money paid), B find out A's car Information, by a completely new one.   Solution 1 is shadows copy or move, solution 2 is deep copy.


Notice there is no implicit move contructor, if no explict move constructor, it will be copy constructor instead. The reason is that, the compiler does not know how to remove the xvalue. 

## Template

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


 
### specialization 
template defines a generic class or function with one or parameters.  <br>
The parameters  can be a type/value/template <br>

Compiler generated differnet implementations of a template based on different arguments. 

specialization is a technique to make one kinds of argument special, which is not follow the template. 

A useful use case , please refert to 25.3 of [link](#cppbook)



### concept and constraint
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


## Initialization List

### Four ways for initialization
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
### uninitialized variable 
for variable stored in data segment ( global/static variable),  uninitialized means ```{}```, which means it is 0. <br>

for variable stored in heap or stack, its value is underdermined. On Windwos, it is a random data, on Linux, it is zero

### As arguments to a parameter  of 
* std::initializer<T>
* A type can be initialized with the values in the list (equal to () of the legacy way) 
* A refernce to an array of T. 

See section of 12.2.3  of  [1](#cppbook)


## explicit ```default```ed  or ```delete```d  special functions
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

## Mist 
This section contains simple tips

### Arrary reference 
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
## smart pointer 

Used for RAII. Exception-safe. Avoid memory leaking.

### shared_ptr
1. How  initialize:
```c++
	shared_ptr<int> sp(new int(3));
	shared_ptr<int> sp = make_shared<int>(3); // safe way
```
2. It can be copied, this is why it is named _shared_.  Multiple shared pointer can point to the same object instance. 
when the last pointer is deleted, the instance itself is deleted automatically. 

### unique_ptr
1. compared with shared_ptr, an object can only be pointed to by a unique pointer. Copying a uniuqe ptr causes compilation error.  But std::move could work. 
2. It is a light-weight smart pointer compared with shared_ptr. 
3. make_unique is also available.

##  Use chrono to count time interval 

```c++
#include <chrono>
 std::chrono::time_point<std::chrono::system_clock> start, end;
 start = std::chrono::system_clock::now();
 // do something 
 end = std::chrono::system_clock::now();
 
    std::chrono::duration<double> elapsed_seconds = end - start;
    std::cout << " elapsed time: " << elapsed_seconds.count() << "s\n";

```

## traits
### type traits
Defined in standand library <type_traits>. Provided functions to determines the properties of types, genenrate new types. It is primiarily used in compile time.
```
is_pod<X>::value
is_pod<X>()
is_pointer<T>

add_const<X> // try to add const to type X
```
## Reference 
1. <a name=cppbook> The C++ Programming Language. Fourth Edition. </a>

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

## Lamda function 
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

## Construct/cleanup/Copy/Move
TODO

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

### uninitialized variable 
for variable stored in data segment ( global/static variable),  uninitialized means ```{}```, which means it is 0. <br>

for variable stored in heap or stack, its value is underdermined. On Windwos, it is a random data, on Linux, it is zero

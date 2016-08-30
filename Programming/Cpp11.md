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

## ```decltype```
get the type of variable and return the type. The expression is resolved in compilation
```c++

    vector<int> vec;
    vec.push_back(1);
    vec.push_back(2);
    int m = 1;
    decltype(vec[0]) x = m;

```

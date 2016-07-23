## Shared_ptr
put a newed pointer into shared_ptr  in a single sentence.  Otherwise exception would cause memory leak 

## Tips to design a class 
* DONOT expected to return an reference
	* It may refer to an local variable, that will be destroied soon
	* Using  `new`ed objects, it is easily to cause memory leak
	* static is not safe in multiple thread environment
## Use const whenever possible

* Before and Afer pointers
   * `const char* pStr; // pointer to a constant string`
   * `chart* const pStr; // a constant pointer, the string is not necessarily constant
* Constant member
   * Not allow to change non-static members
      * can change mutual class member ( page 23 of [1])
* const and non-constant can be overloaded     
      
## Initialization 
* Initialize a class in initialization list, so it can be done before construcor
* There is no guratee of initialization sequence of objects in difference compilization unit (different .o or .obj file)
##  Constructor 
* C++ compiler create default constuctor/copy constructor/copy assignment/descructord 
* Sometime need to stop above default member from being called by setting private and not implemented(stop friend class)
* desctructor should be virutal if a class have virutal members, other wise, delelte the point would only release the base class part.  If no virutal member , it is not supposed to be a base class

## Not to call virutal function in constructor
设想班级管理系统中有学生和班干部类，班干部类派生于学生类。 有一虚函数名为报告身份。 构造班干部时，要先构造学生，换句话，若当干部，先当学生。当学生的过程中，他报告身份，依然是学生，他不知道自己未来变成干部

## Copy constructor and assignment
Copy function should make sure to copy every member including base class part
## Reference
[1]: Effective C++

## Runtime typeinfo
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


## STL
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



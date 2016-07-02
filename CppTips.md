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
## Reference
[1]: Effective C++

##
### STL
* iterator
    * It is similar to pointer, which is pointing an objects, can be dereferernced, increase, decresed, comparasion, ...
    * Different type of iterators have different level of functionlity. See [here](http://www.cplusplus.com/reference/iterator/)
    * 

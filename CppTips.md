## Use const whenever possible

* Before and Afer pointers
   * `const char* pStr; // pointer to a constant string`
   * `chart* const pStr; // a constant pointer, the string is not necessarily constant
* Constant member
   * Not allow to change non-static members
      * can change mutual class member ( page 23 of [1])
* const and non-constant can be overloaded     
      

## Reference
[1]: Effective C++

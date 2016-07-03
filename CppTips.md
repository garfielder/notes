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
* Stream
    * Stream are something that help searilize objects(int,string...) into strings 
    * Stream are abastration of a a device on which input and output are performed. [link](http://www.cplusplus.com/reference/iolibrary/) 
    * cin/cout are pre-defined ojbect of stream type. ```cout << "li" << "yong"``` is equal to ((cout<< "li") << "yong").  each bracket returns the reference to cout itself.
       * ```cout``` is defined as ```extern ostream cout```  , so it must implemented somewhere 
    * ostream_iterator
        * derived from iterator
        * it points to an item that is supposed to be output.
        * It is a new form of using ```cin```, ```cout```, which works well with ATL container.
* boost::any
   * Represent data of any type
      *  ``` boost::any anyType;  anyType = 18;     cout << any_cast<int>(anytype) << endl;
      *  expection bad_any_cast returns with any_cast failure

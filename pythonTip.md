## Advanced usage of List

###  List comprehension 
It comes from concept of set operation in mathmatic.  such as {x * 2 | x in N, x % 2 == 0} <br>
construct a new list based on existing one.<br>
An elegant to create new list. also availabe in c++ STL algorithm library. 


```python
>>> listN = [1, 3, 5]
>>> print listN
[1, 3, 5]
>>> [n for n in listN]
[1, 3, 5]
>>> [n*10 for n in listN]
[10, 30, 50]
>>>
```

List comprehension is faster than ```for``` loop, because ```for``` loop is running on PVM, while list compresension is implemented with __C__ code. 

### 从列表查找元素

方法1：
```python
    mylist = ['Garfield', 'Odie', 'Nelman']
    if 'Odie' in mylist:  # this is the best way
	    print 'yes'
	else:
		print 'no'
```
方法2：
    use `List.index(x)` , 但是当x不存在时会触发异常

## Type basics

``` python
    a = [1, 2 , 3]
    a = 0
```
Once the last reference is removed, the object is deleted, which is some kinds of garbage recollection mechnasim

Basic types are digit, string, list, tupple, dict, file

new type: set/NOne, boolean.  NOTICE, set operation may be useful sometime.

### Get Help
dir(obj) # return all priorities of obj <br>
help(obj.priority) # find out spec of a function <br>

### Number
octal literal starts with '0' <br>
hex literal starts with '0x' <br>

<br>

convert from decimal to hex : ` hex(64)` ,  <br>
convert from string to number : `eval('100'), eval("0x40")` <br>

### variable/object/reference

```python
	a = 3;
```
Three steps to meet above requirement:  

1.  Create an object to stand for 3
2.  Create a variable 'a' if it is not there
3.  Map variable 'a' and object 3. 


So, <br>
*  Variable is symbolic element in sysmem table 
*  object is a memory space in memory, which is big enough to hold its data.  *type* belongs to object rather than variable
*  Reference is a pointer from variable to object, can be used for object serialization , but the best one is pickle.

All assignment is passing reference of object rather than cloning. There a few ways to clone list, Dict. List[:], Dict.clone(), list(list)

a `is` b : a and b refers to the same object  <br>
a `==` b:  a equal b , compare member to member <br>

### String Tips
From learning python

* 字符串表示
	*   单引号
	*   双引号
	*   通过raw抑制转义
	   *   常用于表示windows路径和正则表达式
	   *   open("c:\\new\\text.dat", "w")  Vs  open(r"c:\new\text.dat", "w")
	*    三重引号
	   *   文档字符串
	   *   注释代码的好方法
	   *   可以在前面加上raw抑制转义
* 分片
   *  str[i:j]
   *  str[i:j:k]  # 从i 到j-1 每隔k个进行索引
* method
   * rstrip: remove tariling whitespace. ususlly for end-of-line
   * eval(string): convert string into executable. Convert string into python code.

### Dict
`list` is a collection of other objects in a given order, while `dict` is a collection of other objects with no order. Elements in `dict` is referred by key rather than offset.

## Iterator

An iterable objects includes list sequencial data type (list, string, tupple), some non-sequence type(dict, file) and any objects that has __getitem__ or __iter__ method. <br>

An iterator object  =  an iterable object + Next() method <br>
```iter(<iterable object>)``` grants the magic Next() to iterable object

[here](http://www.cnblogs.com/bukekangli/p/5152451.html) for more

* ```zip``` can be used to construct dict
```pythobn
key = ['a', 'b']
value = [9, 10]
d = dict(zip(key, value))
```

* enumerate can disintegrate an list into list of （index， data）tupple


## Function 
### difference with C
def is an executable sentence , like ``` a = "lyq" ```,  ```def``` create a function object and assign to  the function name.  function name is a reference to the function object.

### lambda
* light-weight funtion
* takes any number of arguments
* return the value of a single expression
* It helps to save code from having too much one line functions. 

[Here](http://www.diveintopython.net/power_of_introspection/lambda_functions.html) for more
### Yield
* ```yield```  is only used when defining a generator function 
*  If ```yield``` appers in the body of a funtion starting with ```def```, it is no longer a regular function but a generator function.
*  When generator function is called it returns an iterator known as generator. 
*  The generator then controls of the generator function. 
*    generator.next()  starts generator funtion until the first yield experssion, suspend, and return the yeild expression to the caller , or resume last call in generator function, until meeting second yield experssion. 

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
###generator function
* A function that returns an iterator. See ```yield``` part
### generator expression
* It has a similar format as list comprehension. but it uses `()` rather  than `[]`. 
* Compared with list comprehension, it may be a bit slower soemtimes, but it is memory efficient, becuase it does not have to create the full list.
* It returns an iterator
``` python
>>> listgen = (x for x in range(5))
>>> listgen.next()
0
>>> listgen.next()
1
>>> listgen.next()
2
>>> listgen.next()
3
>>> listgen.next()
4
>>> listgen.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>> 

```
[here](http://legacy.python.org/dev/peps/pep-0289/) for more

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
iter(<iterable object>) grants the magic Next() to iterable object

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
```python
def fun():
	str = 'spam'
	for s in str:
		yield s+s 

myitr = fun()

for i in myitr:
    print i  # it calls myitr.next implicitly 
```
```
print myitr.next()
print myitr.next()
print myitr.next()
print myitr.next()
print myitr.next()
```

## modules 
Modules could let us reuse python (or other language) code, create a top level namespace to avoid name confliction and write large software.
### inside import
* find the module file.
   * The searching path is defined in sys.path
   * starts from current directory
* compile source code into binaries (if necessaries)
* execute module code
   * so that module client could use the tools defined in the module
   

## Class
* Vs module
    * Class is similar to module, it has attribute and method. Class mothod is invoked by <class_name>.method(). The most obvious difference is that, class can create multiple instances,   but there is only one module instance.
* keyword ```class``` defines a class object.It looks like function object. While the returned object is an class instance
  ```python
  class ClassName: pass
  instance = ClassName()
  ```
* Class has named attribute that can be bind and reference 
   * Class attribute bind to function are named method.

* built-in method
   * ```__init__ ``` : constructor, call class object implicitly invoke this api.
   * ```__dict__```  : dict that holds all its attributes except special member with ```__<name>__```
   * ```__getitem__```: Used to capture index operation.  respond to ```for``` and ```<item> in <container>```  which looks like iterator
   * ```__iter__```: Capture iterator operation. The class should have a ```next()``` method, and throw ```StopIteration``` after the last element
See << Python in a NutShell>> for more
* Class Instance
   * each class instance inhert attribute from class object and has its own namespace
   * assignment of self attribute will generate  the attribute that belongs to the object itself. 
* C++区别
C++类和对象有着明确的区分，类是类，对象是对象。 类的属性在编译时确定 。 而python， 类定义后，也是一种类对象，本身的一些attribute和方法， 类的某一实例是类对象的派生对象。 当索引类对象的方法或属性，会依据搜索法则从上一层类对象，父类，祖宗类里面搜索


## Regular experession
### `re.sub`
```python
>>> a = "li yong qing  yong yuan"
>>> re.sub(r"(yong)", (r"_\1_"), a)
'li _yong_ qing  _yong_ yuan'

```
### Define c-ctyle struct
In C, we have ```struct```, what to do in python? Here it is: 
```python
class Elem : pass  # We don't have to declare attribute in class
elem = Elem()
elem.start = 0xa;
elem.end = 0xb; 
```
### directory walk 
``` python
rootDir = " "
for dirName, subdirList, fileList in os.walk(rootDir, topdown=False):
    for file in fileList:
        print dirName  + "/" + file
        
 ```
 
## Regular Expression
### re.sub
 Command Usage:
 
 ```python
 re.sub(pattern, repl, string, count=0, flags=0)
 ```

 repl is NOT always string, but can be a function 
 ```python
  ## Regular Expression
 ### re.sub
 Command Usage:
 
 ```python
 re.sub(pattern, repl, string, count=0, flags=0)
 ```
 

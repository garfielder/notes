## Advanced usage of List

### construct a new list based on existing one:

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

### Type basics

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
*  Reference is a pointer from variable to object.
 
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

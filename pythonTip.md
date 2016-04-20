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


convert from decimal to hex : ` hex(64)` , 
convert from string to number : `eval('100'), eval("0x40")`


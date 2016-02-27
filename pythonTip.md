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

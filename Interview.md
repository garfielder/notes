
## C++ 
### Will there be problem within following code:
```c++

class MyClass{
public:
    MyClass(){}

    void Print();

};

int main(){
    MyClass my;
    my.Print();
}
```
What if ```my.Print();```  is commentted out

### Translate C code into assembly language

```c
void fun(char a, int b)
{
    char aa = a;
    int bb  = b;
}

int main{
    char a = 'a';
    int b = 0xe;
    
    fun(a, b)
}
```

## Other 
### Copy Test in python
* Result of the following code
```python
class Node:
    def __init__(selfa):        pass
    def SetNode(self, data):    self.__data = data
    def GetNode(self):          return self.__data

n1 = Node()
n1.SetNode(10)

n2 = n1;
n2.SetNode(20)

print n1.GetNode()
print n2.GetNode()
```
How to make a deep copy: <br>

```python
#!/usr/bin/env  /tool/pandora64/.package/python-2.5.2/bin/python

import copy

class Node:
    def __init__(selfa):        pass
    def SetNode(self, data):    self.__data = data
    def GetNode(self):          return self.__data

n1 = Node()
n1.SetNode(10)

n2 = copy.copy(n1);
n2.SetNode(20)

print n1.GetNode()
print n2.GetNode()

```

### Make file 

We have 3 files to compile,

header.h
```
class MyClass{
public:
    MyClass();
    ...
};
```

header.cpp

```
#incldue "header.h"

MyClass::MyClass(){}

// Implementation of other methods
...
```

main.cpp
```
#include "header.h"

void main()
{
    MyClass myClass;
}
```

Please write the makefile: <br>
```
flag = -DGOOD_TAG -g --std=c++11
CC   = g++

out:    main.o header.o
        $(CC) -O $(flag) main.o header.o -o out

main.o: main.cpp
        $(CC) -O $(flag) -Wuninitialized -c main.cpp -o main.o

header.o: header.cpp  header.h
        $(CC) -O $(flag) -Wuninitialized  -c header.cpp -o header.o

clean:
        rm out *.o
```

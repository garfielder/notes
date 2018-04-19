
## C++ 
### C++ Misc
* What happens for a private desctructor 
    * can only be ```new```ed without free

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
### find function implementation

We always declear  a class header in a .h/.hpp file,  and define in a .cpp.  For a cpp file it looks like:

```c++
void MyClass::Fun1(){
    if (a > b) {...} else{...}
}

void MyClass::Fun2()
{
   // ....
}

// other members ....

```

Write a script to capture all function bodies between '{' and '}'

```python
fp = open(file_path, 'r')

content = fp.read(); 
fp.close()

bodies = []

stack = []
for idx in range(0, len(content)):
    ch = content[idx]
    if ch == '{':
        stack.append(idx)
    elif  ch == '}':
        if len(stack) == 1: # We got a function block
            bodies.append( (stack.pop(), idx) )
        elif (len(stack) == 0):
            raise Exception(" '}' does not match any '{'") 
        else:
            stack.pop()

for body in bodies:
    print "--------------------------------"
    for idx in range(body[0], body[1] + 1):
        sys.stdout.write(content[idx])
        
    print

```

## Memory in C
A process is  running when OS loaded an executable. What is in memory to stand for a process? <br>
Who initialized global data structure

```c++

class MyClass{
    MyClass(){printf("in contructor\n");}
};

MyClass myclass;
int main()
{
    printf("Hi in main\n");
}
```
### ```fflush```

### Template Usage
```c++
// in header.h
template<class T>
void PrintTypeInfo();


// In body.cpp
#include "header.h"
template<class T>
void PrintTypeInfo(){
   // print something relative to type T
}
```
   
 What's the problem with above implementation

### enum
Why we use enum in c++? <br> compare with string. 

If there is a type in enum variable, it is compile-error. If a typo in string, it will be a run-time error and hard to detect.!t

string cannot be use in a ```switch-case```scenario.

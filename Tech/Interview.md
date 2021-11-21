
## 总体衡量点

   * 基本工作能力
      * 工作风格（稳重，激进）
      * 表达能力（清晰，逻辑性）
      * 合作能力 
   * 语言能力
      * C
      * C++
      * Python
      * 脚本 
   * 算法与数据结构       
   * 计算机体系结构
      * 内存管理
      * 进程和线程管理
      * 处理器架构
         * 指令执行
      * 总线
   



## C++ 
### C++ basic
* Describe class constructor and types of constructors
   * copy constructor, default constructor, copy assignment operator
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

We always declare  a class header in a .h/.hpp file,  and define in a .cpp.  For a cpp file it looks like:

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

### Get number of tailing zeros

```c++
unsigned  tailing_zeros(unsigned  n)
{
	if (n == 0) return sizeof(unsigned) * 8;
	else {
		// log2( n & -n)
		return static_cast<unsigned>(log2(n & static_cast<unsigned>(-static_cast<int>(n))) );
	}
}
```

## Data structure

1. Merge two linked list 

```c
typedef stuct Node {
	int data;
	struct Node* next;
} Node;

Node* MergeSortedList(Node* link1, Node* link2)
```
## 编译原理
 * 堆和栈区别
 * 编译一个C/C++程序具体做了哪些事情

## 计算机体系结构
* 负数，浮点数的表达
* cache的原理
* 计算机进程调度，进程切换

## 图形学
* 着色基础
* 光照模型

## 多线程
Sington再多线程环境需要注意的事项

static is OK becaues it is only intanced by when firstly runnning 


两个线程对一个变量操作， 最小值和最大值分别是多少


## 工作能力
   * 理解 - 需求分析
      * 获取需求
      * 沟通需求
   * 评估 - 可行性研究
      * 衡量难度
      * 可行性
      * 做的理由，不做的理由
   * 执行
      * 克服困难
   * 改进
      * 流程



*其他考虑点* <br>
   * 判断Candidate 真正做了哪些事情
   * 主要精力花在了什么上

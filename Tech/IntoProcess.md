# Into Process


## What is 
* A program running in execution.
* Monitor Program layout in a program
  Main data structure for a process 
\<TODO: adding the impage\> figure 3.1  of [[1]](#system)

  For memory layout, [reference 2 ]( #ref2) is also a good example. It answers why user main function is not starting from, that is due to [cr0.o](https://en.wikipedia.org/wiki/Crt0),  one important thing for cr0.o does is to initialize global data. 
<br>
Notice virutual address range are only 48bit lenght even for a x64 platform. That's becaus 48 bit is already large enough. 
```
db) print &d
$5 = 0x7fffffffda63 "b\016"
```

```/proc/<proc_id>/maps ``` give a good example of memory layout of a process

## Thread 
###  Green Thread 
Some language provided API to create green thread, they are run in user mode, created and scheduled by language or library runtime.  OS is not aware of the existance of them.  such as sc_spawn in systemC library or Thread object in Java. <br>

Take Java threads for example, there may many Java thread running cocurently, but it is JVM rather than OS manages and scheduls them, so there are still only one Java thread running in OS. 

Green threads cannot utilize multi-core, it always runs on the same Core in a single OS thread

## Reference 

<a name='system'> 1. Avi Silberschatz.  Operating System Concepts.  Wiley publishing,  Ninth Edition, 2013.  </a> <br>
<a name='ref2'>   2. http://www.cnblogs.com/01picker/p/4449322.html  </a>

# Into Process


## What is 
* A program running in execution.
* Monitor Program layout in a program
  Main data structure for a process  <br>

\<TODO: adding the impage\> figure 3.1  of [[1]](#system)

  For memory layout, [reference 2 ]( #ref2) is also a good example. It answers why user main function is not starting from, that is due to [cr0.o](https://en.wikipedia.org/wiki/Crt0),  one important thing for cr0.o does is to initialize global data. 
<br>
Notice virutual address range are only 48bit lenght even for a x64 platform. That's becaus 48 bit is already large enough. 
```
db) print &d
$5 = 0x7fffffffda63 "b\016"
```

*/proc/<proc_id>/maps* give a good example of memory layout of a process
```
richli-VirtualBox:/proc/2210> cat maps
00400000-00401000 r-xp 00000000 08:01 429891                             /home/richli/studio/cpp/a.out
00600000-00601000 r--p 00000000 08:01 429891                             /home/richli/studio/cpp/a.out
00601000-00602000 rw-p 00001000 08:01 429891                             /home/richli/studio/cpp/a.out
7fdf08f10000-7fdf090cb000 r-xp 00000000 08:01 922370                     /lib/x86_64-linux-gnu/libc-2.19.so
7fdf090cb000-7fdf092ca000 ---p 001bb000 08:01 922370                     /lib/x86_64-linux-gnu/libc-2.19.so
7fdf092ca000-7fdf092ce000 r--p 001ba000 08:01 922370                     /lib/x86_64-linux-gnu/libc-2.19.so
7fdf092ce000-7fdf092d0000 rw-p 001be000 08:01 922370                     /lib/x86_64-linux-gnu/libc-2.19.so
7fdf092d0000-7fdf092d5000 rw-p 00000000 00:00 0 
7fdf092d8000-7fdf092fb000 r-xp 00000000 08:01 922346                     /lib/x86_64-linux-gnu/ld-2.19.so
7fdf094fa000-7fdf094fb000 r--p 00022000 08:01 922346                     /lib/x86_64-linux-gnu/ld-2.19.so
7fdf094fb000-7fdf094fc000 rw-p 00023000 08:01 922346                     /lib/x86_64-linux-gnu/ld-2.19.so
7fdf094fc000-7fdf094fd000 rw-p 00000000 00:00 0 
7fdf094ff000-7fdf09504000 rw-p 00000000 00:00 0 
7fff320e1000-7fff32102000 rw-p 00000000 00:00 0                          [stack]
7fff32108000-7fff3210a000 r--p 00000000 00:00 0                          [vvar]
7fff3210a000-7fff3210c000 r-xp 00000000 00:00 0                          [vdso]
ffffffffff600000-ffffffffff601000 r-xp 00000000 00:00 0                  [vsyscall]

```
Notice, *vdso* provides mechansim to accelerate execuration of certains system call. Kernel maps some kernel routines (gettimeofday) into user space,  all such user pages are mapped into the same kernel physical page.  With it, there is no expensive system call and context switch between user process and kernel. 

(https://lwn.net/Articles/446528/) gives a more details about vDSO.
### /process
proc - process information pseudo-file system

(http://linux.die.net/man/5/proc)

### Context Switch and system call


## Programming  Process
### System Call 
Be used to request access to the resource of the machine , communicate with other running programs, and to start new process. 

Categories:<br>
*  Memory management
  * mmap()
* Time management 
  * time()
* File system
  * open/read/write/close
* Process
  * fork/exec
* other 


### Basic Programming
### Process communication
### atomic 

## Thread 
###  Green Thread 
Some language provided API to create green thread, they are run in user mode, created and scheduled by language or library runtime.  OS is not aware of the existance of them.  such as sc_spawn in systemC library or Thread object in Java. <br>

Take Java threads for example, there may many Java thread running cocurently, but it is JVM rather than OS manages and scheduls them, so there are still only one Java thread running in OS. 

Green threads cannot utilize multi-core, it always runs on the same Core in a single OS thread

### Multi-Thread in C++11

## Reference 

<a name='system'> 1. Avi Silberschatz.  Operating System Concepts.  Wiley publishing,  Ninth Edition, 2013.  </a> <br>
<a name='ref2'>   2. http://www.cnblogs.com/01picker/p/4449322.html  </a>

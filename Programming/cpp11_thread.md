#CPP11  Cocurrent Programming

## Concurency Concept
  Name          | DESC		
  ------------- | -------------
  volatile      | Tell compiler not to optmize it
 lock-free      | Simply speaking, no mutex or lock. More precisly, one thread does not block each other. See [here](http://preshing.com/20120612/an-introduction-to-lock-free-programming/) for more

## Basic Sample
Will link to my sanity test after checked into github

## Atomic and  Memory model 

For atomic concept, See https://github.com/garfielder/notes/blob/master/Tech/TechDoc.md#synchronization
Atomic operation relies on hardware support to avoid data race small data. It is an way for lock-free programming.  Accessing atomic variable introduce inter-thread synchronzation  and order non-atomic memory access.  While **How to order** them are defined by std::memory_order.    **order** may from compiler reordering or OS scheduling. 

Fore more, **FIXME** 

http://en.cppreference.com/w/cpp/atomic/memory_order

## Key words 

**Waittinf for event**

  Name          | DESC		
  ------------- | -------------
  unique_lock(mutex)  | a wrapper of lock, or similar to a unique_ptr applied to a mutex, mutex.lock() is called in constructor and mutext.unlock is call in destructor
 condition_variable::wait(unique_lock)   | Waiting for a event, release the lock while waiting,  if notified, re-acquire the lock
 condition_varible::notify()| Notify above wait action
 
 
 **this_thread**
 
  Name          | DESC		
  ------------- | -------------
  yield   |  give OS a hint to reschedule execution of threads, allow other thread to run

 
 
## How to return a future value

### primise

### packaged_task
Similar to a std::function object, I can be called like a  function. The difference is that, packaged_task could return a asynchronous result. 
But funciton object cannot. 
### async

It can submit a callable object aynchronously. notice, do not submit a packaged task in aync. because async created a packaged_task internally. 

## Cocurrency 

Within processes:  communication between processes are expensive/slow/complex. Starting a process is of overhead. But provided good data protection. Diffent process can communcates through network.

Within threads: lite process , but be careful for data shares. 

People uses cocurrency for separation of concerns(separation of independent functions)  and performance ( on a multiple core system)



## TODO
What is inside mutex/condition_variable in c++11, compared with pthread

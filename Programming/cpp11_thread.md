#CPP11  Cocurrent Programming

## Concurency Concept
  Name          | DESC		
  ------------- | -------------
  volatile      | Tell compiler not to optmize it
 lock-free      | Simply speaking, no mutex or lock. More precisly, one thread does not block each other. See [here](http://preshing.com/20120612/an-introduction-to-lock-free-programming/) for more

## Basic Sample
Will link to my sanity test after checked into github

## Memory model 
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

difference of them 



## TODO
What is inside mutex/condition_variable in c++11, compared with pthread

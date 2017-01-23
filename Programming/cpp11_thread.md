#CPP11  Cocurrent Programming

## Basic Sample
Will link to my sanity test after checked into github

## Memory model 
## Key words 

### Waittinf for event
  Name          | DESC		
  ------------- | -------------
  unique_lock(mutex)  | a wrapper of lock, or similar to a unique_ptr applied to a mutex, mutex.lock() is called in constructor and mutext.unlock is call in destructor
 condition_variable::wait(unique_lock)   | Waiting for a event, release the lock while waiting,  if notified, re-acquire the lock
 condition_varible::notify()| Notify above wait action
 
## How to return a future value

primise

packaged_task

async

difference of them 



## TODO
What is inside mutex/condition_variable in c++11, compared with pthread

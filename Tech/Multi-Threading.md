# Multi-Threading Notes

## Thread mangemet

```c++
void fun()  { cout << 1 << endl; }

std::thread my_thread(fun); // start a thread 

// my_thread will be terminated when my_stread is destructed, unless my_thread.detach is called.
```

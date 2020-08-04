# C++17 Notes
* Write compact and concise code

##  Structured Binding

We can multiple returned from an expression in pythons:

```python
def fun():
   return ("hello", "Odie")

a, b = fun();
```
Now, we can also do this with C++17.

```c++
std::pair a(1, 1.2f); // audo 
audo [x, y] = a;
```

The returned value can come from tuple/arry/struct

## Links
   * https://www.cppindetail.com/data/cpp17indetail-sample.pdf

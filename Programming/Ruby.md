# Ruby Tips

## different variables 

  Name     |prefix     | DESC		
  ---------|---------- | -------------
  Local variable | None      | Local variable 
 Instance variable |  @var_name | c++ class member
 class variable | @@var_name| c++ static class member
 global variable |$var_name| c++ global variable 



## Block

It is similar to c++ callback function or function oject, and can be called from another function.
The callable block can be invoked by yield. 

A significant point is the function object name should be same with caller functionxxx

```ruby
def myfun
    puts "Now calling function block:"
    yield
end

myfun {puts "LYQ in block"}
```

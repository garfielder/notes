# C++11 New features 

C++11 introduced a few grammar suggars that helps programmer to write less code, such as ```auto```,  ```decel``` . It brings features from mordern languages such as lamda function. It includes more tr1 library as its stardard library. 

## auto
With auto, we don't have to indicate a type explictly because it can be deduced on the right of '=' operator.  So ```for (std::vector<int>::conster itr = vec.begin(); ...```, can be saved as ``` for (auto itr = vec.begin(); ...) ```

#GDB TIPS

## Define customized command 

The following GDB command defines a customized command named *nf* which is combination of ```next``` and ```frame 0```
(gdb) define nf
Redefine command "nf"? (y or n) y
Type commands for definition of "nf".
End with a line saying just "end".
>next
>frame 0
>end

``` 

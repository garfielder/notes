# GVIM
## replacement

```tcsh
:%s/src_string/dst_string/g  # '/' is used as delimiter 
:%s#src_string#dst_string/g  # '#' is used as delimiter 
```

## line wrap
```
set nowrap # disable line wrap
set wrap   # enable line wrap
```
## non-greedy search 

Instread of using 
```
/.*
```
using 
```
/.\{-}
```

## Move 

3l  : move to 3th colomn of current line <br>
fX  : move to next X

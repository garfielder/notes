# GVIM

##  Search for non-ascii character in vim

```[^\x00-\x7f]```

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

## view and edit binary
1. Open file in binary mode 
```vim -b bin_file```
2. convert the file to hex foramt
```   :%!xxd ```
3. Convert it back to binary
```%!xxd -r```

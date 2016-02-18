# Ubuntu Tips

## Install Ubuntu

## Compile Kernel

## Useful APP
### Chinese Input
### Flash plugin
    http://www.linuxidc.com/Linux/2014-04/100490.htm

## git vs perforce
###  Artichicture 
 - Git is distributed version control system while perforce is central version control systtem
 - See http://blog.csdn.net/garfish/article/details/46939383

### Command Vs Command

|Function             | perforce |  git       | comments|
|---------------------|----------|------------|----------|
| Check out worksapce | p4 sync  |  git clone <depot_link> |  Perforce needs P4CLIENT & P4PORT   |
| Add a file          | p4 add   | git add||
| update workspace |  p4 sync | git pull |  git would update both local repo and work copy|
| update a file or files | p4 sync file/files| no single command | |
|edit a file | p4 edit file/files | git comment -a -m "message" | git detectes modified files |

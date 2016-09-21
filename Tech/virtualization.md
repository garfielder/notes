# Virtualization
## Software-Supported virtualization
### 2D pagetable 
### shadow page table
http://ju.outofmemory.cn/entry/127173
There are three kinds of  mapping in virtulized system.

1. guest virutal address --> guest physical address   # guest page table 
2. guest physical address --> system phsycial address # pmap page table
3. guest virtual address --> system physical pagetable # shadow pagetable
 
3 is a merge of 1 and 2, it is really written into CR3 ( CR3 defines the starting point for page table for page directory walk). 
Guest pagetable and pmap are changing, shdows page pagetable should be changed consequently to reflect this. 


## Links 
http://www.sersc.org/journals/IJSEIA/vol10_no3_2016/1.pdf
http://cs.rochester.edu/~sandhya/csc256/seminars/hedayati_vm_npt.pdf
http://www.mulix.org/lectures/turtles/turtles-dc9723.pdf
http://www.vmware.com/pdf/virtualization_considerations.pdf

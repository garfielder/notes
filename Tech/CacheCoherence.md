# Cache Coherency
## Concept 
Concept from  计算机体系结构量化的研究方法
Cache coherence ensures that multiple processor see a consistent view of memory. <Br>
There are different discriplines for cache coherence. The strict it is, the more performance penaltiy there is: < br>
* Every write operation appears to occur instantaneously
* All processors sees the same sequence of changes of value for each separated oprand

##  Formal defination
X: An address in main memory  <br>
P1: Processor 1 <br>
P2: Processor 2 <br>
-> : then  
* P1 write int X ->  P1 read from X    ;  P1 read return P1 write
* P1 write into X -> P2 read from  X    ; P2 read return P1 write 
* P1 write A into X -> P2 write  B into X   ; Address is seen with A then with B

##  Solution to memory incoherency
### Simple sulutions 
* No Cache 
   * Yes, really simple, but ...
* Do not cache shared data
   * Low performance if too many shared data. 
   * Memory can be caterigoried as different types 
* Software flush at stategic time
   * Useful when sync operation is not too frequenct
* Hardware cache coherence 
   * see next
   
### Hardware cache coherence 
Use hardware to solve incoherence 
*  Snoop protocal (bus-based)
   * Write invalidation. See  setction 17.3 of  [ref3](#ref3). Common is comercial computer system. 
   * Write broadcast. typical is write through. Each in algorighm. but heavy bus load.  no read miss
* directory protocal 
   * centralized controller that is part of meory controlle
   *  peer-to-peer cache communication, good for system with larger processor numbers.
   


## Reference 

<a name=ref1> 1. Computer Architecture. A quantitative Approach. 4ed </a>
<a name=ref2> 2. 浙江大学《计算机体系结构课件》 </a>
<a name=ref3> 3. Computer origanization and architecture 9ed. </a>

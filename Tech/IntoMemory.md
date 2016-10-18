# Looking Into Memory 

When talking about memory, people may think of DDR, GDDR, Memory, Chips, or some  picture below. 

However, there are much more story inside memory. Let's start from the very beginning

## Semiconductor 
What makes the conductivity of a material? It is the atrribute of the  [valence electron](https://en.wikipedia.org/wiki/Valence_electron#Electrical_conductivity).  For metal, it has fewer valence electrons compared with non-metal,  in solid state, it is relatively free to leave one atom in order to associate with another one nearby, so we have 'free electrons in metal, and thus make metal conductive 

For insulator, it's [ionization energy] ( https://en.wikipedia.org/wiki/Ionization_energy) is high, the electrons cannot easily leave the atom even when electric field is applied. 

For semiconductor such as silcon and germanium,  they have single crystal structure. Their conductivity is between metal and nonmeta ( resulator).  Such a aotm has four valance elctrons shared with its neighbours, so it is relatively stable at room tempature, when temprature,  its valance electrons get more energy so that it easily escap from where it belongs. 




## Diode and JFET
Magical things happen when introducing impurites into above crysital structure. There are N-type and P-type semiconductors.  Just as the names suggests,  N-type has more valance electrons while P types with more holes.
(see chapter 1 of <<electronic devices and circuit theory>>　by Roylestad and Nahelshy)

A Diode is a juction of n-type and p-type  secmiconductor.  

![P-N junction ](https://upload.wikimedia.org/wikipedia/commons/d/d6/Pn-junction-equilibrium.png)
(https://en.wikipedia.org/wiki/P%E2%80%93n_junction)

In the space charge region,  there is an internal e-field , if the external e-field is of the same direction, it makes the slice thicker, thus current is blocked.  Other wise, it makes current flows through the junction. 

Jnction gate  field-effect  transistor(JEFT)  is a three-terminal semiconductor devices that can be used as electronically-controled switches, amplifiers, or voltage-controlled resistors. 


See here for how it works:

(http://www.learnabout-electronics.org/fet_03.php)

By controlling the Vgs, we can control the conductivity between source and drain. 

MOS transistor is another kinds of FED (field-effect transistor) other than JFET.  There are NMOS and PMOS. See the link below for more: 

(http://wenku.baidu.com/view/b029704325c52cc58bd6be7a.html?re=view)

CMOS is a *process technology* that contains both CMos and NMos transisor . It is not a name for a specific kind of transistor. 

## SRAM and DRAM

Both SRAM and DRAM are semiconductor storage. The minum storage unit is a CMOS transistor, also named memory  bit, several bits  consist a memory  unit. Data will be lost after powerdown. 

### SRAM
A typical SRAM cell is made up of size CMOSFET cell, each bit is stored on the four tansistors (T1-T4). ([link](https://en.wikipedia.org/wiki/Static_random-access_memory)
Here is the handwirting diagram:

* T1/T2: Store 1/0
* T3/T4: Behaviors as resistors to avoid shorcut between VCC and A/B
* T5/t6/T7/T8: Select this cell
* I/O:     Read or Write

### DRAM
To increase transisor density in a chip, people removed T3/T4 , and it because four-transistor RAM. To hold the data, two capacitances are introduced between gate port of T1/T2 and ground. 

There is no VCC to recharge the dram shell through T3/T4 as SRAM cell,  so external logic is required to recharge DRAM periodically. 


## Memory Extension
Size of  memory chip is limited, but we can construct a 8K X 8  memory based on  eight 8K X 1 meomry chip to extent bits in a word, or we can construct a 64K X 8 memory based sixteen 8K X 8 memory chip. 
Two image

## Memory system orgination 
![Memory system orgination](http://cdn3.techbang.com.tw/system/images/164318/original/8f04a1f57fe07692327b9269ba484ce4.jpg?1401354086)
(http://www.techbang.com/posts/18381-from-the-channel-to-address-computer-main-memory-structures-to-understand)

## Interleaved Memory Access

(http://accel.cs.vt.edu/files/lecture11.pdf)
(http://accel.cs.vt.edu/files/lecture12.pdf)

Bank is the logical unit that can be accessed cocurrently. 

When GPU is doing compute or graphic work.   A number of threads from the same thread group can be executing simtenouly. For the best memory effiency, all threads are access different banks at the same time. All those memory access can be bound into one memory access which named coalescing access. (page 50 of <跨平台的多核与众核编程讲义>)


## Cache 

Memory is import in computer system. It is measure in three ways(better word), including : a) capicity  a) dollor per bit b) access  speed. People are greedy, they want large capicity, fast access time and low price, but a single storage could not meet the requirement, so memory hierachy is introduced 

![Memory hierarchy](http://wiki.expertiza.ncsu.edu/images/archive/4/43/20100223023710%21Memchart.jpg)

As one goes down the hierachy,  frequency of the memory access from processor does down.   Principle here is *locality of reference*. During an execuation of a program,  memory reference by process, tend to cluster. 

### Element to clarify difference arhitectures [section 4.3 of book 1 ](#book1)
* Caches address 
  *  Logical Cache: store data using virutal adderss.  But same virutal address in diffeernt  VM contexts are mappped to different physcal location. So, context switching requires invalidations 
  * Phycial cache.
* Cache size
  *  tradoff. The small the faster. 
* Mapping function. 
   * fully associative. Each memory block can be mapped into any cache line. 
      * Low missing rate.  but complex control logic. Only available for small cache
   * direct assiciative. Each meory block is mapped into a specific cache line. Easy to implement, but high missing rate. 
   * set associate. Cache lines are divided into different sets, each sets contains 2/4/16/32/64 lines(or cache blocks), although each memory block can be mapped in a single block, but  hit rate is still high, bacause there are a number of  candicated lines for the memory block 
      * A set with N lines are named N-way cache
  

## Reference 
<a name=book1>1. compute Organization and Architecture 9ed. Willam Stallings. </a>

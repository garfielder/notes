# Windows Display Driver Model Architure
## Architure
![WDDM](https://msdn.microsoft.com/dynimg/IC504961.png)

* Direct3D Runtime
   * You can find and install on computer. 
   * Provide library and headers to write D3D-based applications
   * In the same level with Win32GDI and OpenGL runntime
* OpenGL runntime
  * provide libarary to write openGL-based  applications
* Directx graphic kernel subsystem 
  *  Provide interface that support Direct3D Runtime upward
  * Call into Display miniport driver for furhter process
  *  Relies on Video memory manager to mange memory
* Video memmory manager 
  * It mamanges GPU memory management unit and underlying pagetable 
  * It provides interface to allow user mode driver map GPU Virtual Address to allocation (physcial address) 
## IoMmu Model
  ![HSA](https://msdn.microsoft.com/Dn894176.iommu_model.1(en-us,VS.85).png)
It describes how CPU and GPU shares memory



# OpenCL 
## Models
What is platform : The host plus a collection of devices
### Platform models
* One host, the big boss that controls every thing. 
* A number of compute devices, it can be a GPU or a multi-core GPU, or somethign else
* There are CUs in different Devices, CU is composed of PE
* I think low level drier could report all devices and CU information

![platform module](http://www.rastergrid.com/blog/wp-content/uploads/2010/11/opencl_platform_model.png)

### Executation Model
* Kernel Program that execute on host that controls everything. The ```main``` function  in source code. 
* Kernels that executes on one or more devices.
   * work-item: one kernel instance has global Instance Id. will be process by one kernel on one PE. One workitem process one elements in the NDRange. 
   * NDRange defines the input space, it could be N dimentional tupple (n = 1,2,3)
   * Workgroup : a group of workitems. workitems in a group runs concrurently  on the same CUs and shares same local memory. 
* A few concept
   * A context, stands for one application, has its own command queues, available devices, kernels , memorys , program objects
   * Kernel: Functions to run on compute devices
   * Program objects: program source and executable that implement the kernels
   * command queue: attached to a device, that is used to queue a set of operations. 



[doc] : https://www.khronos.org/assets/uploads/developers/library/2012-pan-pacific-road-show-June/OpenCL-Details-Taiwan_June-2012.pdf
### Event
Event is an operation. It could depends on other event list, it will also block other event to proceed. The event can push into the command queue. 

## Some API
#  Parallel Computing
CUDA stands for Computer Unified Device Architecture。
http://www.nvidia.cn/content/PDF/fermi_white_papers/P.Glaskowsky_NVIDIA's_Fermi-The_First_Complete_GPU_Architecture.pdf


One workgroup is running one streaming multiple processor(SM). Each SM contains 32 CUDA core. It has one FP unit and one Float unit.

[Good Link for AMD GPU involvment](http://www.expreview.com/17961-all.html)


# Compute Architecture notes (From ZJU CS PPT)

## Term
* *response time* :   The tiem between start and the completion of an event.
* *executaion time* : as refer to as response time
* *throughput* :     The total amount of work in a given time. In a pipeline case, it is the items exiting the pipeline per unit time
* *latency* :        Time between issuing and completing the instruction


## CISC and RISC 
reference : (http://cs.stanford.edu/people/eroberts/courses/soco/projects/risc/risccisc/)

Number of instructions per-program  Vs number of clocks per-instruction. 

### CISC
* A primary goal of CISC is to complete a task in as  few lines of assembly as  possible. 
* It is good for compiler, because hardware does complex work. 
* The hardware could do a serial of operations in one instruction

### RISC 
* Separating "LOAD" and "STORE", they are indenpendent instructions
* CPI is almost to 1. 
* Hardcode line instread of micro code.
* instruction formats number is small
* Easy to to schedule on pipeline
* Can easily be optimized by pipeline

## Pipeline
*A technique that allows to start an instruction before completing another one*
* It has many stages, each stage carries out a different part ofinstruction or operation, which cooperats at a synchronized clock, are connected to form a pipe
* An implementation technique to exploits parallesim among instructions in a sequential stream

### Hazard (what makes pipelining hard to implement)

Type of hazard<br>

* structrual hazard
  * hardware functional unit cannot support simultaneous access
* data hazard
  * an instruction depends on the result of previous instruction which is not ready yet
* control hazard
  * arise whiling pipling of branches or other instructions that change PC

Fix for hazard: <br>
* data hazard
  * Simple way is to stall
    * Need hardware logic to check data hazard
  * forward
    * Reduce data stall
    * Instread of wait for result in memory, we forward it imediately  to the instruction that wants it
* Structural hazard
  * Structural hazard can be overcome by replicating hardware resource
    * Multiple access to registers/memory
* control hazard
  * simple way: holding or deleting any instruction after branch until the branch destination is known
    * flushing until branch is resolved
  * predict not taken
    * penalty is , when we are wrong, we have to restart fetching branch targe and turned fetched instruction as NOP
    * compiler can code the frequent case in the untaken case

## ILP -- Instruction-Level-Parallelism
* Basic block ILP is quite small, there are likely to be branches in a programs. So, loop-level parallalism can be exploited
* Expand the loop and schedule the instruction according to dependencies between instructions

###　Dependency and Hazard
* Dependency
  * RAW : true dependency 
  * WAW: output dependency 
  * WAR: anti-dependency 
* Dependency is a potential hazard, it sets up an upper bound of how parallism can possibly be exploited
* Program order
  * determined by source program order
  * perserve the program order where it affets the outcome of the program

### Overcome data hazard with dynamical scheduling
Enable out-of-order execution and out of order completion.  <br>
*Score board* is used for dynamical scheduling <br>
*Tomasulo* algorithm 

## synchronization

### Atomic Operation 
 see section 6.15 of PCI_Express_Base_r3.0***.pdf
* Ready and modify memory unit atomically 
* We knows wehter we really did atomic operation (executation feedback)
* Atomic operation in PCIE spec
  * AtinucIo acoabukuues are optional normative
  * Endpoint and Root port are permitted to implement AtomicOp Requester capabilites
  * PCIE Express Function wiht Memory BARs  are premitted to implent AtomiticOp compelter capbilities arearchitectured for device-to-host, device-to-device, and host-to-devices.
  * If hte completer of an AtomicOp enounter an uncorrectable error access target location or carrying out the atomic operation, the completer must handle it as a completer error(CA). 
* classic atomic operations
  * atomic exchange
    * Can be used to lock something 
    ```asm
        // Spin lock
        // The lock variable can be cached for performance 
        ADDUI R2, R0, #1
lockit: EXCH R2, 0(R1)
        BNEZ R0, lockit
    ```
  * test and set
  * fetch and increasment
  * Load linked/Stcore conidtional 
    * use a linked registers to store the memory adderss
    * once interrupt or write invalidate against that address detected, clear the address
    * SC just check the adderss in linked reigsters to see whehter matched. 
* One rule for atomic operation
  * At any time, there is only one processor that can take the bus (or lock the bus)
  * Gain perforce by caching  lock variable and reduce write invalidate
* Coherence Requirement 
  * WW/RR/WR/WR (https://github.com/garfielder/notes/blob/master/Tech/TechDoc.md#synchronization)
  
## System Design Tips
* Mechanism
  * How to do something
  * The system could provide all interfaces to do all kinds of works, delivered together with a lot of parameters to control what will be done  
* Policy 
  * What will be done
  
Separation of Mechanism is important for flexibility. Policies are likely to changeover time. A good design to make mechanism insentive to policies change.
  
## Virtual Memory 
   * How to customize page attribute
      * PAT and MTRR

## Reference 
1. Avi Silberschatz. Operating System Concepts. Wiley publishing, Ninth Edition, 2013. 


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


# Compiling and linking
## Compile and Link
*Compiling* :   <br>

Compiler converts C/C++ source into machine code, named ".o" or ".obj".   For each c++ source code file,  compiler compiles it into an object file.  The object file is not a executable. 

The compiler does not look at more than one file at a time.  If it couldn't find a funciton defination in current file, it asusmes it in another. 


*Linking*: <br>
Linker converts the object files and pre-compiled libraries  into  a single executable  that can run on machine.  The linker would  try to to find all the definations that was mentioned. 

*benifits of the separation*<br
1. Reduce the complexity. Devide the work into two parts
2. make conditional compilation possible, so that one file changed, we don't have to recompile all of the other files
2. reuse other precompiled libraries 
## Symbol and relocation table
### Memory layout of an obj file
The following segment is stored in the object file itself
* text segmant 
* data segmant 
The following segment is generated dynamically
* Heap 
* stack 

### symbol table 
symbols in data segment uses relative addess inside the segment, the symbol table keeps track of the list of the symbols 

### relocation table 
keeps track of subset of instructions.

###  relocation 

for data and code segments, when the linker tries to link two or more object files together, it should be able to merge the text and data segment, and resovle the symbols (replace symbols with absolute address)

https://stevenschmatz.gitbooks.io/eecs-370/Lecture_Notes/lecture_7.html
https://en.wikipedia.org/wiki/Symbol_table


## Links 
1. http://www.cprogramming.com/compilingandlinking.html
2. 

# Others 
## Virtual Memory 
   * How to customize page attribute
      * PAT and MTRR
      
## NUMA
Uniformed memory access

http://developer.amd.com/wordpress/media/2012/10/LibNUMA-WP-fv1.pdf

## Reference 
1. Avi Silberschatz. Operating System Concepts. Wiley publishing, Ninth Edition, 2013. 


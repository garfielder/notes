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

# OpenGL Notes

## Useful links 


## Texture
|Name | Explain|
|------|-|
|filter| Determine texture color for a textured mapped pixel, options are nearst neighour/bileaner/Anisotropic|
|sample| |

## APIs

*glGen*
```void glGenBuffers(GLsizei n, GLuint *buffers);```
```void glGenTexture(GLsizei n, GLuint *buffers);```

They just allocate unused name in forms of integers, not really allocate resource 

*glBind*
```void glBindBuffer(GLenum target, GLuint buffer);```
Buffer is the name created by ```glGenBuffer```

really allocate memory at this step. 


### Download glut library

(https://sourceforge.net/projects/freeglut/?source=typ_redirect)

Tips of how to use it:

(https://ins.nafsadh.com/2009/09/07/opengl-and-glut-in-c-with-ms-visual-studio-2008-msvs9/



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


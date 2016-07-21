# Windows Display Driver Model Architure
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
  

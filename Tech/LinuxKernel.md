# Linux Kernel 
## Plan 
   * PCIE Driver part
   * Virtual-Physical translation part
   * Bootup
   * Think the art in Linux kernel design/coding style
   * Android source 
   
## Purpose 
   * Business

   * Career
      * System Design skill
      * Spot light for furhter job
      * Good oppernity to gain Android Knowledge
      
      
## PCIE Driver
* mydriver_init * <br>

Called when driver is installed.  Register ```pci_driver``` by ```pci_register_driver```

Register driver means, when Linux detects the devices in my list, please leave it to me, I will handle it by mydriver_probe function.


* mydriver_probe*
Create data structure for current device. :A
regsiter the char driver, 


*pci_enable_device* <break>
wakes up the device and enable access to it. 


*device_create* 

create a /dev/mydriver* node, so that we can open and access it in user space 


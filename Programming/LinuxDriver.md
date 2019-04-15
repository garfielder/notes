# Linux Driver Programming Notes

## mmap
unlike ioctrl, mmap reply on system to do most of the work, while device kernel driver needs to fill vma.  <br>

VMA actuall defines a memory range that has the same attribute, also called fragment, a memory object. 

S32K344 Boot/IVT Header
====
* Raw binary image starts with BOOT HEADER 
* BOOT HEADER
  * Word1 = IVT Marker  -> 0x5AA55AA5
  * Word2 = Boot Config Word
  * Word3 = Resreved
  * Word4 = START ADDRESS = __CORE0_VTOR
  This is defined in Linker file 



![image](https://github.com/user-attachments/assets/bd2fcffa-837e-4d35-8b2e-8d121ca5d8f1)

![image](https://github.com/user-attachments/assets/1906796c-d2d6-4698-9539-9f91bdea48be)


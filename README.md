USB Mouse Driver for linux which adjusts brightness on left and right clicks.

Using the device driver file :

  After downloading the project, run make
  This will create a .ko file which we will use to load the device driver

1. You need to register a device with a major number (same as in device driver code ) and minor number.
  <code>sudo mknod /dev/myDev c 91 1 </code>
  

2. Now remove the default usb driver (usbhid)
  <code>sudo rmmod usbhid</code>
  
3. Now your usb mouse should stop working. Now load our device driver.
  <code>sudo insmod usbmouse.ko</code>

4. Check whether clicks are working.
  you can do <code>dmesg | tail after</code>  after pressing left click and right click to check if clicks are     getting registered.

5. compile adjustBrightness_exiting.c
  <code>gcc adjustBrightness_exiting.c </code>
  This file basically reads from /dev/myDev and adjusts brightness. 

6. Now run the compiled file
  <code>sudo ./a.out</code> 
  on pressing left and right clicks, the brightness should change. (note the brightness file and values can be different for different machines. On mine the brightness varies from 0 - 10 and the file is /sys/class/backlight/acpi_video0/brightness.) middle click exits the program.
  
7. Removing our driver 
  <code>sudo rmmod usbmouse </code>

8. Loading default usb driver back
  <code>sudo modprobe usbhid</code>

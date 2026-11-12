# kntrl-dos-drv
A DOS Driver and TSR able to communicate to a server PC via serial port (the switches are implemented but i didn't had a chance to implement the Parallel Port code because i didn't had one).

**It can**
* **emulate keyboard and mouse, extract the video-memory** 
* **mount folders** located on the server PC (using the MS-DOS Installable File System interface, IFS/Redirector)
* **mount virtual disk/diskette images** as device block drivers located on the server PC
* **handle data transfers** between client and server PC
* **debugging** step, breakpoints, download arbritary memory space, upload and run arbitrary code at a location, perform I/O commands
* i don't provide the other-end PC Application that serves the driver, as it was left in oblivion without maintance. So this is just the driver code, and needs an app that would establish a serial port connection and send/receive the appropriate packets. My choice for the debugger implementation was the Capstone library.

**Description**
The driver is initialized in CONFIG.SYS with these optional args:
* **-D** install debugger
* **-XT** | **-AT** ibm pc compatible type
* **-I** transfer always the control to the server application for debugging
* **-DH=x** sets the debugger hotkey as function key x (local debugging)
* **-IH=x** sets the debugger hotkey as function key x (debugging on the server app)
* **-P=COMx,BAUDRATE** | **LPTx** sets the port to LPTx or COMx with the settings
* **-S=x** creates x block device slots



# kntrl-dos-drv (2019)
A DOS Driver or TSR + a Utility, able to communicate to a server PC application via serial port (i didn't had a chance to implement the Parallel Port code because i didn't had one at the time). 

**It can**
* **emulate keyboard and mouse on a remote computer, change mouse cursors, extract the video-memory, etc** 
* **mount folders** located on the server PC (using the MS-DOS Installable File System, IFS/Redirector interface)
* **mount virtual disk/diskette images** as device block drivers located on the server PC
* **handle data transfers** between client and server PC
* **debugging** step, breakpoints, download arbritary memory space, upload and run arbitrary code at a location, perform I/O commands
* i don't provide the other-end PC Application that serves the driver/TSR, as it was left in oblivion without maintenance. So this is just the driver code, and needs an app that would establish a serial port connection and send/receive the appropriate packets. My choice for the debugger implementation was the Capstone library.

**Windows 95**

 This is a real mode driver for older computers running MS-ODS, and despite it works in Windows 95,  "Windows will warning you that its use can hit the computer performance".

**Description**

The solution is 1) DOS Driver + 2) a Utility + 3) TSR. It can used as 1+2 combo, or 2+3 combo. If the driver isn't installed (the 2+3 combo) then block device drivers aren't possible. All other commands, transfer files, mount folders and debugger are possible. There's a **user interface** to mount disks/folders on demand, called by the utility with **-i** option or, using the **hotkey** defined in CONFIG.SYS (if using the driver); all the **user interface options** are available also as **commands options at the utility**, like **-mount [drive,]path** and **KNTRL -unmount drive**.

The driver is initialized in CONFIG.SYS with these optional args:
* **-D** install debugger
* **-XT** | **-AT** IBM PC compatible type
* **-I** transfer always the control to the server application for debugging
* **-DH=x** sets the mounting/debugger user interface function key x
* **-IH=x** sets the debugger hotkey as function key x (immediately debugging on the server app)
* **-P=COMx,BAUDRATE** | **LPTx** sets the port to LPTx or COMx with the settings
* **-S=x** creates x block device slots



# kntrl-dos-drv (2019)
A DOS Driver or TSR + a Utility, able to communicate to a server PC application via serial port (i didn't had a chance to implement the Parallel Port code because i didn't had one at the time). Compiled with Borland Turbo C.

**It can**
* **emulate keyboard and mouse on a remote computer, change mouse cursors, extract the video-memory, etc** 
* **mount folders** located on the server PC (using the MS-DOS Installable File System, IFS/Redirector interface)
* **mount virtual disk/diskette images** as device block drivers located on the server PC
* **handle data transfers** between client and server PC
* **real-mode debugging** step, breakpoints, download arbritary memory space, upload and run arbitrary code at a location, perform I/O commands
* i don't provide the other-end PC Application that serves the driver/TSR, as it was left in oblivion without maintenance. So this is just the driver/tsr/utility code; it needs an app to establish a serial port connection and send/receive the appropriate packets. Also the app should ask for memory, disassembly,.. etc maintaining the state of debbuger, by sending step/run packets and receiving the CPU registers, among other things. Theres an interface for this called **DIX** at the driver that the app must conform. My choice for the debugger implementation was the **Capstone** library.

**Windows 95**

 This is a real mode driver for older computers running MS-DOS, and despite it works in Windows 95,  Windows will warning you once that its use can hit the computer performance.

**Description**

The solution is 1) DOS Driver + 2) a Utility + 3) TSR. It can used as 1+2 combo, or 2+3 combo. If the driver isn't installed (the 2+3 combo) then block device drivers aren't available, so no disk mounts. All other commands, transfer files, mount folders and debugger are possible. There's a **user interface** to mount disks/folders on demand, called by the utility with **-i** option or, using pressing **hotkey** defined in CONFIG.SYS (if using the driver); all the **user interface options** are available also as **commands options at the utility**, like **-mount [drive,]path** and **-unmount drive**.

The driver is initialized in CONFIG.SYS with these optional args:
* **-D** install debugger
* **-XT** | **-AT** IBM PC compatible type
* **-I** always transfer the control to the server application for debugging
* **-DH=x** sets the mounting/debugger user interface function key x
* **-IH=x** sets the debugger hotkey as function key x (immediately debugging on the server app)
* **-P=COMx,BAUDRATE** | **LPTx** sets the port to LPTx or COMx with the settings
* **-S=x** creates x block device slots

**User interface "relay"**
The text user interface is not local to the driver or TSR, instead, is provided by the server application. When invoked, the current video buffer is transferred with RLE compression to the server, and the server accepts the keyboard keys from the client. In this way the MS-DOS computer receive the available virtual image files for mounting, or the whole debugging user interface, transfering only the text block differences. After exiting the user interface, the saved video buffer is restored on the MS-DOS computer. This may not always work as it checks the current video mode on BIOS, and this is a bit unreliable.

**References**
* Dr Dobbs journal 
* MS-DOS Version 4.0 Programmer's Reference



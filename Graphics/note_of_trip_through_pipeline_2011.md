#[part-1 Introduction: the Software stack](http://fgiesen.wordpress.com/2011/07/01/a-trip-through-the-graphics-pipeline-2011-part-1/)#


##The D3D Software Stack is##

- Application
- Runtime
- The user-mode driver (UMD)
	- nvd3dum.dll and atiumd.dll
	- compile shaders
	- suballocates some larger memory blocks it gets **from** the KMD
	- translate API into commands, manages command buffers (DMA buffers)
- Scheduler in GPU
	- One gpu, multiple clients
	- Only one process gets to actually submit commands to the 3D pipe at any given time.
- The kernel-mode driver (KMD)
	- There may be multiple UMD instances running at any one time, but there’s only ever one KMD
	- initialize the GPU at startup
	- allocate (and map) **physical** memory
	- program the HW watchdog timer so the GPU gets reset if it stays unresponsive for a certain time
	- respond to interrupts
	- manages and writes to the **actual** command buffer
	- The main command buffer is usually a (quite small) ring buffer – the only thing that ever gets written there is system/initialization commands and calls to the “real”, meaty 3D command buffers.
- The bus
	- PIC Express
- The command processor
	- the frontend of the GPU
	- reads the commands the KMD writes

##The OpenGL Stack differs at#
- no sharp distinction between the API and UMD layer
- shader compilation handled by driver, which means drivers have to do all the optimizations themselves

#[part-2 GPU memory architecture and the Command Processor](http://fgiesen.wordpress.com/2011/07/02/a-trip-through-the-graphics-pipeline-2011-part-2/)


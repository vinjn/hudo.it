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

#[part-2 GPU memory architecture and the Command Processor](http://fgiesen.wordpress.com/2011/07/02/a-trip-through-the-graphics-pipeline-2011-part-2/)#
- difference
	- high bandwidth/throughput 
	- high latency
	- don’t wait for results that aren’t there yet, do something else instead!
- DRAM
	- DRAM chips are organized as a 2D grid – both logically and physically. There’s (horizontal) row lines and (vertical) column lines. At each intersection between such lines is a transistor and a capacitor.
	- address of a location in DRAM is split into a row address and a column address, and DRAM reads/writes internally always end up accessing all columns in the given row at the same time.
- The PCIe host interface
	- The bandwidth is decent though – up to about 8GB/s (theoretical) peak aggregate bandwidth across the 16-lane PCIe 2.0 connections
	- And unlike earlier standards like AGP, this is a symmetrical point-to-point link – that bandwidth goes both directions; AGP had a fast channel from the CPU to the GPU, but not the other way round.
- MMU (memory management unit)
	- allows you to defragment your video memory address space without having to actually copy stuff around when you start running out of video memory
- DMA copy engine
	- copy memory around without having to involve any of our precious 3D hardware/shader cores
	- system memory <-> video memory
 	- video memory -> video memory

[http://www.farbrausch.de/~fg/gpu/gpu_memory.jpg]

- The single command processor
	- Add a large enough buffer and prefetch far enough ahead to avoid hiccups.
	- The actual command processing front end is basically a state machine that knows how to parse commands (with a hardware-specific format). 
	- Some commands deal with 2D rendering operations – unless there’s a separate command processor for 2D stuff and the 3D frontend never even sees it. Either way, there’s still dedicated 2D hardware hidden on modern GPUs, just as there’s a VGA chip somewhere on that die that still supports text mode, 4-bit/pixel bit-plane modes, smooth scrolling and all that stuff. 
	- Some commands actually hand some primitives to the 3D/shader pipe
	- Some commands go to the 3D/shader pipe but never render anything
	- Some commands change states. A GPU is a massively parallel computer, and you can’t just change a global variable in a parallel system and hope that everything works out OK. The solutions are:
		- Whenever you change a state, you require that all pending work that might refer to that state be finished (i.e. basically a partial pipeline flush).
		- You can make hardware units completely stateless. Just pass the state change command through up to the stage that cares about it; then have that stage append the current state to everything it sends downstream, every cycle.
		- Maintain two copies of the state. Say you have enough registers (“slots”) to store two versions of every state, and some active job references slot 0. You can safely modify slot 1 without stopping that job, or otherwise interfering with it at all. 
		- You don’t want to reserve state space for 2*128 active textures just because you’re keeping track of 2 in-flight state sets so you might need it. For such cases, you can use a kind of register renaming scheme – have a pool of 128 physical texture descriptors.
- Synchronization
	
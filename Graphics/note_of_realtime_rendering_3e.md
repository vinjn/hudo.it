#The Color Buffer#
	- Color Mode:
		- High color: two bytes per pixel, 15 bits(5.5.5) or 16 bits(5.6.5)
		- True color: three or four bytes per pixel, 24 bits(8.8.8) or 32 bits(8.8.8.8)
	- Monitors can have more than 8 bits per channel.
#Z-Buffer#
	- Depth resolution
		- usually has 24 bits per pixel
		- low presision causes z-fighting
		- The characteristics of the perspective transform matrix result in greater precision for objects closer to the viewer
#Double Buffering#
	- To avoid the visibility problem
	- one front buffer plus one back buffer
	- full screen applications use a color buffer flipping technique, or pge flipping.
	- windowed applications use BLT swapping, or blitting.
#Sorting#
	- sort-first architecture sorts primitives before the geometry stage. devides the screen into a set of regions, and the primitives inside a region are sent to a complete pipeline that "owns" that region. Only used with multiple screens or projectors.
	- sort-middle architecture sorts primitives after primitives are transformed to screen coordinates. Each rasterizer unit is responsible for a screen-space region, here called a tile. The Mali 200.
	- sort-last fragment architecture happends after fragment generation (FG) and before fragment merge (FM).GPU of PS3 .
	- sort-last image architecture happends after fragment merge (FM).GPU of PS3. PixelFlow. Each pipeline renders an image with depth.

[303] [896]
	
#Texture Access#
	- Texture reading is often the main consumer of bandwidth. [10]
	- Use cache to save bandwidth, a small on-chip memory (a few kb) shared by all textures currently in use.
	- Use prefetching to hide latency, read and cache all neighboring texels together before further computation. That's why GPU has many registers.
	- Mipmapping improves both visuals and performance.
	- Texture swizzling improves cache performance and page locality.
		- Morton sequence [906]
#Memory Bandwidth#
	- A simplified model for the bandwidth used by a single fragment on its ways through the pixel pipeline.
	- Bc for color buffer, Bz for depth buffer, Bt for texture.
	- B = Bc + Bz + Bt
#Latency#
	- The latency is the time between making the query and receiving the result.
#Buffer Compression#
	- Tile table is an on-chip storage or a chache. Applies to Z-buffer compression as well as color and stencil.
	- Each table item stores the status and the maximun z-value, Zmax of, say, an 8 x 8 [902] tile of pixels in the frame buffer
	- The state can be
		- compressed, including different types of compression
		- uncompressed
		- cleared, marked by clear command of DX/OGL
#Z-Culling#
	- In order to test whether a triangle is occluded inside a tile, we need to computue the mininum z-value of the triangle. If it's bigger that Zmax of the tile, then it's occluded. Then both pixel shader and depth test can be avoided.
	- Use "less than" depth test
	- Occulusion culling benefits from rendering front to back.
	- It's time-consuming to computuer the extarct value of the mininum z-value, instead, we can:
		- Use the mininum z-value of the three vertices of the triangle
		- Use the mininum of the four corners of the tile using the plane equation of the triangle.
		- Take the larger of them.
	- AMD calls it HyperZ [1065]
	- NVIDIA calls it Lightspeed Memory Architecture (LMA)
#Early-Z#
	- If a tile survives Z-culling, there is early-Z [879, 1108].
	- It works only if the pixel shader does not modify the z-depth, and the render state is set for a typical Z-buffer test.
	- Before the execution of the pixel shader, the fragment's precise z-depth value is computed and compared to the Z-buffer's stored value. If the fragment is occluded, it is discarded.
	# Early-Z and Z-Culling are performed by separete handware, either technique can be used without the other.
#early z pass#
	- This is a software technique, the idea being to render geometry once and establish the Z-buffer depths. [7.9.2]

	
	
	
	
	
	
	
	
	
	
	
	
	
	
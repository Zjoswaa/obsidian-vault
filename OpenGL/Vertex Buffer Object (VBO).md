To start drawing something we have to first give OpenGL some input vertex data. OpenGL is a 3D graphics library so all coordinates that we specify in OpenGL are in 3D (`x`, `y` and `z` coordinate). OpenGL doesn't simply transform **all** our 3D coordinates to 2D pixels on our screen; OpenGL only processes 3D coordinates when they're in a specific range between `-1.0` and `1.0` on all 3 axes (`x`, `y` and `z`). All coordinates within this so called ==**normalized device coordinates**== range will end up visible on our screen (and all coordinates outside this region won't).

If we want to render a single triangle, we need to specify three vertices with each vertex having a 3D position. We define them in normalized device coordinates in a `float` array.
``` CPP
constexpr float vertices[] = {
	-0.5f, -0.5f, 0.0f,
	0.5f, -0.5f, 0.0f,
	0.0f, 0.5f, 0.0f
}
```
Because OpenGL works in 3D space we render a 2D triangle with each vertex having a `z` coordinate of `0.0`. This way the _depth_ of the triangle remains the same making it look like it's 2D.
> [!info]
> **Normalized Device Coordinates (NDC)**
> Once our vertex coordinates have been processed in the vertex shader, they should be in normalized device coordinates which is a small space where the `x`, `y` and `z` values vary from `-1.0` to `1.0`. Any coordinates that fall outside this range will be discarded/clipped and won't be visible on our screen.
> 
> The **center** of the screen is at coordinate `(0, 0)`
> **Bottom-left** is at `(-1, -1)`
> **Top-left** is at `(-1, 1)`
> **Top-right is at `(1, 1)`
> **Bottom-right** is at `(1, -1)`

With the vertex data defined we'd like to send it as input to the first process of the graphics pipeline: the vertex shader. This is done by creating memory on the GPU where we store the vertex data, configure how OpenGL should interpret the memory and specify how to send the data to the graphics card. The vertex shader then processes as much vertices as we tell it to from its memory.

We manage this memory via so called ==**vertex buffer objects (VBO)**== that can store a large number of vertices in the GPU's memory. The advantage of using those buffer objects is that we can send large batches of data all at once to the graphics card, and keep it there if there's enough memory left, without having to send data one vertex at a time. **Sending data to the graphics card from the CPU is relatively slow**, so wherever we can we try to send as much data as possible at once. Once the data is in the graphics card's memory the vertex shader has almost instant access to the vertices making it extremely fast.

Creating a VBO follows the regular [[OpenGL|OpenGL object]] creation, it has a unique ID corresponding to that buffer, so we can generate one with a buffer ID using the `glGenBuffers` function:
``` CPP
unsigned int VBO;
glGenBuffers(1, &VBO);
```
OpenGL has many types of buffer objects and the buffer type of a vertex buffer object is `GL_ARRAY_BUFFER`. OpenGL allows us to bind to several buffers at once as long as they have a different buffer type. We can bind the buffer to the `GL_ARRAY_BUFFER` target with the `glBindBuffer` function:
``` CPP
glBindBuffer(GL_ARRAY_BUFFER, VBO);
```
From that point on any buffer calls we make (on the `GL_ARRAY_BUFFER` target) will be used to configure the currently bound buffer, which is `VBO`. Then we can make a call to the `glBufferData` function that copies the previously defined vertex data into the buffer's memory:
``` CPP
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
```
`glBufferData` is a function specifically targeted to copy user-defined data into the currently bound buffer. Its first argument is the type of the buffer we want to copy data into: the vertex buffer object currently bound to the `GL_ARRAY_BUFFER` target. The second argument specifies the size of the data (in bytes) we want to pass to the buffer, using `sizeof` of the vertex data suffices. The third parameter is the actual data we want to send.
The fourth parameter specifies how we want the graphics card to manage the given data. This can take 3 forms:
- `GL_STREAM_DRAW`: the data is set only once and used by the GPU at most a few times.
- `GL_STATIC_DRAW`: the data is set only once and used many times.
- `GL_DYNAMIC_DRAW`: the data is changed a lot and used many times.

The position data of the triangle does not change, is used a lot, and stays the same for every render call so its usage type should best be `GL_STATIC_DRAW`. If, for instance, one would have a buffer with data that is likely to change frequently, a usage type of `GL_DYNAMIC_DRAW` ensures the graphics card will place the data in memory that allows for faster writes.

As of now we stored the vertex data within memory on the graphics card as managed by a vertex buffer object named `VBO`. Next we want to create a [[Vertex Shader|vertex shader]] and fragment shader that actually processes this data.
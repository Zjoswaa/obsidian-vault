## What is OpenGL
OpenGL is a cross-language, cross-platform application programming interface for rendering 2D and 3D vector graphics.
It is typically used to interact with a graphics processing unit (GPU), to achieve hardware-accelerated rendering.

However, OpenGL itself is not an API, it is merely a specification, developed and maintained by the Khronos Group. This specification specifies exactly what the result/output of each function should be and how it should perform. It is then up to the developers *implementing* the specification to come up with a solution on how this function should operate.
Most implementations are made by graphics cards manufacturers in the form of graphics drivers, that include the newest versions of OpenGL that your card supports.
## State machine
OpenGL is by itself a large state machine: a collection of variables that define how OpenGL should currently operate. This state of OpenGL if often referred to as the OpenGL ==**context**==.

When using OpenGL, we change this state by for example setting options and manipulating some buffers by calling functions. We then render using the current context.\

## Objects
The OpenGL libraries are written in C and allows for many derivations in other languages, but in its core it remains a C-library. Since many of C's language-constructs do not translate that well to other higher-level languages, OpenGL was developed with several abstractions in mind. One of those abstractions are ==**objects**== in OpenGL.

An object in OpenGL is a collection of options that represents a subset of OpenGL's state. For example, we could have an object that represents the settings of the drawing window; we could then set its size, how many colors it supports and so on. One could visualize an object as a C-like struct:
``` C
struct object_name {
	float option1;
	float option2;
	char[] name;
}
```
Whenever we want to use objects it generally looks something like this (with OpenGL's context visualized as a large struct):
``` C
// The state of OpenGL
struct OpenGL_Context {
	...
	object_name* object_Window_Target;
	...
}
```
``` C
// Create object
unsigned int objectId = 0;
glGenObject(1, &objectId);
// Bind/assign object to context
glBindObject(GL_WINDOW_TARGET, objectId);
// Set options for object currently bound to GL_WINDOW_TARGET
glSetObjectOption(GL_WINDOW_TARGET, GL_WINDOW_WIDTH, 800);
glSetObjectOption(GL_WINDOW_TARGET, GL_WINDOW_HEIGHT, 600);
// Set context target back to default
glBindObject(GL_WINDOW_TARGET, 0);
```
This piece of code is a workflow you'll frequently see when working with OpenGL. We first create an object and store a reference to it as an id (the real object's data is stored behind the scenes). Then we bind the object (using its id) to the target location of the context (the location of the example window object target is defined as `GL_WINDOW_TARGET`). Next we set the window options and finally we un-bind the object by setting the current object id of the window target to `0`. The options we set are stored in the object referenced by `objectId` and restored as soon as we bind the object back to `GL_WINDOW_TARGET`.
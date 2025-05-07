OpenGL expects all the vertices, that we want to become visible, to be in normalized device coordinates after each vertex shader run. That is, the `x`, `y` and `z` coordinates of each vertex should be between `-1.0` and `1.0`; coordinates outside this range will not be visible. What we usually do, is specify the coordinates in a range (or space) we determine ourselves and in the vertex shader transform these coordinates to normalized device coordinates (NDC). These NDC are then given to the rasterizer to transform them to 2D coordinates/pixels on your screen.

Transforming coordinates to NDC is usually accomplished in a step-by-step fashion where we transform an object's vertices to several coordinate systems before finally transforming them to NDC. The advantage of transforming them to several _intermediate_ coordinate systems is that some operations/calculations are easier in certain coordinate systems. There are a total of 5 different coordinate systems that are of importance to us:
- Local space / Object space
- World space
- View space / Eye space
- Clip space
- Screen space
Those are all a different state at which our vertices will be transformed in before finally ending up as fragments.
## The global picture
To transform the coordinates from one space to the next coordinate space we'll use several transformation matrices of which the most important are the ==**model**==, ==**view**== and ==**projection**== matrix. Our vertex coordinates first start in local space as **local coordinates** and are then further processed to **world coordinates**, **view coordinates**, **clip coordinates** and eventually end up as **screen coordinates**. The following image displays the process and shows what each transformation does:

![[Coordinate Spaces.png]]
1. Local coordinates are the coordinates of your object relative to its local origin; they're the coordinates your object begins in.
2. The next step is to transform the local coordinates to world-space coordinates which are coordinates in respect of a larger world. These coordinates are relative to some global origin of the world, together with many other objects also placed relative to this world's origin.
3. Next we transform the world coordinates to view-space coordinates in such a way that each coordinate is as seen from the camera or viewer's point of view.
4. After the coordinates are in view space we want to project them to clip coordinates. Clip coordinates are processed to the `-1.0` and `1.0` range and determine which vertices will end up on the screen. Projection to clip-space coordinates can add perspective if using perspective projection.
5. And lastly we transform the clip coordinates to screen coordinates in a process we call viewport transform that transforms the coordinates from `-1.0` and `1.0` to the coordinate range defined by `glViewport`. The resulting coordinates are then sent to the rasterizer to turn them into fragments.
> [!info]
The reason we're transforming our vertices into all these different spaces is that some operations make more sense or are easier to use in certain coordinate systems. For example, when modifying your object it makes most sense to do this in local space, while calculating certain operations on the object with respect to the position of other objects makes most sense in world coordinates and so on. If we want, we could define one transformation matrix that goes from local space to clip space all in one go, but that leaves us with less flexibility.
## Local space
Local space is the coordinate space that is local to your object, i.e. where your object begins in. Imagine that you've created your cube in a modeling software package (like Blender). The origin of your cube is probably at `(0,0,0)` even though your cube may end up at a different location in your final application. Probably all the models you've created all have `(0,0,0)` as their initial position. All the vertices of your model are therefore in _local_ space: they are all local to your object.

The vertices of the container has coordinates between `-0.5` and `0.5` with `0.0` as its origin. These are local coordinates.
## World space
If we would import all our objects directly in the application they would probably all be somewhere positioned inside each other at the world's origin of `(0,0,0)` which is not what we want. We want to define a position for each object to position them inside a larger world. The coordinates in world space are exactly what they sound like: the coordinates of all your vertices relative to a (game) world. This is the coordinate space where you want your objects transformed to in such a way that they're all scattered around the place (preferably in a realistic fashion). The coordinates of your object are transformed from local to world space; this is accomplished with the **model** matrix.
The model matrix is a transformation matrix that translates, scales and/or rotates your object to place it in the world at a location/orientation they belong to. Think of it as transforming a house by scaling it down (it was a bit too large in local space), translating it to a suburbia town and rotating it a bit to the left on the y-axis so that it neatly fits with the neighboring houses.
## View space
The view space is what people usually refer to as the **camera** of OpenGL (it is sometimes also known as **camera space** or **eye space**). The view space is the result of transforming your world-space coordinates to coordinates that are in front of the user's view. The view space is thus the space as seen from the camera's point of view. This is usually accomplished with a combination of translations and rotations to translate/rotate the scene so that certain items are transformed to the front of the camera. These combined transformations are generally stored inside a **view matrix** that transforms world coordinates to view space.
## Clip space
At the end of each vertex shader run, OpenGL expects the coordinates to be within a specific range and any coordinate that falls outside this range is clipped. Coordinates that are clipped are discarded, so the remaining coordinates will end up as fragments visible on your screen. This is also where clip space gets its name from.

Because specifying all the visible coordinates to be within the range `-1.0` and `1.0` isn't really intuitive, we specify our own coordinate set to work in and convert those back to NDC as OpenGL expects them.

To transform vertex coordinates from view to clip-space we define a so called **projection matrix** that specifies a range of coordinates e.g. `-1000` and `1000` in each dimension. The projection matrix then converts coordinates within this specified range to normalized device coordinates (`-1.0`, `1.0`) (not directly, a step called **Perspective Division** sits in between). All coordinates outside this range will not be mapped between `-1.0` and `1.0` and therefore be clipped. With this range we specified in the projection matrix, a coordinate of (`1250`, `500`, `750`) would not be visible, since the `x` coordinate is out of range and thus gets converted to a coordinate higher than `1.0` in NDC and is therefore clipped.
>[!note]
>Note that if only a part of a primitive e.g. a triangle is outside the **clipping volume** OpenGL will reconstruct the triangle as one or more triangles to fit inside the clipping range.

This _viewing box_ a projection matrix creates is called a ==**frustum**== and each coordinate that ends up inside this frustum will end up on the user's screen. The total process to convert coordinates within a specified range to NDC that can easily be mapped to 2D view-space coordinates is called **projection** since the projection matrix **projects** 3D coordinates to the easy-to-map-to-2D normalized device coordinates.

Once all the vertices are transformed to clip space a final operation called **perspective division** is performed where we divide the `x`, `y` and `z` components of the position vectors by the vector's homogeneous `w` component; perspective division is what transforms the 4D clip space coordinates to 3D normalized device coordinates. This step is performed automatically at the end of the vertex shader step.

It is after this stage where the resulting coordinates are mapped to screen coordinates (using the settings of `glViewport`) and turned into fragments.

The projection matrix to transform view coordinates to clip coordinates usually takes two different forms, where each form defines its own unique frustum. We can either create an **orthographic** projection matrix or a **perspective** projection matrix.
### Orthographic projection
An orthographic projection matrix defines a cube-like frustum box that defines the clipping space where each vertex outside this box is clipped. When creating an orthographic projection matrix we specify the width, height and length of the visible frustum. All the coordinates inside this frustum will end up within the NDC range after transformed by its matrix and thus won't be clipped. The frustum looks a bit like a container:

![[Orthographic Projection.png]]
The frustum defines the visible coordinates and is specified by a **width**, a **height** and a **near** and **far** plane. Any coordinate in front of the near plane is clipped and the same applies to coordinates behind the far plane. The orthographic frustum **directly** maps all coordinates inside the frustum to normalized device coordinates without any special side effects since it won't touch the `w` component of the transformed vector; if the `w` component remains equal to `1.0` perspective division won't change the coordinates.
To create an orthographic projection matrix we make use of [[GLM]]'s built-in function `glm::ortho`
``` C++
glm::ortho(0.0f, 800.0f, 0.0f, 600.0f, 0.1f, 100.0f);
```
The first two parameters specify the left and right coordinate of the frustum and the third and fourth parameter specify the bottom and top part of the frustum. With those 4 points we've defined the size of the near and far planes and the 5th and 6th parameter then define the distances between the near and far plane. This specific projection matrix transforms all coordinates between these `x`, `y` and `z` range values to normalized device coordinates.

An orthographic projection matrix directly maps coordinates to the 2D plane that is your screen, but in reality a direct projection produces unrealistic results since the projection doesn't take **perspective** into account.
### Perspective projection
If you ever were to enjoy the graphics the _real life_ has to offer you'll notice that objects that are farther away appear much smaller. This effect is called **perspective**.
Due to perspective lines seem to coincide at a far enough distance. This is exactly the effect perspective projection tries to mimic and it does so using a **perspective projection matrix**. The projection matrix maps a given frustum range to clip space, but also manipulates the `w` value of each vertex coordinate in such a way that the further away a vertex coordinate is from the viewer, the higher this `w` component becomes. Once the coordinates are transformed to clip space they are in the range `-w` to `w` (anything outside this range is clipped). OpenGL requires that the visible coordinates fall between the range `-1.0` and `1.0` as the final vertex shader output, thus once the coordinates are in clip space, perspective division is applied to the clip space coordinates:
$$
out=
\begin{pmatrix}
\frac{x}{w}\\
\frac{y}{w}\\
\frac{z}{w}
\end{pmatrix}
$$
Each component of the vertex coordinate is divided by its `w` component giving smaller vertex coordinates the further away a vertex is from the viewer. This is another reason why the `w` component is important, since it helps us with perspective projection. The resulting coordinates are then in normalized device space.
A perspective projection matrix can be created in [[GLM]] as follows:
``` C++
glm::mat4 proj = glm::perspective(glm::radians(45.0f), (float)width/(float)height, 0.1f, 100.0f);
```
What `glm::perspective` does is again create a large frustum that defines the visible space, anything outside the frustum will not end up in the clip space volume and will thus become clipped. A perspective frustum can be visualized as a non-uniformly shaped box from where each coordinate inside this box will be mapped to a point in clip space. An image of a perspective frustum is seen below:

![[Perspective Projection.png]]
Its first parameter defines the **FOV** value, that stands for field of view and sets how large the viewspace is. For a realistic view it is usually set to 45 degrees, but for more doom-style results you could set it to a higher value. The second parameter sets the aspect ratio which is calculated by dividing the viewport's width by its height. The third and fourth parameter set the _near_ and _far_ plane of the frustum. We usually set the near distance to `0.1` and the far distance to `100.0`. All the vertices between the near and far plane and inside the frustum will be rendered.
>[!info]
>Whenever the _near_ value of your perspective matrix is set too high (like `10.0`), OpenGL will clip all coordinates close to the camera (between `0.0` and `10.0`), which can give a visual result you maybe have seen before in videogames where you could see through certain objects when moving uncomfortably close to them.
## Putting it all together
We create a transformation matrix for each of the aforementioned steps: model, view and projection matrix. A vertex coordinate is then transformed to clip coordinates as follows:
$$
V_{clip}=M_{projection}\cdot M_{view}\cdot M_{model}\cdot M_{local}
$$
Note that the order of matrix multiplication is reversed (remember that we need to read matrix multiplication from right to left). The resulting vertex should then be assigned to `gl_Position` in the vertex shader and OpenGL will then automatically perform perspective division and clipping.
>[!info]
>The output of the vertex shader requires the coordinates to be in clip-space which is what we just did with the transformation matrices. OpenGL then performs _perspective division_ on the _clip-space coordinates_ to transform them to _normalized-device coordinates_. OpenGL then uses the parameters from `glViewPort` to map the normalized-device coordinates to _screen coordinates_ where each coordinate corresponds to a point on your screen (in our case a 800x600 screen). This process is called the _viewport transform_.

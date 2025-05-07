OpenGL shaders are written in the C-like language [[GLSL]].
Shaders always begin with a version declaration, followed by a list of input and output variables, uniforms and its `main` function. For example:
``` GLSL
#version version_number
in type in_variable_name;
in type in_variable_name;

out type out_variable_name;
  
uniform type uniform_name;
  
void main() {
	// process input(s) and do some weird graphics stuff
	...
	// output processed stuff to output variable
	out_variable_name = weird_stuff_we_processed;
}
```
When we're talking specifically about the vertex shader each input variable is also known as a *vertex attribute*. There is a maximum number of vertex attributes we're allowed to declare limited by the hardware. OpenGL guarantees there are always at least 16 4-component vertex attributes available, but some hardware may allow for more which you can retrieve by querying `GL_MAX_VERTEX_ATTRIBS`:
``` CPP
int nrAttributes;
glGetIntegerv(GL_MAX_VERTEX_ATTRIBS, &nrAttributes);
std::cout << "Maximum nr of vertex attributes supported: " << nrAttributes << std::endl;
```
## Types
GLSL has most of the basic data types:
- `int`
- `float`
- `double`
- `uint`
- `bool`
It also contains two special container types:
- Vectors
- Matrices
## `in` and `out`
Each shader can specify inputs and outputs using the `in` and `out` keywords and wherever an output variable matches with an input variable of the next shader stage they're passed along. The vertex and fragment shader differ a bit though.

The vertex shader **should** receive some form of input otherwise it would be pretty ineffective. The vertex shader differs in its input, in that it receives its input straight from the vertex data. To define how the vertex data is organized we specify the input variables with location metadata so we can configure the vertex attributes on the CPU. This is done with the line: `layout (location = 0)`. The vertex shader thus requires an extra layout specification for its inputs so we can link it with the vertex data.

The other exception is that the fragment shader requires a `vec4` color output variable, since the fragment shaders needs to generate a final output color. If you fail to specify an output color in your fragment shader, the color buffer output for those fragments will be undefined (which usually means OpenGL will render them either black or white).

So if we want to send data from one shader to the other we'd have to declare an output in the sending shader and a similar input in the receiving shader. When the types and the names are equal on both sides OpenGL will link those variables together and then it is possible to send data between shaders (this is done when linking a program object). To show you how this works in practice we're going to alter the shaders from the previous chapter to let the vertex shader decide the color for the fragment shader.
## Uniforms
**Uniforms** are another way to pass data from our application on the CPU to the shaders on the GPU. Uniforms are however slightly different compared to vertex attributes. First of all, uniforms are ==**global**==. Meaning that a uniform variable is unique per shader program object, and can be accessed from any shader at any stage in the shader program. Second, whatever you set the uniform value to, uniforms will keep their values until they're either reset or updated.

To declare a uniform in GLSL we simply add the `uniform` keyword to a shader with a type and a name. From that point on we can use the newly declared uniform in the shader. Let's see if this time we can set the color of the triangle via a uniform:
``` GLSL
#version 330 core
out vec4 FragColor;
  
uniform vec4 uColor;

void main()
{
    FragColor = uColor;
}
```
The uniform is currently empty; we haven't added any data to the uniform yet so let's try that. We first need to find the index/location of the uniform attribute in our shader. Once we have the index/location of the uniform, we can update its values:
``` CPP
int vertexColorLocation = glGetUniformLocation(shaderProgram, "uColor");
glUseProgram(shaderProgram);
glUniform4f(vertexColorLocation, 0.0f, 1.0f, 0.0f, 1.0f);
```
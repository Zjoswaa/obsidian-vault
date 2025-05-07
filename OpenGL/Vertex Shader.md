The vertex shader is one of the [[Shader|shaders]] that are user-programmable. Modern OpenGL requires that we at least set up a vertex and fragment shader if we want to do some rendering.

The first thing we need to do is write the vertex shader in the shader language [[GLSL]] (OpenGL Shading Language) and then compile this shader so we can use it in our application. Below is the source code of a very basic vertex shader in [[GLSL]]:
``` C
#version 330 core
layout (location = 0) in vec3 aPos;

void main() {
	gl_Position = vec4(aPos.x, aPox.y, aPos.z, 1.0);
}
```
We declare all the input vertex attributes in the vertex shader with the `in` keyword. Right now we only care about position data so we only need a single vertex attribute. [[GLSL]] has a vector datatype that contains 1 to 4 floats based on its postfix digit. Since each vertex has a 3D coordinate we create a `vec3` input variable with the name `aPos`. We also specifically set the location of the input variable via `layout (location = 0)`.

To set the output of the vertex shader we have to assign the position data to the predefined `gl_Position` variable which is a `vec4` behind the scenes. At the end of the main function, whatever we set `gl_Position` to will be used as the output of the vertex shader. Since our input is a vector of size 3 we have to cast this to a vector of size 4. We can do this by inserting the `vec3` values inside the constructor of `vec4` and set its `w` component to `1.0f`.

This vertex shader is probably the most simple vertex shader we can imagine because we did no processing whatsoever on the input data and simply forwarded it to the shader's output. In real applications the input data is usually not already in normalized device coordinates so we first have to transform the input data to coordinates that fall within OpenGL's visible region.

## Compiling
We take the source code for the vertex shader and store it in a const C string for now:
``` CPP
const char *vertexShaderSource* = "#version 330 core\n"
	"layout (location = 0) in aPos;\n"
	"void main() {\n"
	"    gl_Position = vec4(aPos.x, aPox.y, aPos.z, 1.0);\n"
	"}\0"
```
In order for OpenGL to use the shader it has to dynamically compile it at run-time from its source code. The first thing we need to do is create a shader [[OpenGL|object]], again referenced by an ID. So we store the vertex shader as an `unsigned int` and create the shader with `glCreateShader`:
``` CPP
unsigned int vertexShader;
vertexShader = glCreateShader(GL_VERTEX_SHADER);
```
We provide the type of shader we want to create as an argument to `glCreateShader`. Since we're creating a vertex shader we pass in `GL_VERTEX_SHADER`.

Next we attach the shader source code to the shader object and compile the shader:
``` CPP
glShaderSource(vertexShader, 1, &vertexShaderSource, nullptr);
glCompileShader(vertexShader);
```
The `glShaderSource` function takes the shader object to compile to as its first argument. The second argument specifies how many strings we're passing as source code, which is only one. The third parameter is the actual source code of the vertex shader and we can leave the 4th parameter to `nullptr`.
> [!tip]
> You probably want to check if compilation was successful after the call to `glCompileShader` and if not, what errors were found so you can fix those. Checking for compile-time errors is accomplished as follows:
> ``` CPP
> int succes;
> char infoLog[512];
> glGetShaderiv(vertexShader, GL_COMPILE_STATUS, &success);
> ```
> First we define an integer to indicate success and a storage container for the error messages (if any). Then we check if compilation was successful with `glGetShaderiv`. If compilation failed, we should retrieve the error message with `glGetShaderInfoLog` and print the error message:
> ``` CPP
> if (!success) {
>     glGetShaderInfoLog(vertexShader, 512, nullptr, infoLog);
> 	std::cerr << "Vertex shader compilation failed\n" << infoLog << std::endl;
> }
> ```
> If no errors were detected while compiling the vertex shader it is now compiled.

Finally, the shader needs to be linked into a [[Shader Program|shader program]], together with a [[Fragment Shader|fragment shader]].
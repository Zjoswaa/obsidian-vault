The fragment shader is one of the [[Shader|shaders]] that are user-programmable. The fragment shader is all about calculating the color output of your pixels. To keep things simple the fragment shader will always output an orange-ish color.
> [!info]
> Colors in computer graphics are represented as an array of 4 values: the red, green, blue and alpha (opacity) component, commonly abbreviated to RGBA. When defining a color in OpenGL or [[GLSL]] we set the strength of each component to a value between `0.0` and `1.0`. If, for example, we would set red to `1.0` and green to `1.0` we would get a mixture of both colors and get the color yellow. Given those 3 color components we can generate over **16 million** different colors.
``` GLSL
#version 330 core
out vec4 FragColor;

void main() {
	FragColor = vec4(1.0f, 0.5f, 0.2f, 1.0f);
}
```
The fragment shader only requires one output variable and that is a vector of size 4 that defines the final color output that we should calculate ourselves. We can declare output values with the `out` keyword, that we here promptly named `FragColor`. Next we simply assign a `vec4` to the color output as an orange color with an alpha value of `1.0` (`1.0` being completely opaque).\
## Compiling
The process for compiling a fragment shader is similar to the [[Vertex Shader|vertex shader]], although this time we use the `GL_FRAGMENT_SHADER` constant as the shader type:
``` CPP
unsigned int fragmentShader;
fragmentShader = glCreateShader(GL_FRAGMENT_SHADER);
glShaderSource(fragmentShader, 1, &fragmentShaderSource, nullptr);
glCompileShader(fragmentShader);
```
> [!tip]
> You probably want to check if compilation was successful after the call to `glCompileShader` and if not, what errors were found so you can fix those. Checking for compile-time errors is accomplished as follows:
> ``` CPP
> int succes;
> char infoLog[512];
> glGetShaderiv(fragmentShader, GL_COMPILE_STATUS, &success);
> ```
> First we define an integer to indicate success and a storage container for the error messages (if any). Then we check if compilation was successful with `glGetShaderiv`. If compilation failed, we should retrieve the error message with `glGetShaderInfoLog` and print the error message:
> ``` CPP
> if (!success) {
>     glGetShaderInfoLog(fragmentShader, 512, nullptr, infoLog);
> 	std::cerr << "Fragment shader compilation failed\n" << infoLog << std::endl;
> }
> ```
> If no errors were detected while compiling the vertex shader it is now compiled.

Finally, the shader needs to be linked into a [[Shader Program|shader program]], together with a [[Vertex Shader|vertex shader]].
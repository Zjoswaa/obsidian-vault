A shader program object is the final linked version of multiple shaders combined. To use the recently compiled shaders we have to *link* them to a shader program object and then activate this shader program when rendering objects. The activated shader program's shaders will be used when we issue render calls.

When linking the shaders into a program it links the outputs of each shader to the inputs of the next shader. This is also where you'll get linking errors if your outputs and inputs do not match.

To create a shader program:
``` CPP
unsigned int shaderProgram;
shaderProgram = glCreateProgram();
```
The `glCreateProgram` function creates a program and returns the ID reference to the newly created program object. Now we need to attach the previously compiled shaders to the program object and then link them with `glLinkProgram`:
``` CPP
glAttachShader(shaderProgram, vertexShader);
glAttachShader(shaderProgram, fragmentShader);
glLinkProgram(shaderProgram);
```
> [!tip]
> Just like shader compilation we can also check if linking a shader program failed and retrieve the corresponding log. However, instead of using `glGetShaderiv` and `glGetShaderInfoLog` we now use:
> ``` CPP
> glGetProgramiv(shaderProgram, GL_LINK_STATUS, &success);
> if (!success) {
>     glGetProgramInfoLog(shaderProgram, 512, nullptr, infoLog);
> 	std::cerr << "Shader program linking failed\n" << infoLog << std::endl;
> }
> ```

The result is a program object that we can activate by calling `glUseProgram` with the newly created program object as its argument:
``` CPP
glUseProgram(shaderProgram);
```
Every shader and rendering call after `glUseProgram` will now use this program object (and thus the shaders).

> [!warning]
> Don't forget to delete the shader objects once we've linked them into the program object; we no longer need them anymore:
> ``` CPP
> glDeleteShader(vertexShader);
> glDeleteShader(fragmentShader);
> ```


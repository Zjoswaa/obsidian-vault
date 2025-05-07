If you have many [[Vertex Attributes|vertex attributes]] and many different objects. You would have to bind the appropriate [[Vertex Buffer Object (VBO)|buffer]] objects and configure all [[Vertex Attributes|attributes]] for every object quickly, this will become a cumbersome process.
Luckily, there is the ==**vertex array object**==, also known as a ==**VAO**== can be bound just like a [[Vertex Buffer Object (VBO)|VBO]] and any subsequent vertex attribute calls from that point on will be stored inside the VAO. This has the advantage that when configuring vertex attribute pointers you only have to make those calls once and whenever we want to draw the object, we can just bind the corresponding VAO. This makes switching between different vertex data and attribute configurations as easy as binding a different VAO. All the state we just set is stored inside the VAO.
> [!warning]
> Core OpenGL **requires** that we use a VAO so it knows what to do with our vertex inputs. If we fail to bind a VAO, OpenGL will most likely refuse to draw anything.

A vertex array object stores the following:
- Calls to `glEnableVertexAttribArray` or `glDisableVertexAttribArray`.
- Vertex attribute configurations via `glVertexAttribPointer`.
- Vertex buffer objects associated with vertex attributes by calls to `glVertexAttribPointer`.

Creating a VBO follows the regular [[OpenGL|OpenGL object]] creation, it has a unique ID corresponding to that buffer, so we can generate one with a buffer ID using the `glGenVertexArrays` function:
``` CPP
unsigned int VAO;
glGenVertexArrays(1, &VAO);
```
To use a VAO all you have to do is bind the VAO using `glBindVertexArray`. From that point on we should bind/configure the corresponding VBO(s) and attribute pointer(s) and then unbind the VAO for later use. As soon as we want to draw an object, we simply bind the VAO with the preferred settings before drawing the object and that is it. In code this would look a bit like this:
``` CPP
// 1. Bind VAO.
glBindVertexArray(VAO);
// 2. Copy our vertices array in a buffer for OpenGL to use.
blBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
// 3. Then set our vertex attributes pointers
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);

[...]

// (In render loop)
// 4. Draw the object
glUseProgram(shaderProgram);
glBindVertexArray(VAO);
glDrawArrays(GL_TRIANGLES, 0, 3);
```
> [!info]
> Usually when you have multiple objects you want to draw, you first generate/configure all the VAOs (and thus the required VBO and attribute pointers) and store those for later use. The moment we want to draw one of our objects, we take the corresponding VAO, bind it, then draw the object and unbind the VAO again.

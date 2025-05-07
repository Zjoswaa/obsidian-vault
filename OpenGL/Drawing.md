To actually draw something to the screen you need to do the following:
- An active [[Shader Program|shader program]] that has been linked with a [[Vertex Shader|vertex shader]] and [[Fragment Shader|fragment shader]].
- A bound [[Vertex Array Object (VAO)|VAO]].
- Data from the [[Vertex Buffer Object (VBO)|VBO]]'s vertex data (indirectly bound via the VAO).
Then it would look something like this:
``` CPP
glUseProgram(shaderProgram);
glBindVertexArray(VAO);
gLDrawArrays(GL_TRIANGLES, 0, 3);
```
The `glDrawArrays` takes as its first argument the OpenGL primitive type we would like to draw. The second argument specifies the starting index of the vertex array we'd like to draw. The third argument specifies how many vertices we want to draw.
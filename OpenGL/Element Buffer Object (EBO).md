	There is one last thing we'd like to discuss when rendering vertices and that is ==element buffer objects== abbreviated to EBO. To explain how element buffer objects work it's best to give an example: suppose we want to draw a rectangle instead of a triangle. We can draw a rectangle using two triangles (OpenGL mainly works with triangles). This will generate the following set of vertices:
``` CPP
constexpr float vertices[] = {
	// First triangle
	0.5f, 0.5f, 0.0f,   // Top right
	0.5f, -0.5f, 0.0f,  // Bottom right
	-0.5f, 0.5f, 0.0f,  // Top left
	// Second triangle
	0.5f, -0.5f, 0.0f,  // Bottom right
	-0.5f, -0.5f, 0.0f, // Bottom left
	-0.5f, 0.5f, 0.0f   // Top left
}
```
As you can see, there is some overlap on the vertices specified. We specify `Bottom right` and `Top left` twice! This is an overhead of 50% since the same rectangle could also be specified with only 4 vertices, instead of 6. This will only get worse as soon as we have more complex models that have over 1000s of triangles where there will be large chunks that overlap. What would be a better solution is to store only the unique vertices and then specify the order at which we want to draw these vertices in. In that case we would only have to store 4 vertices for the rectangle, and then just specify at which order we'd like to draw them.

Thankfully, element buffer objects work exactly like that. An EBO is a buffer, just like a [[Vertex Buffer Object (VBO)|vertex buffer object]], that stores indices that OpenGL uses to decide what vertices to draw. This so called ==**indexed drawing**== is exactly the solution to our problem. To get started we first have to specify the (unique) vertices and the indices to draw them as a rectangle:
``` CPP
constexpr float vertices[] = {
	// First triangle
	0.5f, 0.5f, 0.0f,   // Top right
	0.5f, -0.5f, 0.0f,  // Bottom right
	-0.5f, -0.5f, 0.0f, // Bottom left
	-0.5f, 0.5f, 0.0f   // Top left
};

constexpr unsigned int indices[] = {
	0, 1, 3, // First triangle
	1, 2, 3  // Second triangle
};
```
You can see that, when using indices, we only need 4 vertices instead of 6. Next we need to create the element buffer object:
``` CPP
unsigned int EBO;
glGenBuffers(1, &EBO);
```
Similar to the VBO we bind the EBO and copy the indices into the buffer with `glBufferData`. Also, just like the VBO we want to place those calls between a bind and an unbind call, although this time we specify `GL_ELEMENT_ARRAY_BUFFER` as the buffer type.
``` CPP
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);
```
Note that we're now giving `GL_ELEMENT_ARRAY_BUFFER` as the buffer target. The last thing left to do is replace the `glDrawArrays` call with `glDrawElements` to indicate we want to render the triangles from an index buffer. When using `glDrawElements` we're going to draw using indices provided in the element buffer object currently bound:
``` CPP
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
```
The first argument specifies the mode we want to draw in, similar to `glDrawArrays`. The second argument is the count or number of elements we'd like to draw. We specified 6 indices so we want to draw 6 vertices in total. The third argument is the type of the indices which is of type `GL_UNSIGNED_INT`. The last argument allows us to specify an offset in the EBO (or pass in an index array, but that is when you're not using element buffer objects), but we're just going to leave this at 0.
The `glDrawElements` function takes its indices from the EBO currently bound to the `GL_ELEMENT_ARRAY_BUFFER` target. This means we have to bind the corresponding EBO each time we want to render an object with indices which again is a bit cumbersome. It just so happens that a [[Vertex Array Object (VAO)|vertex array object]] also keeps track of element buffer object bindings. The last element buffer object that gets bound while a VAO is bound, is stored as the VAO's element buffer object. Binding to a VAO then also automatically binds that EBO.
The resulting initialization code then look something like this:
``` CPP
// 1. Bind Vertex Array Object.
glBindVertexArray(VAO);
// 2. Copy our vertices array in a vertex buffer for OpenGL to use.
glBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
// 3. Copy our index array in a element buffer for OpenGL to use.
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);
// 4. Then set the vertex attributes pointers.
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
glEnableVertexAttribArray(0);  

[...]
  
// In render loop
// 5. Draw the object
glUseProgram(shaderProgram);
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
glBindVertexArray(0);
```
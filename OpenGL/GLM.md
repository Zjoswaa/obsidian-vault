GLM stands for Open**GL** **M**athematics and is a _header-only_ library used for vector and matrix math.
It is useful when working with [[Transforms|transforms]] and [[Coordinate Systems|coordinates]]
``` C++
#include <iostream>
#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>

glm::vec4 vec(1.0f, 0.0f, 0.0f, 1.0f);
glm::mat4 trans = glm::mat4(1.0f);
trans = glm::translate(trans, glm::vec3(1.0f, 1.0f, 0.0f));
trans = glm::rotate(trans, glm::radians(90.0f), glm::vec3(0.0, 0.0, 1.0));
trans = glm::scale(trans, glm::vec3(0.5, 0.5, 0.5));
vec = trans * vec;
std::cout << vec.x << vec.y << vec.z << std::endl;
```

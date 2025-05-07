# Vectors
Represent **directions** or **positions**
- `(x, y)`
- `(x, y, z)`
- `(x, y, z, w)`
## Vector operations
### Vector-Scalar operations
$$
\begin{pmatrix}
1\\
2\\
3
\end{pmatrix}+x\rightarrow
\begin{pmatrix}
1\\
2\\
3
\end{pmatrix}+
\begin{pmatrix}
x\\
x\\
x
\end{pmatrix}=
\begin{pmatrix}
1+x\\
2+x\\
3+x
\end{pmatrix}
$$
$$
\text{Where + can be + , - ,}\cdot\text{, }\div
$$
### Addition and subtraction
$$
\overline{a}=
\begin{pmatrix}
1\\
2\\
3
\end{pmatrix},\overline{b}=
\begin{pmatrix}
4\\
5\\
6
\end{pmatrix}
$$
$$
\overline{a}+\overline{b}=
\begin{pmatrix}
1+4\\
2+5\\
3+6
\end{pmatrix}=
\begin{pmatrix}
5\\
7\\
9
\end{pmatrix}
$$
$$
\overline{a}-\overline{b}=
\begin{pmatrix}
1-4\\
2-5\\
3-6
\end{pmatrix}=
\begin{pmatrix}
-3\\
-3\\
-3
\end{pmatrix}
$$
### Length
$$
\|\overline{v}\|=\sqrt{x^2+y^2}
$$
$$
\|\overline{v}\|=\sqrt{x^2+y^2+z^2}
$$
There is a special type of vector called a ==**unit vector**==, the length is always 1. We can calculate a unit vector $\hat{n}$ from any vector by dividing each of the vectors components by its length.
$$
\hat{n}=\frac{\overline{v}}{\|v\|}
$$
We call this **normalizing** a vector, they are generally easier to work with, especially when we only care about their directions.
### Vector-Vector multiplication
#### Dot product
The dot product of two vectors is equal to the scalar product of their lengths times the cosine of the angle between them.
$$
\overline{v}\cdot\overline{k}=\|\overline{v}\|\cdot\|\overline{k}\|\cdot\cos{\theta}
$$
If $\overline{v}$ and $\overline{k}$ are unit vectors, their length would be 1, which would reduce the formula to:
$$
\hat{v}\cdot\hat{k}=1\cdot1\cdot\cos{\theta}=\cos{\theta}
$$
An example of multiplying two unit vectors:
$$
\begin{pmatrix}
0.6\\
-0.8\\
0
\end{pmatrix}\cdot
\begin{pmatrix}
0\\
1\\
0
\end{pmatrix}=(0.6\cdot0)+(-0.8\cdot1)+(0\cdot0)=-0.8
$$
To calculate the angle between these vectors:
$$
\theta=\cos^{-1}({-0.8})=143.13
$$
#### Cross product
The cross product is only defined in 3D space and takes two non-parallel vectors as input and produces a third vector that is ==**orthogonal to both the input vectors**==. If both the input vectors are orthogonal to each other as well, a cross product would result in 3 orthogonal vectors.
$$
\begin{pmatrix}
A_x\\
A_y\\
A_z
\end{pmatrix}\times
\begin{pmatrix}
B_x\\
B_y\\
B_z
\end{pmatrix}=
\begin{pmatrix}
A_y\cdot B_z-A_z\cdot B_y\\
A_z\cdot B_x-A_x\cdot B_z\\
A_x\cdot B_y-A_y\cdot B_x
\end{pmatrix}
$$
# Matrices
Rectangular array of numbers
$$
\begin{bmatrix}
1&2&3\\
4&5&6
\end{bmatrix}
$$
## Matrix operations
### Addition and subtraction
Matrix addition and subtraction between two matrices is done on a ==**per-element basis**==. So the same general rules apply that we're familiar with for normal numbers, but done on the elements of both matrices with the same index. This does mean that addition and subtraction is ==**only defined for matrices of the same dimensions**==. A 3x2 matrix and a 2x3 matrix (or a 3x3 matrix and a 4x4 matrix) cannot be added or subtracted together.
$$
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix}+
\begin{bmatrix}
5&6\\
7&8
\end{bmatrix}=
\begin{bmatrix}
1+5&2+6\\
3+7&4+8
\end{bmatrix}=
\begin{bmatrix}
6&8\\
10&12
\end{bmatrix}
$$
$$
\begin{bmatrix}
4&2\\
1&6
\end{bmatrix}-
\begin{bmatrix}
2&4\\
0&1
\end{bmatrix}=
\begin{bmatrix}
4-2&2-4\\
1-0&6-1
\end{bmatrix}=
\begin{bmatrix}
2&-2\\
1&5
\end{bmatrix}
$$
### Matrix-Scalar multiplication
A matrix-scalar product multiples each element of the matrix by a scalar.
$$
2\cdot
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix}=
\begin{bmatrix}
2\cdot1&2\cdot2\\
2\cdot3&2\cdot4
\end{bmatrix}=
\begin{bmatrix}
2&4\\
6&8
\end{bmatrix}
$$
### Matrix-matrix multiplication
- You can only multiply two matrices if the number of columns on the left-hand side matrix is equal to the number of rows on the right-hand side matrix.
- Matrix multiplication is ==**not commutative**==: $A\cdot B\ne B\cdot A$
$$
\begin{bmatrix}
\color{red}1&\color{red}2\\
\color{green}3&\color{green}4
\end{bmatrix}\cdot
\begin{bmatrix}
\color{blue}5&\color{purple}6\\
\color{blue}7&\color{purple}8
\end{bmatrix}=
\begin{bmatrix}
\color{red}1\color{white}\cdot\color{blue}5\color{white}+\color{red}2\color{white}\cdot\color{blue}7&\color{red}1\color{white}\cdot\color{purple}6\color{white}+\color{red}2\color{white}\cdot\color{purple}8\\
\color{green}3\color{white}\cdot\color{blue}5\color{white}+\color{green}4\color{white}\cdot\color{blue}7&\color{green}3\color{white}\cdot\color{purple}6\color{white}+\color{green}4\color{white}\cdot\color{purple}8
\end{bmatrix}=
\begin{bmatrix}
19&22\\
43&50
\end{bmatrix}
$$
### Matrix-Vector multiplication
This is how you ==**transform**== a matrix
#### Identity matrix
In OpenGL we usually work with `4x4` transformation matrices for several reasons and one of them is that most of the vectors are of size 4. The most simple transformation matrix that we can think of is the identity matrix. The identity matrix is an `NxN` matrix with only 0s except on its diagonal. As you'll see, this transformation matrix leaves a vector completely unharmed:
$$
\begin{bmatrix}
\color{red}1&\color{red}0&\color{red}0&\color{red}0\\
\color{green}0&\color{green}1&\color{green}0&\color{green}0\\
\color{blue}0&\color{blue}0&\color{blue}1&\color{blue}0\\
\color{purple}0&\color{purple}0&\color{purple}0&\color{purple}1
\end{bmatrix}\cdot
\begin{bmatrix}
1\\
2\\
3\\
4
\end{bmatrix}=
\begin{bmatrix}
\color{red}1\color{white}\cdot1\\
\color{green}1\color{white}\cdot2\\
\color{blue}1\color{white}\cdot3\\
\color{purple}1\color{white}\cdot4
\end{bmatrix}=
\begin{bmatrix}
1\\
2\\
3\\
4
\end{bmatrix}
$$
#### Scaling
If we represent the scaling variables as $(\color{red}S_1\color{white},\color{green}S_2\color{white},\color{blue}S_3\color{white})$ we can define a scaling matrix on any vector $(x,y,z)$ as:
$$
\begin{bmatrix}
\color{red}S_1&\color{red}0&\color{red}0&\color{red}0\\
\color{green}0&\color{green}S_2&\color{green}0&\color{green}0\\
\color{blue}0&\color{blue}0&\color{blue}S_3&\color{blue}0\\
\color{purple}0&\color{purple}0&\color{purple}0&\color{purple}1
\end{bmatrix}\cdot
\begin{pmatrix}
x\\
y\\
z\\
1
\end{pmatrix}=
\begin{pmatrix}
\color{red}S_1\color{white}\cdot x\\
\color{green}S_2\color{white}\cdot y\\
\color{blue}S_3\color{white}\cdot z\\
1
\end{pmatrix}
$$
>[!info]
**Homogeneous coordinates** 
The `w` component of a vector is also known as a homogeneous coordinate. To get the 3D vector from a homogeneous vector we divide the `x`, `y` and `z` coordinate by its `w` coordinate. We usually do not notice this since the `w` component is `1.0` most of the time. Using homogeneous coordinates has several advantages: it allows us to do matrix translations on 3D vectors (without a `w` component we can't translate vectors).
Also, whenever the homogeneous coordinate is equal to `0`, the vector is specifically known as a **direction vector** since a vector with a `w` coordinate of `0` cannot be translated.

#### Translation
If we represent the translation variables as $(\color{red}T_x\color{white},\color{green}T_y\color{white},\color{blue}T_z\color{white})$ we can define the translation matrix by:
$$
\begin{bmatrix}
\color{red}1&\color{red}0&\color{red}0&\color{red}T_x\\
\color{green}0&\color{green}1&\color{green}0&\color{green}T_y\\
\color{blue}0&\color{blue}0&\color{blue}1&\color{blue}T_z\\
\color{purple}0&\color{purple}0&\color{purple}0&\color{purple}1
\end{bmatrix}\cdot
\begin{pmatrix}
x\\
y\\
z\\
1
\end{pmatrix}=
\begin{pmatrix}
x+\color{red}T_x\\
y+\color{green}T_y\\
z+\color{blue}T_z\\
1
\end{pmatrix}
$$
#### Rotation
Rotations in 3D are specified with an angle **and** a rotation axis. The angle specified will rotate the object along the rotation axis given.
##### Rotation around the X-axis
$$
\begin{bmatrix}
\color{red}1&\color{red}0&\color{red}0&\color{red}0\\
\color{green}0&\color{green}\cos{\theta}&\color{green}-\sin{\theta}&\color{green}0\\
\color{blue}0&\color{blue}\sin{\theta}&\color{blue}\cos{\theta}&\color{blue}0\\
\color{purple}0&\color{purple}0&\color{purple}0&\color{purple}1
\end{bmatrix}\cdot
\begin{pmatrix}
x\\
y\\
z\\
1
\end{pmatrix}=
\begin{pmatrix}
x\\
\color{green}\cos{\theta}\color{white}\cdot y -\color{green}\sin{\theta}\color{white}\cdot z\\
\color{blue}\sin{\theta}\color{white}\cdot y +\color{blue}\cos{\theta}\color{white}\cdot z\\
1
\end{pmatrix}
$$
##### Rotation around the Y-axis
$$
\begin{bmatrix}
\color{red}\cos{\theta}&\color{red}0&\color{red}\sin{\theta}&\color{red}0\\
\color{green}0&\color{green}1&\color{green}0&\color{green}0\\
\color{blue}-\sin{\theta}&\color{blue}0&\color{blue}\cos{\theta}&\color{blue}0\\
\color{purple}0&\color{purple}0&\color{purple}0&\color{purple}1
\end{bmatrix}\cdot
\begin{pmatrix}
x\\
y\\
z\\
1
\end{pmatrix}=
\begin{pmatrix}
\color{red}\cos{\theta}\color{white}\cdot x +\color{red}\sin{\theta}\color{white}\cdot z\\
y\\
\color{blue}-\sin{\theta}\color{white}\cdot x +\color{blue}\cos{\theta}\color{white}\cdot z\\
1
\end{pmatrix}
$$
##### Rotation around the Z-axis
$$
\begin{bmatrix}
\color{red}\cos{\theta}&\color{red}-\sin{\theta}&\color{red}0&\color{red}0\\
\color{green}\sin{\theta}&\color{green}\cos{\theta}&\color{green}0&\color{green}0\\
\color{blue}0&\color{blue}0&\color{blue}1&\color{blue}0\\
\color{purple}0&\color{purple}0&\color{purple}0&\color{purple}1
\end{bmatrix}\cdot
\begin{pmatrix}
x\\
y\\
z\\
1
\end{pmatrix}=
\begin{pmatrix}
\color{red}\cos{\theta}\color{white}\cdot x -\color{red}\sin{\theta}\color{white}\cdot y\\
\color{green}\sin{\theta}\color{white}\cdot x +\color{green}\cos{\theta}\color{white}\cdot y\\
z\\
1
\end{pmatrix}
$$

---
reference: "[[Introducing Python - Book]]"
chapter: "11"
---
>[!info]
>In Python, modules and packages are essential concepts for **organizing and structuring** code. They help **break down large programs into manageable and reusable components**.

# Modules
- A module in Python is like a small **toolbox** that contains a **collection of functions, variables and classes** that can be used in other Python programs.
- These elements are **grouped together in a single** file with a **.py extension**. Modules organize and encapsulate code, making it easier to manage and reuse.
## Creating a module
- You can create a module by **simply writing your Python code in a .py file**.
## Using a module
- To use a module in another Python file, you need to **import** it. You do this using the `import` statement.
``` Python
import module
```
- Once you have imported the module, you can access its functions and variables using **dot notation**.
``` Python
module.function()
module.variable
```
- You can import a module and assign an **alias**.
``` Python
import module as md
md.function()
md.variable()
```
- You can also import everything from a module using `*`.
	- This is **not always recommended** because it can cause **naming conflicts**.
``` Python
from module import *

function()
variable
```
# Packages
- A package is a ==**collection of modules**== grouped together **in a directory**. A package is like a folder that contains multiple modules.
- Its a way to organize related code more systematically.
## Creating a package
- To turn a directory into a package, you need to ==**include a special file called `__init__.py`**==.
	- This file can be empty.
- Packages can also contain **subpackages**.
## Using a package
``` Python
import package.module1
import package.module2

package.module1.function()
package.module2.variable
```
- This can be shortened by using the ==**`from`**== keyword.
	- This is used for importing **specific modules or attributes from a package or module**.
``` Python
from package import module1, module2

module1.function()
module2.variable()
```
# Libraries
- In Python, a library is a collection of pre-written code that provides a set of functions and tools to **perform common tasks** or **solve specific problems**.
- They typically consist of modules, packages, functions and classes that can be imported into your Python code to extend its capabilities.
## Using libraries
``` Python
import library
```
- You can also use **aliasing** for libraries
``` Python
import library as lib
import pandas as pd
import pygame as pg
import numpy as np
```
## Installing third-party packages/libraries
- There are packages/libraries that are written by other people.
- Before you can use a third-party package you need to install it using a **package manager**.
	- Pythons default package manager is called ==**pip**==.


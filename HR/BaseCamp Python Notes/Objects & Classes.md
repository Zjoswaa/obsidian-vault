---
reference: "[[Introducing Python - Book]]"
chapter: "10"
---
# Object-Oriented-Programming (OOP)
- Programming paradigm designed to make it easier to organize and manage complex code by modeling real-world entities as objects.
- The 4 pillars of OOP:
	- Inheritance
	- Polymorphism
	- Encapsulation
	- Abstraction
# Class
- A class is a **blueprint** or **template** for creating objects of a certain type.
- You can think of a class as a recipe for creating objects of a specific characteristics and behaviors.
- Classes define **attributes** (data) and **methods** (functions) that can be used by objects.
- Creating a class
``` Python
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name  # Attribute
		self.last_name = last_name  # Attribute

	def greet():  # Method
		print(f"Hello, I am {self.first_name}")
```
- It is a convention to write class names in **"CamelCase"**.
- The `init()` is used to **initialize** the objects attributes. It is also known as the **constructor** in other languages.
## Class Attributes
- There are **two types** of class attributes:
	- Class attribute
		- Is **unique to each class**
		- **Every instance** of this class will have the same class attributes
	- Instance attribute
		- Can be **different** for every instance of the class.
		- Access and modify instance attributes with the `self` keyword.
``` Python
class Car:
	# Class attribute
	fuel_type = "Gasoline"

	def __init__(self, color, make, model)
		self.color = color  # Instance attribute
		self.make = make  # Instance attribute
		self.model = model  # Instance attribute
```
## Class methods
- Methods are functions that an **object can perform**. These methods are **defined withing the class** and can **interact with the object's attributes**.
- In Python, when you define methods within a class, you use `self` as the **first parameter** in the method. This allows you to ==**access other instance attributes**== of the class.
# Object
- An object represents a **real-world** entity or concept.
- It is an **instance** of a class.
- Creating an object
``` Python
>>> person = Person("Joshua", "van der Jagt")  # Calls the init() function
>>> print(person.last_name)
van der Jagt
>>> person.greet()
Hello, I am Joshua
```
- An object is stored in a **variable**.
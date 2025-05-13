# MVC
- Model-View-Controller design pattern
- Modern web apps use the MVC pattern to allow:
	- Simultaneous development
	- Code reuse
- MVC partitions an application into tree parts
	- Model
	- View
	- Controller
## Model
- Two general ways to implement the Model
	- Tightly coupling the data-access code to a database provider like MySQL using SQL
	- Adding another abstraction layer, which is database provider independent, using object-relational mapper (**ORM**)
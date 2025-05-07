- A **database** is a collection of related data
	- **Data** means known facts that can be recorded and that have implicit meaning
# Data Modeling
- A **data model** is a collection of concepts that can be used to describe the **structure of a database**
	- The structure means the data types, relationships and constraints that apply to the data
- **High-level** or **conceptual data models**
- **Low-level** or **physical models**
- **Representational** or **implementational** models
# Entity
- An entity is described using a set of attributes
- The values given for the attributes makes it distinguishable
- An **attribute** represents some property of interest that further describes an entity, such as the employee's name or salary
# Primary Key
- A primary key is a **minimal** set of attributes whose values uniquely identity an entity in the set
- Unique, not null, immutable, singular (can be composite)
# Relationship
- A **relationship** is an association among the entities
- A **relationship set** is a collection of **relationships** all belonging to one **relationship** type
- A set of relationships involving the same entity sets is defines as a **relationship set**
# Foreign Key
- A set of attributes that reference the primary key of another relation
	- **Reference** means that each value in the foreign key must be found in the primary key of the other relation
# Cardinality
- The cardinality of a join between two tables is the **numerical relationship between rows in one table and rows in the other**
	- one-to-one, 1:1
	- one-to-many, 1:M
	- many-to-many, M:M

# Subsystems
- Most dynamic web applications pass data to one or more **subsystems**
	- SQL database
	- Operating systems
	- Libraries
	- Shell command interpreters
	- etc.
- We communicate with these subsystems by building **strings** that contain some **control information** and some **data**
- In such cases, the subsystems contain a **parser** which decodes incoming strings character by character, and decides what to do based on what it reads
## Metacharacters
- When our application passes data around, the strings may reach a system in which one or more of the characters **are not treated as plain text**, but as something **special**
### What is the risk
- They do not pose any threat by themselves
- The problems is raised when developers **think** they are passing pure **data**, and those ‘‘data’’ are found to contain characters that **make the subsystem do something else than we expect**
- When the subsystem parser reaches a metacharacter, it stops reading pure data, and may instead start reading commands: **The parser switches context**
# SQL Injection
- In SQL Injection, an attacker is able to **modify** or **add** queries that are sent to a database by **playing** with input to the web application
- The attack works when a program builds queries based on strings from the client, and passes them to the database server **without** handling characters that have special meaning to the server
## Preventing SQL Injection
- We should make metacharacters lose their special meaning, either by handling them **manually** or by building queries in a way in which there are **no metacharacters**
	- Neutralizing SQL metacharacters
	- Prepared statements
## Prepared statements
- A "blueprint" of the query is created by the developer, only the data that needs to be inserted is missing.
- A method is called to insert data into this prepared statements, this does certain checks on illegal characters automatically
# Shell Injection
- Programs written in web programming languages, such as Perl and similar languages often rely heavily on running **external commands** to perform many tasks
- When a Perl program runs an external command, the interpreter will in many cases leave the actual running of the program to an operating system shell, such as `sh`, `bash`, `csh` or `tcsh`.
- Unfortunately, **shells** typically understand a large set of **metacharacters**, and one risks major security problems **if one doesn’t do any filtering**
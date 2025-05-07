---
reference: "[[Introducing Python - Book]]"
chapter: "16"
---
# Types of structured data
- **CSV** - Data separated with a **delimiter/separator** like a tab, comma or vertical line.
- **XML** / **HTML** - Tags surrounded by `<` and `>`.
- **JSON** - Data stored as key-value pairs, contains characters like `{`, `}` and `:`.
- **YAML** - Indentation
- Other
# CSV
- Comma Separated Values
- Best to use the `csv` module because parsing can be difficult.
	- Alternate delimiters.
	- Escape sequences.
	- Files have different line endings based on operating system.
	- The first line may contain column names.
## Reading from a CSV file (List of Lists)
- Using `newline=""` and `encoding="utf-8"` is recommended.
``` Python
import csv

with open("file.csv", "rt", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)
    data = list(reader)
print(data)
```
## Reading from a CSV file (List of Dictionaries)
``` Python
import csv  
  
with open("file.csv", "rt", newline="", encoding="utf-8") as file:  
    reader = csv.DictReader(file)  
    data = list(reader)  
print(data)
```
## Writing to a CSV file (List of Lists)
- Using `newline=""` and `encoding="utf-8"` is recommended.
``` Python
import csv

villains = [
	["first_name", "last_name"],
	["Doctor", "No"],
	["Rose", "Klebb"],
	["Mister", "Big"],
	["Auric", "Goldfinger"],
	["Ernst", "Blofeld"]
]

with open("file.csv", "wt", newline="", encoding="utf-8") as file:  
    writer = csv.writer(file, delimiter=",")
    writer.writerows(villains)
```
## Writing to a CSV file (List of Dictionaries)
- Using `newline=""` and `encoding="utf-8"` is recommended.
``` Python
import csv  
  
villains = [
    {"first_name": "Doctor", "last_name": "No"},
    {"first_name": "Rose", "last_name": "Klebb"},
    {"first_name": "Mister", "last_name": "Big"},
    {"first_name": "Auric", "last_name": "Goldfinger"},
    {"first_name": "Ernst", "last_name": "Blofeld"}
]

with open("file.csv", "wt", newline="", encoding="utf-8") as file:
    writer = csv.DictWriter(file, ["first_name", "last_name"])
    writer.writeheader()
    writer.writerows(villains)
```
# JSON
- JavaScript Object Notation
- Use the `json` module.
## Reading from a JSON file
- Using `encoding="utf-8"` is recommended.
``` JSON
{  
  "emp_details": [
    {
      "emp_name": "Shubham",
      "email": "ksingh.subh@gmail.com",
      "job_profile": "intern"
    },
    {
      "emp_name": "Gaurav",
      "email": "gaurav.singh@gmail.com",
      "job_profile": "developer"
    },
    {
      "emp_name": "Nikhil",
      "email": "nikhil@hotmail.com",
      "job_profile": "full-time"
    }
  ]
}
```
``` Python
import json

with open("file.json", "r", encoding="utf-8") as file:
    data = json.load(file)
    print(data)
```
``` Python
def read_from_json(file_name: str) -> dict:
    with open(file_name, "r", encoding="utf-8") as file:
        return json.load(file)
```
```
{'emp_details': [{'emp_name': 'Shubham', 'email': 'ksingh.subh@gmail.com', 'job_profile': 'intern'}, {'emp_name': 'Gaurav', 'email': 'gaurav.singh@gmail.com', 'job_profile': 'developer'}, {'emp_name': 'Nikhil', 'email': 'nikhil@hotmail.com', 'job_profile': 'full-time'}]}
```
## Writing to a JSON file
- Using `encoding="utf-8"` is recommended.
``` Python
import json

data = {
    "emp_details":
        [
            {"emp_name": "Shubham",
             "email": "ksingh.subh@gmail.com",
             "job_profile": "intern"
             },
            {"emp_name": "Gaurav",
             "email": "gaurav.singh@gmail.com",
             "job_profile": "developer"
             },
            {"emp_name": "Nikhil",
             "email": "nikhil@hotmail.com",
             "job_profile": "full-time"
             }
        ]
    }

with open("file.json", "w", encoding="utf-8") as file:  
    json.dump(data, file, ensure_ascii=False, indent=2)
```
``` Python
def write_to_json(data: dict, file_name: str):
    with open(file_name, "w", encoding="utf-8") as file:
        json.dump(data, file, ensure_ascii=False, indent=2)
```
``` JSON
{  
  "emp_details": [  
    {  
      "emp_name": "Shubham",  
      "email": "ksingh.subh@gmail.com",  
      "job_profile": "intern"  
    },  
    {  
      "emp_name": "Gaurav",  
      "email": "gaurav.singh@gmail.com",  
      "job_profile": "developer"  
    },  
    {  
      "emp_name": "Nikhil",  
      "email": "nikhil@hotmail.com",  
      "job_profile": "full-time"  
    }  
  ]  
}
```
# Pandas
- Pandas is a library that supports reading and writing many file formats.
	- **CSV**
	- **Fixed-width text**
	- **Excel**
	- **JSON**
	- **HTML**
	- **SQL**
	- **HDF5**
	- **Others**
- Group, split, merge, index, slice, sort, select, label
- Convert data types
- Change size or shape
- Handle missing data
- Generate random values
- Manage time series

- Pandas' read functions return a `DataFrame` object. Pandas' standard representation for two-dimensional data.
- Its one-dimensional version is called a `Series`
## Read CSV with Pandas
``` Python
import pandas  
  
data = pandas.read_csv("file.csv")  
print(data)
```
```
  first_name   last_name
0     Doctor          No
1       Rose       Klebb
2     Mister         Big
3      Auric  Goldfinger
4      Ernst     Blofeld
```
## Read JSON with Pandas
``` Python
import pandas  
  
data = pandas.read_json("file.json")  
print(data.to_string())
```
```
                                                                             emp_details
0     {'emp_name': 'Shubham', 'email': 'ksingh.subh@gmail.com', 'job_profile': 'intern'}
1  {'emp_name': 'Gaurav', 'email': 'gaurav.singh@gmail.com', 'job_profile': 'developer'}
2      {'emp_name': 'Nikhil', 'email': 'nikhil@hotmail.com', 'job_profile': 'full-time'}
```

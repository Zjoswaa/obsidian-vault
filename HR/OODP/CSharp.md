## Data types
- `char` - 16 bit
- `int` - 32 bit
- `float` - 32 bit
- `double` - 64 bit
- `bool` - 8 bit
- `string`
## JSON
- You need the `Newtonsoft.Json` package.
### Reading a `double`
``` C#
using Newtonsoft.Json;

StreamReader reader = new StreamReader(fileName);
string jsonString = reader.ReadToEnd();
reader.Close();
var fromjson = JsonConvert.DeserializeObject<double>(jsonString)!;
```
### Writing a `double`
``` C#
using Newtonsoft.Json;

StreamWriter writer = new StreamWriter(fileName);
writer.Write(JsonConvert.SerializeObject(valueToWrite));
writer.Close();
```
### Reading an object
``` C#
using Newtonsoft.Json;

StreamReader reader = new(fileName);
string File2Json = reader.ReadToEnd();
List<CLASSNAME> listOfObjects = JsonConvert.DeserializeObject<List<CLASSNAME>>(File2Json)!;
reader.Close();
```

### Writing an object
``` C#
using Newtonsoft.Json;

StreamWriter writer = new(fileName);
string List2Json = JsonConvert.SerializeObject(listOfObjects);
writer.Write(List2Json, Formatting.Indented);
writer.Close();
```

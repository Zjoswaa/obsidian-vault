# Hash table
``` C#
h(k) = ToUpper(k[0]) - 'A'
index(k) = abs(h(k)) % length
```
## Linear probing
``` C#
p(k, i) = (index(k) + i) % length
```
- When there is a **collision** (multiple keys have the same output of the hash function), you shift the item up linearly until there is a free spot
## Quadratic probing
``` C#
p(k, i) = (index(k) + i^2) % length
```
- When there is a **collision** (multiple keys have the same output of the hash function), you shift the item up quadratically until there is a free spot
## Probing problem
The problem with probing is that when the load factor becomes bigger, the time to find a free spot becomes bigger too. Where `load factor = #entries / length`

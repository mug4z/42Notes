## void

- void represent no data.
- void w**ith pointer**, declare a pointer but without specifying which data type it is pointing to
```
void* vague_pointer
```
### Null pointer constant
```
(void*)0
```
## size_t
- C'est le type rendue par l'operation sizeof.
- Similaire un `unsigned int` ou `unsigned long` ça dépand du système.
- Avantage quand on loop sur un index on est garantie que size_t peut contenir l'ensemble de n'importe quel array contrairement a int.
[[Structure]]
## Type casting
Permet de changer le type d'une variable 
Ex conversion d'un `int` à un `unsigned char`
```
int c;
unsigned char character;
character = (unsigned char)c;
```

## Create new names for data types


# Sources
[[Source]]
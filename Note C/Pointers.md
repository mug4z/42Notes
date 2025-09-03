### Pointers
Contien L'addresse d'une donner
Permet de modifier une donner dans une fonction. Sans pointeur on ne fait que des copie de donnees et le scope des fonction font que les donner a l'interieur sans pointeur sont detruite

Avantages:
- Modifier des donner dans une fonction
- Evite la copie

```
type *name; 
int *p;
p contient l'address d'une variable int
```
#### Use
```
int *p; // Declare le pointeur
p = &a // initialize le pointeur
*p = 1 <-> a = 1
Si p contient l'addresse de a alors *p est la meme
*name c'est l'objet de type type, l'addresse du'ou c'es stocker dans nom.
```

The **&** operator only applies to objects in memory: variables and array elements. It cannot be applied to expressions, constants, or register variables.

```
mon_pointeur : adresse de la valeur pointer.
*mon_pointeur : valeur de la variable pointer.
&mon_pointeur : addresse du pointeur.
```

### Function and pointers
- Faire passer une valeur d'une variable dans une fonction, -> on passe l'adresse.
```c
void ft_1 (int *a)
{
	*a = 42;
}
int main(void)
{
	int a;
	ft_1(&a)
}
```
- Faire passer un pointeur dans une fonction (qui prend en parameter un pointeur) on passe l'adresse de la valeur pointé.
```c
void ft_1(int *a)
{
	*a = 42
}
int main(void)
{
	int a;
	int *ptr
	ptr = &a
	ft_1(ptr)
}
```

### Pointer arithmetic
```
int tab[42]; and p = &(tab[0]);
tab[x] <-> *(p+x)
p[valeur] 
```
### Control structures
```c
	if(expression)
		instruction
	else
		instructions
```

## Pointer Null
Tout simplement assigner la valeur NULL ou 0 a un pointer.
```c
int *ptr = NULL;
```

## Static pointer

## Void pointer
Un pointer générique qui peut prendre n'importe quelle type de donées.
Syntax
```c
void *ptr_name;
```
Exemple:
```c
int main() {
    int x = 10;
    
    // Declare a void pointer
    void *ptr;
    
    // Assign the address of x to the void pointer
    ptr = &x;
    
    return 0;
}
```
Pour pouvoir utiliser la donné a l'intérieur on doit type casté vers le type voulue (int * , char * ..)
# Source

[[Note C/Source|Source]]
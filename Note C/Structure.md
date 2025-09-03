Les structure permettent de regrouper un ensemble de donnée.
C'est un [[Data Types]] qui est définie par le programmeur, elle est composé de différente type de donnée. Elle peut aussi inclure d'autre structure.

Une structure ce définie par le mot `struct` et on indique ces `membres` comme avec les variables en indiquant son type et son nom. (Le nom est optionel mais si on ne nomme pas la structure on ne peut pas si référer)
```c
struct point // Nom de la structure
{
	int x; // Membre x
	int y; // Membre y
};
```

On peut déclarer les variables d'un type structure quand on définie la structure.
```c
struct point // Nom de la structure
{
	int x; // Membre x
	int y; // Membre y
} first_point, second_point; // Varaibles
```

On peut aussi le faire après la définition
```c
struct point // Nom de la structure
{
	int x; // Membre x
	int y; // Membre y
}newNodestruct point fist_point,second_point;
```

## Initialization des membres de la structure
Quand les membres de la structure sont initialisé, les valeurs corresponde au membres dans l'ordre de leur déclaration.
```c
struct point // Nom de la structure
{
	int x; // Membre x
	int y; // Membre y
}
struct point fist_point = {5, 10} // x = 5, y = 10
```

## Accédé a une valeur dans une structure
Quand la structure n'est pas un pointeur
```
first_point.x // 5
```
Quand la structure est un pointeur
```
first_point -> x // 5
```


## Modifier une structure.
 Quand on modifie une structure on doit `make re` pour bien recompiler avec le changement.
---

# Source
[[Source]]
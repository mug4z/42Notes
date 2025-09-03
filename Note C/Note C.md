
gcc -D<macroname>=<value> -> permet de changer la valeur d'une macro

When print NULL pointer is undefined behavior so it up to the compiler or library to handle it.
## Priorité des operation
En C, l'opérateur de déréférencement `*` (qui est utilisé pour accéder à la valeur pointée par un pointeur) a une priorité plus basse que l'opérateur d'accès aux membres d'une structure via un pointeur `->`. Cela signifie que si vous n'utilisez pas de parenthèses, l'expression serait interprétée incorrectement.
pages 50 du livres the c programming language

---- 
atoi calcule `res = 10 * res + (str[i] - '0');`
## Diff between mem functions an str functions
Exemple: memcmp and strcmp
strcmp : Compare Null terminated string
memcmp: Compare binary bytes buffers on N bytes

Exa 
Consignes
rendre fonction main uniquement quand demander un programme.
moulinette utilise ces flags -Wall -Wextra -Werror et gcc
Si code compile pas -> 0

## Miscealenous
- `\0` -> character 0 and null terminator
- `\n` -> newline

## Data type
void represent no data.
void w**ith pointer**, declare a pointer but without specifying which data type it is pointing to
```
void* vague_pointer
```


## Norme

## GCC
### Options
- -o fichier_sortie : Permet de specifier un nom du fichier a executer avec compilation
- -c : Permet de générer des fichier .o a partir des fichiers .c . 
## Prototype
Declare un nom d'une fonction ces parametres et son type de retour avant la declaration de la fonction.

## Variable Scope
## Taille

### Local 
### Global

## Write
Prend des bits en entrer et ensuite les envoyer ou c'est demander
Pour les code prendre la tables ASCII pour savoir quoi afficher.

## Compilation
Flag de gcc
```
gcc -Wall -Wextra -Werror -o 
```
**-Wall**
Les options de Warnings activées sont les suivantes :  
- -Waddress
- -Wc++0x-compat
- -Wchar-subscripts
- -Wenum-compare
- -Wimplicit-int
- -Wimplicit-function-declaratino
- -Wcomment
- -Wformat
- -Wmain
- -Wmissing-braces
- -Wnonnull
- -Wparentheses
- -Wpointer-sign
- -Wreorder
- -Wreturn-type
- -Wsequence-point
- -Wstrict-aliasing
- -Wstrict-overflow=1
- -Wswitch
- -Wtrigraphs
- -Wuninitialized
- -Wunknown-pragmas
- -Wunused-function
- -Wunused-label
- -Wunused-value
- -Wunused-variable
- -Wvolatile-register-var

**-Wextra** : Affiche encore plus de warnings

Les options de Warnings activées sont les suivantes :  

- -Wclobbered
- -Wempty-body
- -Wignored-qualifiers
- -Wmissing-field-initializers
- -Wmissing-parameter-type
- -Wold-style-declaration
- -Woverride-init
- -Wsign-compare
- -Wtype-limits
- -Wuninitialized
- -Wunused-parameter
- -Wunused-but-set-parameter
**-Werror** : Considère les warnings comme des erreurs et cesse la compilation

Verification du c_00
Nom ->  OK
Norminette -> OK
file name in Header -> 
ex00 -> ok
ex01 -> ok
ex02 -> ok
ex03 -> ok
ex04 -> ok



### C_00 Ex05
Input -- rien
-> Pattern est que
012 .. 789
le 3 chiffre > le 2 > le 1

Output -- conbinaison unique de 3 chiffres 789 et 987 ne doivent pas etre present.

# Note C en 42 min
CPU
RAM 
Interface (peripherique)

C -> OS -> Hardware

## Type:
Sont typer de base les unisgned sont specifiquement indiquer
- char: 
- * : pointeur

## Type composer
Arrays
```
type name[numeric_value];
int tab[42];
```

Structure
```
struct struct_name

struct s_fortytwo
{
	int a;
	char b[21];
};
```
Declaration
```
struct struct_name name; struct s_fortytwo a;
```

En declarant ces types de donnes on reserve la place en memoire.

## Entry point
Point de depart du programme -> fonction main.
## Instructions
### blocks
```
{
	declarations;
	instructions;
}
```

## Expressions
An expression is a computation that always evaluates to a numerical value
### Immediate numerical values:
0 42 0x1A 010

### Variables
a
b[18]
sft_var.a > cherche l'element dans la structure.
Evalue la valeur contenue dedans.

### Functions call
sum(18, a)

Prototype de fonction
Permet au compilateur de pouvoir appeler une fonction peut importe ou elle est dans le code.
```
type func_name(arguments...);
int plus_one(int nbr1, int nbr2);
```

Permet aussi de pouvoir appeler des fonction depuis d'autres fichiers, a condition de compiler le fichier qui contient la fonction.

### Comupations: + - * / % ()

### Assignations:
a = 42
b[2 + a] = sum(12, 30)

### Control structures
Permet de controler le deroulement d'une instruction a l'interieur d'un block.

### Comparisons
1 = true, 0 = false > si comparaison juste rend 1 sino rend 0
= : eguale
!= : not eguale
< : plus petit que  > : plus grand que
<= plus petit que ou eguale >= plus grand ou eguale
|| : ou
&& : et
! : not

### Binary operator

### Shortcuts

### Special
'A' -> 65
sizeof(type_of_var) -> renvoye la taille d'une var en memoire
&a (address of variable a in RAM)
 
### Strings
"hello forty-two" -> alloue en memoire les charactere entre les guillements rajoute un 0 a la fin et renvoye l'addresse du premier charactere

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
```
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
```
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
```
	if(expression)
		instruction
	else
		instructions
```
### The while
```
while (expression)
	instruction
```
si vaut 0 on arrete, si vaut 1 on refait l'instruction
### The return

```
return(expression);
return;
```

MMU ?
Swap ?
Memoire haute -> stack (Pile)?
	- quand fais `int a;` on alloue 4 octet (ou 8 sa depend de l'architecture) sur la stack.
	- plus on ajoute d'element plus on descend dans la stack.
Memoire basse -> heap (tas )?
On definie un pointeur comme sa
```
int *ptr;
```
Et on l'assigne comme sa 
```
ptr = &a;
```

## include
Indique que le fichier ce trouve dans le dossier des header standard.
```
include <file>
```

Indique que le fichier header est dans le dossier courant. (ou specifier a la compilation grace a -I)
```
include "file"
```
## Increment
++ (increment) or -- (decrement)
Peuvent etre utiliser en prefix -> ++variable_name, --variable_name
Ou en sufix -> variable_name++ , variable_name--

++variable_name -> increment la variable avant que sa valeur soit utiliser
variable_name++ -> increment la variable apres que sa valeur soit utiliser
Exemple
```
int x;
int n;

n = 5;
x = 0;

x = ++n // x est 6
x = n++ // x est toujours eguale a 5


```


## argc et argv
Demande de verifier 
- argc -> nombre de parametre du programme
- ``**argv``-> contient les parametre qui suit le binaire (programme)
	- `[0] contient le nom du binaire`
```
int main(int argc, char **argv)
{
	
}
```

## Tableaux
**Les addresse d'un tableau se suivent.**
Tableau est un pointeur vers son premier element.
Declare tableaux
```
<type> <nom_tableau>[X]; // Declare avec valeur aleatoire 
```
Initialization tableaux
```
int tableau[5] = {0} // met tout a 0
MAIS
int tableau[5] = {4} // met le premier element a 4 et ensuite le reste a 0
```
Acces au tableaux
```
tableau[x] : element d'indice X

tableau : adresse du tableau
*tableau : valeur du premier element du tableau
*(tableau + X) : Element d'indice X
```
 Remplir une valeur du tableau
 ```
 tableau[0] = 42; // Remplie la premiere valeur du tableau avec la valeur 42
```
Afficher le tableau
```
while (index++ < 5)
{
	printf("%d%,tableau[index])
}
```
Envoyer un tableau dans une fonction.
```
void afficher_tableau(int *tab, int taille)
{
}

int main(void)
{
	int tableau[5] = {0}
	afficher_tableau(tableau, 5)
}

OU 
void afficher_tableau(int tab[], int taille)
{
}

int main(void)
{
	int tableau[5] = {0}
	afficher_tableau(tableau, 5)
}

```
Return tableau
Creer une variable static et permet de retourner un tableau.

Faire une tableau de pointer sur char (version avec `[]`)
```
int main (void)
{
    char *a[] = {"Hello","World","!"};
}
```

Tableau en 2 dimensions
```
int damier[][]; type nom_tab[ligne][colonne]

// parcours le tableau a 2 dimensions
while (i < lignes){
	while(j < collones)
	{
	
	}
}
```


## Chaine de charactere (string)
String constants need not be function arguments. If pmessage is declared as char *pmessage;

then the statement

```
pmessage = "now is the time"; 
```

assigns to pmessage a pointer to the character array. This is **not a string copy**; only pointers are involved. C does not provide any operators for processing an entire string of characters as a unit.

The first function is strcpy(s,t), which copies the string t to the string s. It would be nice just to say s=t but this copies the pointer, not the characters. To copy the characters, we need a loop.



## Recurisiviter
Recursiviter : le principe.
La recurtion c'est quand la fonction ce rappel elle meme.
Fonction iterative -> Fonction classique (qui ne se rappel pas).
!!! Etablir des points d'arret!!! sinon boucle a l'infinie.
!!! Bien gerer les cas d'erreur !!!

Une fonction qui se rappel elle meme.
## Converstion 
Convertir les chiffre de 0 -> 9
- Convetir un char -> int : char_v + '0'
- Convertir un int -> char : int - '0'

## Define
Cree des constante qui permette d'avoir un text pour une valeur.
Permet de clarifier le code.

# Source
[[Source]]

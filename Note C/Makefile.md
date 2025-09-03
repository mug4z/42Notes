- Pour pouvoir utiliser make crée un fichier Makefile
- Le fichier makefile est la pour dire a make comment compiler et link un programme.

Syntax
```
cible: prerequis prerequis
	recipe
```
- Cible: un fichier ou une action
- Prerequis : fichier utiliser comme input pour crée la cible. Une cible dépend souvent d'une multitude de fichiers
- Recipe: action que make execute.
Cette ensemble s'appel une `rule`

ATTENTION , des cible peuvent ne pas avoir de prerequis comme par exemple `clean`

## Phony Targets
Une phony target est un règle qui n'ai pas le nom d'un fichier mais le nom d'un groupe de commande. Ce/Ces commandes seront executé a chaque fois que la cible sera remake.

Exemple de `clean` :
```
clean:
	rm *.dSYM
```
- Une fois `make clean` la command `rm *.dSYM` sera executé
Le problème avec cette méthode est que si un fichier s'appel déjà clean, la cible sera considérer comme a jour.
Pour éviter ça on ajoute une cible spéciale `.PHONY`
```
.PHONY: clean fclean all ... // on peut definir plusieur en une seule ligne
clean:
	rm *.dSYM
```
 Les prerequis de .PHONY sont toujours considérer comme des cibles jamais comme des pattern (même avec % dedans)

## Variables
Le nom d'une variable ne peut pas contenir : `: # =`  ou d'espaces
Déclarations
```
nom_variable = valeur 
```

Utilisé la variable 
```
$(nom_variable)
```

### Automatic variable
Ces variables on uniquement une valeur au sein du recipe.
Voici quelques variable automatique
- $@ -> nom du fichier de la cible ou de la rule.
- $^   -> nom de tout les prerequisite espacé par un espace.

ATTENTION, elles ne peuvent pas être utiliser dans les prerequisites d'une rule.

liste des [variable automatique](https://www.gnu.org/software/make/manual/make.html#Automatic-Variables)
## Pattern Rules
On peut ajouté des wildcard dans les  prerequisite  en ajoutant `%` 
Ex: `%.c` tout les fichier terminant par .c . On dit que la partie match par `%` est le stem.
```
$(objects): %.o: %.c
    $(CC) -c $(CFLAGS) $< -o $@
```

## Function Wildcards
Les wildcard sont automatiquement ajouter au sein des rules, mais elles ne sont pas ajouté quand:
- Quand une variable est seté
- A l'intérieur d'un arguments d'une fonction
Donc pour utiliser les wildcards dans ces endroits on utilise
```
$(wildcard pattern…)
```
Ex: prend tout les fichiers .c
```
$(wildcard *.c)
```
## Functions for String Substitution and Analysis
Trouve des mots séparer par des espaces qui match le pattern et remplace les avec replacement
```
$(patsubst pattern,replacement,text)
```

Ex: Prend la liste de fichier .c  définie dans la variables SRC et les remplace en .o 
```
SRC = main.c ft_isalnum.c ft_isalpha.c ft_isdigit.c
$(patsubst %.c,%.o,$(SRC))

RESULT -> main.o ft_isalnum.o ft_isalpha.o ft_isdigit.o
```

## Implicit Rules

Il y a des rule que make fait de lui même en fonction des extension de fichier.
La compilation c prend des .c et les transforme en .o  donc make fait ça automatiquement quand il voit ces deux extensions.

Voici la liste des variables utilisé dans les  [règles implicite](https://www.gnu.org/software/make/manual/make.html#Implicit-Variables)


## Submakefile
Permet depuis un makefile de lancer d'autre makefile

Exemple:
```
$(MAKE) [command] -C path/to/directory
```

## Debuging makefile 
### info command
Can print a variable while the makefile is being red.
`$(info $$DATA = $(DATA))`
	-> $DATA = some_data
### error command
Stop the makefile at a certain point and print the data inside a given variable.
`$(error $$DATA = $(DATA))`
# Source
[[Source]]

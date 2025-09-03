-  Fichier ce terminant par .h
- Contient des prototypes de fonction.

Permet d'utiliser des fonctions qui viennent de different fichier.

1. Crée le fichier de la fonction ex: ft_isalpha.c
2. Ecrire la fonction
3. Crée le fichier header
5. Mettre les prototype de la fonction ex `int ft_isalpha(int c);`
6. Dans un fichier main inclure le header  ex `#include"fichier.h"`
7. Compiler avec tout les fichier ex `gcc -Wextra -Wall -Werror -o result ft_isalpha.c main.c`

ATTENTION si on ne met pas le prototype de la fonction dans le header on aura l'erreur undefined.

ATTENTION si on met un prototype fonction dans le header on ne peut pas réutiliser ce nom dans un autre fichier de fonction sinon erreur -> 
```
duplicate symbol '_ft_isalpha' in:`
	/var/folders/zz/zyxvpxvq6csfxvn_n000cdy80033gk/T/ft_isalnum-1c2b2e.o
    /var/folders/zz/zyxvpxvq6csfxvn_n000cdy80033gk/T/ft_isalpha-49b736.o
duplicate symbol '_ft_isdigit' in:
    /var/folders/zz/zyxvpxvq6csfxvn_n000cdy80033gk/T/ft_isalnum-1c2b2e.o
    /var/folders/zz/zyxvpxvq6csfxvn_n000cdy80033gk/T/ft_isdigit-86bae1.o
ld: 2 duplicate symbols for architecture x86_64
```

On peut aussi y ajouter des commande de preprocesseur -> [[Préprocesseur]]

# Source
[[Source]]
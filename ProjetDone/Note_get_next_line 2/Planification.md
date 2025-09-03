## Recherche
- Variable statique ? -> OK 
- Descripteur de fichier ? -> OK
- function read ? -> OK
- option -D  compilation change macro buffer_size ? -> OK
- Comment rendre buffer qui acceuille le retour correctement dimensionner.
	- pointer de pointer ?

## INTERDIT
- Variable globale.
- lseek()
- La libft

**VOIR la logique de comment fonction fgets et getline pour la reproduire.**
## TODO
- Revoir la structure du code en entier.
	- Logique générale :
	1. read le nombre du buffer
	2. sauver dans la stash en static
		1. si la stash est remplie faire un join
	3. regarder dans la stash si on a un `\n` strchr()
		1. read si il y a pas
	4. si `\n` on extrait la ligne  avec le `\n`
	5. Enlever ce qu'on vient d'extraire.
## Implementation
But : Lire un fichier ligne par ligne. rend NULL si plus rien a lire ou erreur.
- rendre gnl indépendant du BUFFER_SIZE, dans le sens que peut importe sa taille on retour ligne par ligne.
- ATTENTION à BUFFER_SIZE = 0
- read line
	- read lit le nombre du buffer donc une ligne ou pas
	- check line
- extract line / getline
	- Une ligne est séparer par un `\n`
	- Analyser le buffer modifier par read.

- Si le fichier pointer par le descripteur de fichier change au cours de deux appel de get_next_line -> UNDEFINED behaviour

### Read the buffer


## OK
BUFFER_SIZE est une macro a mettre sans doute dans le .h -> OK
	- Default value: comme je veux
	- Doit pouvoir changer avec le flag -D
	- Mon projet doit pouvoir compiler avec ou sans -D
	- Exemple de compilation: `cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 .c`
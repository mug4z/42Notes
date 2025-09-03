## Recurisiviter
### Principe
Recursion est un process ou une fonction s'appel elle même directement ou indirectement.
Exemple
```
int fun()
{
...
fun ();
}
```

Called and caller
Quand une fonction recursive s'appel elle même elle ajoute a chaque call une etape dans la stack.
Quand la condition de sortie est juste. La valeur retourner est envoyer a son caller dans la stack et ainsi de suite

Exemple:
```c
#include <stdio.h>

int fun(int n)
{
	if (n==0)
	{
		return 1;
	}
	else
		return 7 + fun(n-2);
}
int main(void)
{
	printf("%d",fun(4);
	return 0;
}
```

## Mémoire
Quand la 

La recurtion c'est quand la fonction ce rappel elle meme.
Fonction iterative -> Fonction classique (qui ne se rappel pas).
!!! Etablir des points d'arret!!! sinon boucle a l'infinie.
!!! Bien gerer les cas d'erreur !!!

## Source
[[Source]]
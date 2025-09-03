Une directive de préprocesseur commence toujours par un `#`
## Directives
- `#ifndef` -> Retourne true si une macro n'est pas définie
- `#define` -> Permet de définir une macro
- `#endif`   -> Termine le bloque commencé par `#ifndef/#ifdef`

## Macro
Un fragment de code auquel on donne un nom, quand ce nom est utiliser il est remplacer par ce qu'il contient.

Les directives de preprocessor peuvent être définie dans un fichier [[Headers]]

## Once-only header
Si un fichier header est inclue plus d'une fois le compilateur le processera deux fois. Sa posera sans doute problème. Si sa pose pas de problème sa fera perdre du temps. C'est pour sa qu'on peut ajouter le code ci-dessous.
```
#ifndef LIBFT_H
# define LIBFT_H

int	ft_isalnum(int c);
int	ft_isalpha(int c);
int	ft_isdigit(int c);
#endif
```
Quand le header sera de nouveau inclue la conditions sera fausse parce que LIBFT_H est définie le preprocesseur ignora cette partie et le compilateur ne le verra pas deux fois.
# Source
[[Source]]
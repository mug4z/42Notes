## Liste chainées

```
typedef struct s_list // s_list est le nom de la structure
{
	void          *content;
	struct s_list *next;
}                 t_list; // correspond au typedef au dessus donc t_list == struct s_list.
```

next : est un pointer vers une structure tout simplement parce que le prochain element dans la liste est une structure.

Pour ajouter en debut
Logique:
	1. Dire a la nouvelle node de que son next pointe sur la head
	2. Definir la head comme la nouvelle node
# Source 
[[Source]]
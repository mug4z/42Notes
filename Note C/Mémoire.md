## Allocation dynamique
Malloc alloue de la memoire dans la heap.
```
malloc(Taille en octet) : Alloue dynamiquement la taille en octets d'une donner
sizeof(donnee)          : Allouer dynamiquement une zone memoire.
free (donner_allouee)   : libère la mémoire allouée dynamiquement.
```
Pour chaque malloc doit correspondre un free.


La memoire est une liste ordrée de locations qui enregistre de la mémoire(nombre) dont chacune on une unique sequential memory address.

### Pile. (Stack)
Grow downwards.
FILO -> First in last out.
Sommet = dernière donner ajouter
Les données sont stacker dans l'ordre juste a côter de la mémoire allouer pour des variable déjà existante.

La stack est contigue et toute les donner dedans ont une taille fixe qui ne change pas.
- Ex: floats prennent 4 bytes, double prennent jusqu'a 8 bytes.

Can be full because of function calling itself too much.

### Heap 
Grow upwards
La heap est pour l'allocation dynamique.
We can request blocks of memory on the heap of different sizes as the programm is executing.
- A block of memory will be given to us and we can set a pointer (in our stack ) to point to this memory
The block in heap are not necessarily in order.

**malloc is used to request block of memory on the heap.**

malloc renvoie un void pointer (typeless pointer) de la mémoire allouée.

La memoire heap doit être gérere manuellement. On doit utiliser free() pour libérer la place allouer précédemment avec malloc().
Ce type de management est appeler manual memory management
- Ce type de management aide a améliorer les performence mais vient au prix des memory leaks (si on oublie de free la mémoire)

### Garbage collector
Regularly check the heap fo blocks of memory.





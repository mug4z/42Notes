## 1. Structure 
Les erreurs doivent être sur la standard error.
- Ajouter la libft depuis mon github -> OK
- Faire le Makefile -> OK
- Des arguments ne sont pas des integers -> OK
	- Permettre le check depuis une input entre " "  -> OK
- Si il y a un pas asser d'arguments -> OK
- Des arguments sont plus grand qu'integers ->  OK
-  Les chiffre negatifs doivent pouvoir etre traiter -> OK
	- Pour les limites cast en long et comparer avec int max et int min. ->OK
- Il y a une duplication de chiffre. -> OK
	- TODO: voir comment populer une liste chainer de int pour pouvoir checker les dupliquer -> OK
- Faire un schéma des actions disponible.
- Voir si il faut geré des arguments du style "1 2 3" "4 5 6". -> ERROR
- Write `ERROR\n` on the standard error. -> OK
### Test 
- check les test qui sont dans le guide https://42-cursus.gitbook.io/guide/rank-02/push_swap/building-the-thing
- **The program must work with several numerical arguments**
    - ./push_swap 1 3 5 +9 20 -4 50 60 04 08 -> OK
- **The program also works if you receive a single character list as a parameter**
    - ./push_swap "3 4 6 8 9 74 -56 +495" -> OK
- **The program should NOT work if it encounters another character**
    - ./push_swap 1 3 dog 35 80 -3 -> OK
    - ./push_swap a -> OK
    - ./push_swap 1 2 3 5 67b778 947 -> OK
    - .push_swap " 12 4 6 8 54fhd 4354" -> OK
    - ./push_swap 1 -- 45 32 -> OK
        - these examples should return "Error\n"

- **The program should NOT work if it encounters a double number**    
    - ./push_swap 1 3 58 9 3 -> OK
    - ./push_swap 3 03 -> OK
    - ./push_swap " 49 128 50 38 49" -> OK
        - these examples should return "Error\n"
    - ./push_swap "95 99 -9 10 9" -> OK
        - this example should work because -9 & 9 are not equal
- **The program should work with INT MAX & INT MIN**
    - ./push_swap 2147483647 2 4 7 -> OK
    - ./push_swap 99 -2147483648 23 545 -> OK
    - ./push_swap "2147483647 843 56544 24394" -> OK
        - these examples should work and sort your list
    - ./push_swap 54867543867438 3 -> OK
    - ./push_swap -2147483647765 4 5 -> OK
    - ./push_swap "214748364748385 28 47 29" -> OK
        - these examples should return "Error\n"

- Checker les leaks de mémoire. -> OK

## 2.Coder les actions
- Mettre tout les chiffre dans la stack a -> ok
- Coder les actions.
	- Remplir ma stack a. -> ok
	- A chaque  fois que l'action est effectuer print l'action suvi de `\n` 
- **sa (swap a)**: If there are 2 numbers, swap the first 2 elements at the top of the stack a. -> OK
- **sb (swap b )** : If there are 2 numbers, swap the first 2 elements at the top of the stack b. -> OK
- **ss** : sa and sb at the same time. -> OK
- **pa (push a)**: If b is not empty it takes the first element on top of b and puts it on a. -> OK
- **pb (push b)**: If a is not empty, it takes the first element on top of a and puts it on b. -> OK
- **ra (rotate a)**: Shifts all the elements of the stack a up by one position. The first element becomes the last. -> OK
- **rb (rotate b)** : Shifts all the elements of the stack b one position upwards. The first element becomes the last one. -> OK
- **rr** : ra and rb at the same time. -> OK
- **rra (reverse rotate a)**: Shifts all elements of the stack down one position. the stack a. The last element becomes the first. -> OK
- **rrb (reverse rotate b)**: Shifts all the elements of the stack b one position downwards. the stack b. The last element becomes the first. -> OK
- **rrr** : rra and rrb at the same time -> OK
### Test
- Check les leaks -> OK
## 3.Algoritmique
- Faire fonction is_sorted -> OK
- Voir cas 
	- 1 -> OK
	- 2 -> OK
	- 3 -> OK
- Algo radix pour plus de 3: 
	- Créer un tableau qui contient tout les chiffre en arguments -> OK
	- Sort la liste -> OK
	- Convertir les chiffres de la liste en index. -> OK
	- Faire le radix en binaire avec les index. -> 
		- 
	- Check les leaks.
## 3. Test
- Testé avec le checker 
- Recherché si des checker existe pour voir le nombre d'action je fait.
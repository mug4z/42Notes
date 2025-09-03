## Args checker
- Checker si file1 existe. -> OK
- Checker si cmd1 existe. -> OK
	- Construire le path -> OK
	- Aller check tout les paths présent dans la variable d'env PATH -> 
		- Get the paths list -> OK
		- Get the cmd list  -> OK
		- Get the args list ->  OK
- Checker si file2 existe. -> OK
- Checker si cmd2 existe. -> OK

### Test
- Check les leaks. -> OK
## Remplir la structure de contexte.
- Remplir un tableau de structure. 1 case pour chaque commandes. -> OK
- Malloc le tableau -> OK
- Remplir mes args avec toujours le cmdpath en premier arguments.

### Test 
- check les leaks

## Cmd runner and PIPE maker.
- faire un fork pour la première commande.
- faire une redirection de l'input standard vers le fichier.
- Faire un pipe pour la cmd1 et cmd2.
- 

## Chose a check
- Quand tu écrit dans un fichier qui est déjà remplie  alors tout doit être remplacer par la nouvelle output. -> OK avec open option O_TRUNC.
- Si le file2 n'existe pas, le créer et écrire dedans.
- Si pas d'output du groupe 1 (file1 et cmd 2) OUT -> end of file -> IN du groupe 2 (cmd2 file2 )
- Comment utiliser execve avec le format de commande "ls -ls" doit aussi marcher avec "ls -l -s" les commandes avec argument sont toujours entre "" faire split sur espaces.
- file1 existe Cmd1 existe pas,: faire le groupe 2
- file2 existe mais pas cmd2 ce passe rien part le perror)
- file2 et file1 existe mais pas cmd2 et cmd1 ce pass rien (a  part le perror) 
- Permission de read pour file1
## Error
- Si file1 n'existe pas. (Continue quand même pour créer le file2 et remplir avec le résultat de la cmd2) perror (pipex file1)
- Si il n'y a pas de process qui read.


CHECK
- si infile et outfile sont des directory -> OK
- les "" et '' -> OK
- les permissions avec un chmod 000 -> OK
- Faire un splitspace qui permet de split sur tout les espaces. -> pas encore fonctionelle
- Faire une structure d'erreur pour remonter les status d'erreurs.
- Message erreur command invalide -> OK
- Message erreur outfile permission denied. -> OK
	- LE shell a l'air de check d'abord la validiter des fichier et ensuite checke les commande
	- < infile lss | ls > out -> 
- Chek si une commande est "" command not found et pas segfault -> 
	- Le probleme vient du split qui ne split pas sur une chaine composer d'une " "
- Espace avant et apres command not found
- Commandes a check.
	- < infile grepp a | wc out
	- < infile grep a | wccc out
	- 

A check segfault
- ./pipex infil "" "ls" out
- ./pipex infile "grep a" "ls" out (quand le in et out on des permission denied)
Quand status du waitpid est 512 le prompt est rendue directement mais pas quand le status est 3216X`

TEST CHECKLIST:
Out n'existe pas
- ./pipex infile "ls" "wc" out
Out est bien réecraser
- ./pipex infile "ls" "wc" out
Infile est bien pris en input.
-  ./pipex infile "grep CAMION" "wc" out
Les guillement fonctionne avec grep
-  ./pipex infile "grep 'CAMION'" "wc" out
Pas de segfault si la cmd1 est `\0`
- ./pipex infile "'" "wc" out


# A FAIRE REFACTOR POUR QUE LA STRUCTURE SOIT MOINS SPAGHETTI.

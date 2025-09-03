TOKENISATION ?

TRUC A RAJOUTER:
- Gerer les simple quote dans la commande comme dans : grep 'CAMION'
- Des que dans argv[x] il y a un quote ou double quote enlever le premier et le dernier.
- Voir pour gerer les IS_SPACE donc pas uniquement les espaces.
## Objective du programme
Le programme doit gérer des pipes.

Le programme vas s'executer comme ça
`./pipex file1 cmd1 cmd2 file2`

Le programme doit ce comporter **exactement** comme la commande :
- `< file1 cmd1 | cmd2 > file2`

## Input

Le programme prend 4 arguments: 
- file1, file2 -> nom de fichier
- cmd1 ,cmd2 -> commandes shell avec leurs paramètre.

## Recherche
Commandes:
- Comment fonctionne `< file1 cmd1 | cmd2 > file2` ? -> OK
	- Le `<`fait que la stdin est un fichier et non le clavier donc on execute la `cmd1` sur le `file1`
	- Le `|` prend le stdout de `cmd1` et l'envoie dans stdin de `cmd2`.
	- La `cmd2` lit   le stdout de la `cmd1` et donne un résultat.
	- Le `>` envoie sur la stdout le résultat de la `cmd2` dans `file2`, 
Fonctions:
- close 
	- The close() call deletes a descriptor from the per-process object reference table. Return 0 si success et -1 si failed.)
- write -> OK
- perror
	- Va concater le text mis dans perror : le texte errno.
- strerror
	- Donne le message d'erreur correspondant au numéro donner
- access
	- Check the accesibility of a file for a given mode.
	- return 0 if good, -1 if not good.
- dup, dup2 
	- dup : duplicates an exisiting file descriptor and returns it's value to the calling process. The new file descriptor is the first number available from the per-process filedescriptor table (getdtablesize() gives you the size of the table.) The object reference by the filedescriptor and the duplicate one, do not distinguish the file descriptors. So the fds point to the same document.
	- dup2 :  Work. on like dup, but you have to give the number you want to be the duplicate fd. If the number you gave is an active fd it will be first dealocated as if close had been done first.
- execve ()
	- Transform the calling process to a new process. It execute a file. The file can be an executable file or a file of data for an interpreter.
	- It need 3 param 1: the path to the file to be executed 2 : The arguments to be sent to the new process (at least 1), the first one is the name of the process executed. 3: The name of the environment (can be null)
- exit 
	- Exit a process.
	-  Before termination, exit() performs the following functions in the order listed:
		1.   Call the functions registered with the atexit(3) function, in the reverse order of their registration.
		2.   Flush all open output streams.
		3.   Close all open streams.
		4.   Unlink all files created with the tmpfile(3) function.
- fork -> OK (crée un child process et retourne le PID du child envoie 0 au child.)
- pipe -> OK
- unlink
	- 
- wait
	- wait for a child 
- waitpid
	- wait until the process given by the pid is finished.
	- withe options at 0 return only for terminated child.
Principes:
- Comment fonctionne un pipe | -> OK
- operator < et > dans le terminal ? -> OK
- Process ? -> 

## Commencer l'implémentation 
- Faire le checker
- 
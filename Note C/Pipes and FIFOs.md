System File table ?
## Objectif
Transfer le standard output  de la commande de gauche, a la  standard input de la commande de droite.

Exemple: La standard output  de la commande `ls` est passé dans la standard input de la commande `wc`
```bash
ls -l | wc -l
```
## Méchanisme
Pipes are unamed object created to allow two processes to communicate. We call it an **interprocess** communication.
Data written to the pipe by one process can be read by another process.
The data is handle in  a FIFO (First in First out) order.


## Creating a Pipe.

La subtilité est qu'il faut fermer la partie read quand on écrit et fermer la partie writing quand on a fini de lire.
```c
#include <unistd.h>
#include <stdio.h>
#include <fcntl.h>
#include "../libft/libft.h"

int main()
{
// mypipe[1] is for writing
// mypipe[0] is for reading
int mypipe[2];
int fd_fileout;
int status;
char buf[10];
pid_t pid;

if (pipe(mypipe) == -1)
	return (1);
pid = fork();
if (pid == -1)
	return (1);
if (pid == 0)
{
	printf("HELLO FROM CHIlD\n");
	read(mypipe[0],buf,9);
	fd_fileout = open("CAMION",O_WRONLY | O_CREAT | O_TRUNC,0644);
	ft_putstr_fd(buf,fd_fileout);
	close(fd_fileout);
	close(mypipe[1]);
}
if(fd_fileout < 0)
	perror("WRONG file descriptor");
if (pid > 0)
{
	printf("HELLO FROM PARENT\n");
	close(mypipe[0]);
	ft_putstr_fd("asdadasd",mypipe[1]);
	//waitpid(pid,&status,0);
}
return (0);
}
```
## Atomicity of Pipe I/O
Lire ou écrire des donnée de Pipe sont atomic quand la taille de la donné ne dépasse pas la macro PIPE_BUF (définie dans le header limits.h)

# Source
[[Note_unix/Source|Source]]

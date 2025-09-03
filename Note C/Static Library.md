Est une library crée avec la commande `ar` qui contient les fichier des fonctions en .o .

1. D'abord avoir tout les fichier de fonction que vous voulez mettre dans votre librairy
2. les compilé  en .o ->`gcc -Wall -Werror -Wextra -c ft_*.c`
3. Les ajouté a une archive -> `ar -rcs libft.a ft_*.o`
	1. -r: replace or add the specified files to the archive
	2. -c: create the archive silently
	3. -s: write an object-file index into the archive or update an exisiting one, equivalent to ranlib libname.a
4. Link la lib au main.c `gcc main.c -L. -lft -o main`
	1. -L : give the path to the given library `.` mean the current directory
	2. -l : the name of the library without the "lib" and the ".a", the linker add these part itself

# Source
[[Source]]  
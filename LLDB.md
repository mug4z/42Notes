FOC CMD (FOCING SHIT)
Default debugger on mac

Compile the programm with 
gcc -Wall -Wextra -Werror -g files.c
	- g : Generate debug information

```
lldb programme

(lldb) b function_name // breakpoint 
(lldb) run
* thread #1, queue = 'com.apple.main-thread', stop reason = breakpoint 1.1
    frame #0: 0x0000000100003f88 a.out`main at ft_swap.c:26:4
   23  		int a;
   24  		int b;
   25
-> 26  		a = 1;
   27  		b = 2;
   28  		ft_swap(&a,&b);
   29  	}
(lldb) gui // Graphical interface
```

p: permet d'evaluer des variables, de savoir ce qu'elle on a l'intérieur et pouvoir faire des operations dessus

var : permet de voir des variable avec leur valeur a l'interieur.
vo : permet de voir des variable sans les valeur a l'interireur.

## Avoir le contenue d'une addresse mémoire
```
memory read -s1 -fu -c1 [memory_address] --force
```

## Debugger avec des arguments.
```
lldb ./prog arg1 arg2
lldb ./prog "arg1 arg2"
```
OR
```
lldb ./prog
(lldb) r arg1 arg2 arg3 // r "arg1 arg2 arg3"
```

## Executer avec un stdin
```
(lldb) process launch -i file
```
## Executer des commandes shell depuis lldb
```
(lldb) shell {command}
```

Donc on peut aussi faire une changement de code lancer shell code et run le debugging sans avoir besoin de quitter lldb et revenir dedans.


## Voir les elements d'un pointer directement
```
(lldb) parray nbr_element ptr
```

## Processes
Pour l'instant le settings  ne fonctionne pas dans la version `lldb-1200.0.44.2`
```bash
settings set target.process.follow-fork-mode child
```

D'après https://stackoverflow.com/questions/19204395/lldb-equivalent-of-gdbs-follow-fork-mode-or-detach-on-fork ça a été ajouté dans la version 14 de LLVM.
### Debug child process (Only on lldb V14+)
Activate this settings
```
(lldb) settings set target.process.follow-fork-mode child
```

ATTENTION : if you accentaly run the programm before activate the settings, relaunch lldb, apply the setting before running.

Put the breakpoint on the part that should be executed by the child process.

Debug like usual.

## List code source

```
(lldb) source list
(lldb) l // for next part of the code.
```
## Continue to a specific line

```
(lldb) thread until <line_number>
```

## TEST WITH EMPTY STRING
LLDB ignore empty string test with the code below.
```c
for (int i = 0; i < argc; i++) {
if (strcmp(argv[i], "EMPTY_ARG") == 0) {
argv[i][0] = '\0';
}
}
```

## Breakpoint sur des methodes
```
(lldb) breakpoint set --method method_name
(lldb) br s -M method_name
```

# Source
[[Source]]
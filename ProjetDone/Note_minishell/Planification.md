Dependance:
	- Readline v8.2
Notes :
- readline() function cause memory leaks, if memory leaks comes from it  we don't need to fix them.
- You should limit yourself to the subject description. Anything that is not asked is not required.
- go https://www.gnu.org/savannah-checkouts/gnu/bash/manual/html_node/index.html if doubt.
## Objectif 

- Display prompt when waiting for a new command.
- Have a working history
- Launch the right executable based on the PATH variable or using a relative or an absolute path.
- Only 1 global variable to indicate the received signal.
	- The global variable cannot provide other information or data access than the number of a received signal.
- Not interpret unclosed quotes or special characters such as `\` or ;
- Handle `'` single quote, prevent the shell from interpreting the metacharacters in the quoted string.
- Handle `"` double quotes, prevent the shell from interpreting the metacharacters in the quoted string, exepect for $.
- Implement redirections:
	- < : redirect input
	- > : redirect output
	- << : Give a delimiter then read input until the delimiter ,Don't have to update the history
	- >> : append output
- The pipe `|` should work
	- See pipex bonus
- Handle environment variables ${characters} , should expand their values.
- Handle $?, exit status of the most recently executed programm.
- Handle these like in `bash`
	- ctrl-C displays a new prompt
	- ctrl-D exits the shell
	- ctrl-\  does nothing.
- Implement the  following builtins
	- echo with option -n
	- cd with only a relative or absolute path
	- pwd with no options 
	- export with no options 
	- unset with no options 
	- env with no options or arguments
	- exit with no options

## Recherche 
### Shell interactive mode ?

### Meta character ?

### Global variable ?
- Voir les implications de l'utilisation de variable global.


## Recherche
Check what does the builtins.
### Functions
Connait pas -> 35 functions

readline, 
rl_clear_history,
rl_on_new_line, 
rl_replace_line, 
rl_redisplay,
add_history,
printf, -> Connait
malloc, -> Connait
free, -> Connait
write, -> Connait
access, ->Connait
open, -> Connait
read, -> Connait
close, -> Connait
fork,  -> Connait
wait, -> Connait
waitpid, -> Connait
wait3,
wait4,
signal,
sigaction,
sigemptyset,
sigaddset,
kill,
exit, -> Connait
getcwd,
chdir,
stat,
lstat,
fstat,
unlink,
execve, -> Connait
dup,  -> Connait
dup2, -> Connait
pipe, -> Connait
opendir,
readdir,
closedir,
strerror, -> Connait
perror, -> Connait
isatty,
ttyname, 
ttyslot, 
ioctl, 
getenv,
tcsetattr, 
tcgetattr,
tgetent,
tgetflag, 
tgetnum, 
tgetstr, 
tgoto, 
tputs

The results of the word expansions are split using the characters in the value of the shell variable IFS as delimiters. This is how the shell transforms a single word into more than one. Each time one of the characters in $IFS appears in the result, bash splits the word into two. Single and double quotes both inhibit word splitting.

The $IFS (**Internal Field Separator) variable. By default it is space, tab and newline.**

Note that if no expansion occurs, no splitting is performed.

- [https://www.gnu.org/software/bash/manual/bash.html#Word-Splitting](https://www.gnu.org/software/bash/manual/bash.html#Word-Splitting)
    

How to see the value of IFS

- cat -etv <<<"$IFS”
    
- [https://bash.cyberciti.biz/guide/$IFS](https://bash.cyberciti.biz/guide/$IFS)
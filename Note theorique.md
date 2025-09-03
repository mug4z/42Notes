Le character "start of line" fait 1 byte de grandeur.

## Git
### Head
This is your current branch
You can see it  by `cat .git/HEAD`

## Bash
Mettre le **#!** au debut du script indique au kernel qu'il faut executer ce qu'il y a juste apres
Quand on execute le script:
`./nom_script.sh`
Ce que sa fait
1. le kernel voit le shbang #!
2. Il execute ensuite ce qu'il y a apres, exemple: /bin/sh

Donc si au debut vous avez `#!/bin/sh`, ./nom_script.sh = /bin/sh nom_script.sh

Pour plus de portabiliter:
```
#!/usr/bin/env sh
```


**ATTENTION** toujours mettre le shebang au debut sinon le shell executera la commande meme si les commande dans le script ne sont pas fait pour le shell en question.

## Diff output
"< file 1"  "> file 2"
si 11,12 -> means that the modifications was done on line 11 - 12 
c = content was replaced
a = content was added of appendedd
d = content was deleted

Diff fait un fichier en disant quelle ligne est remplacer par quoi et patch applique ces changements.

## Magic files
his is a file used by the [`file`](https://linux.die.net/man/1/file) utility program in UNIX-based operating systems to identify a file type by examining its content rather than relying on its file extension or metadata.

They have some 

Check
ex00 -> ok
ex01 -> ok
02 -> OK
03 -> OK
04 -> OK
05 -> OK
06 -> Ok
07 -> Ok
08 -> OK
09 -> OK
Git clean a voir la review.



# Source
[[Source]]
## Changer de terminal
```
chsh -s /bin/sh
```
redemarrer terminal
## Droit sous linux
### Commande
```
chmod
```

### Changer les permissions d'un symlink
```
chmod -h sym_link
```

### Theorie
les droit sont rwx
- r: read
- w: write
- x: exection

Different user
- ugo: user,group,other
Octale
- 0 : - - - (aucun droit)
- 1 : - - x (exécution)
- 2 : - w - (écriture)
- 3 : - w x (écriture et exécution)
- 4 : r - - (lecture seule)
- 5 : r - x (lecture et exécution)
- 6 : r w - (lecture et écriture)
- 7 : r w x (lecture, écriture et exécution)

Exemple:
``chmod 777 fichier``
- 7 a user, 7 a group et 7 a other

## Changer la date d'un fichier (macosx)
```
touch -t 202306012342 nom_fichier
```
- Change la date et l'heure au 01.06.2023 a 23:42
## Changer la date d'un symlink
```
touch -ht 202306012342 nom_fichier
```

## Compresser un fichier tar
```
tar -cf nom_archive.tar nom_fichier
```
## Extraire un fichier tar
```
tar -xf nom_fichier_archives
```
- -x: extract le fichier de l'archive sur le disque
- -f: specifie de quelle fichier on doit lire ou ecrire.

## Extraire un fichier tar en gardant les permissions des symlink
```
tar -pxf archive_name
```

## Creer un hard-link
```
ln nom_fichier nom_du_link
```
## Creer un lien symbolique
```
ln -s nom_fichier nom_du_link
```

## Creer une cler ssh

```
ssh-keygen
```
3 enter + aller chercher dans ~/.ssh

## Git
### Mettre a jour son repo
1. ``git add nom_fichier ``
2. ``git commit -m "commentaire du commit"``
	1. -m: indique un commentaire a mettre
3. `git push`

Bien faire des git status dans le doute pour voir les modifications

### Annuler un commit (non push)
```
git reset --soft HEAD^

- --soft: leaves all your changed files as "Change to be committed"
```

## Changer sa config git
```
git config --global --edit

- --global: configuration globale et non uniquement lier au 
- --edit: open an editor to modifiy specified config
```
et envoyer les changements 
```
git commit --ammend --reset-author

- --reset-author: declare that the authorship of the resulting commit belong to the committer
```
Exo 05 Git commit:
## Avoir les id des commits
### Donne tout les commit avec leur id et message
```
git log
```

### Limiter au x dernier commit
```
git log -n x
OR
git log -x
```

### Avoir uniquement les commit id
```
git log --pretty=tformat:'%H'

- %H: commit hash
- tformat: putt a newline character at the end of the line.
```

## Ex07 
### diff
```
diff a b
```

### patch
```
patch fichier_a_pacther fichier.diff/patch
```

## Ex08
```
find . -type f  \( -name "*~" -o -name "#*#" \) -print -delete
```

## Man
Avoir la doc des appel systeme
```
man 2 nom_appel_system
```
sous le synopsis a les dependance de la commande.

# Source
[[Source]]
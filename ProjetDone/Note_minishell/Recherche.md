
1. Voir ce que fais un bash en 
	1. https://aosabook.org/en/v1/bash.html#:~:text=Bash%20reads%20input%20from%20the,Unix%20emacs%20and%20vi%20editors. --> A LIRE. apres midi.
		1. Type of token:
			1. reserved words : words that the shell knows internally, 
			2. words : Is a sequence of characters separated by metacharacters.
			3. operators : one or more metacharacters
	2. https://medium.com/geekculture/an-overview-of-the-working-of-the-bash-shell-f063e7f09945
	3. 
3. Tokenisation () --> recherche a faire le matin.

https://www.man7.org/linux/man-pages/man1/bash.1.html#QUOTING:~:text=IFS%20%20%20%20The%20Internal%20Field%20Separator%20that%20is%20used%20for%20word%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20splitting%20after%20expansion%20and%20to%20split%20lines%20into%20words%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20with%20the%20read%20builtin%20command.%20%20The%20default%20value%20is%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%60%60%3Cspace%3E%3Ctab%3E%3Cnewline%3E%27%27.

A FAIRE le 21.03.2024 : Faire le parsing sur le quoting.
	- Simple quote -> les mots doivent etre a l'interieur
	- Double quote -> les mots doivent etre a l'interieur 
- Principe:
	- Quand character " ou ' cherche le prochain et prendre tout ce qu'il y a entre.
	- Enlever les quote les plus au extremiter
	- Si rien n'est pris entre les quote alors return `\0`.

- A FAIRE LE 25.03 integrer les variables d'env sous forme de liste chainer.
- A FAIRE LE 26.03 CORRIGER LE PROBLEME DE QUOTES.
- A FAIRE LE 17.04:
	- DANS L'EXPENSION FAIRE LA PARTIE QUI REMPLACE LA STRING ÉTENDUE DANS LA STRING ORIGINEL. EN PARTANT DU $.
## Command line exemple
```bash
#Arguments
ls
ls -l
ls -l -a
ls -la

#Pipe
ls -la | wc
ls -la | wc -l
ls -la | grep "CAMION" | wc
cat | cat | ls

#Expansion
echo Hello
echo '$HOME'
echo "$HOME"
echo "ls -l | wc"
echo 'ls -l | wc'

```


```
# Arguments
ls
What should be in the list
  t_WORD_LIST.word.word = ls
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next = NULL
-------
ls -l
What should be in the list
  t_WORD_LIST.word.word = ls
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next =
    WORD_LIST.word.word = -l
    WORD_LIST.word.flags = IS_WORD
    t_WORD_LIST.next = NULL
------
ls -l -a
What should be in the list
t_WORD_LIST.word.word = ls
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next =
    WORD_LIST.word.word = -l
    WORD_LIST.word.flags = IS_WORD
      t_WORD_LIST.next =
        WORD_LIST.word.word = -a
        WORD_LIST.word.flags = IS_WORD
        t_WORD_LIST.next = NULL
```

```
# Pipe
ls -la | wc
What should be in the list
t_WORD_LIST.word.word = ls
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next = 
    t_WORD_LIST.word.word = -la
    t_WORD_LIST.word.flags = IS_WORD
    t_WORD_LIST.next =
      t_WORD_LIST.word.word = |
      t_WORD_LIST.word.flags = IS_OPERATOR
	    t_WORD_LIST.next =
		  t_WORD_LIST.word.word = wc
		  t_WORD_LIST.word.flags = IS_WORD
		t_WORD_LIST.next = NULL

ls -la | grep "CAMION"
What should be in the list
t_WORD_LIST.word.word = ls
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next = 
    t_WORD_LIST.word.word = -la
    t_WORD_LIST.word.flags = IS_WORD
    t_WORD_LIST.next =
      t_WORD_LIST.word.word = |
      t_WORD_LIST.word.flags = IS_OPERATOR
	    t_WORD_LIST.next =
		  t_WORD_LIST.word.word = grep
		  t_WORD_LIST.word.flags = IS_WORD
		     t_WORD_LIST.next = 
		       t_WORD_LIST.word.word = "CAMION"
		       t_WORD_LIST.word.flags = IS_DOUBLEQUOTED
		       t_WORD_LIST.next = NULL
```

```
echo '$HOME'
What should be in the list
t_WORD_LIST.word.word = echo
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next = 
    _WORD_LIST.word.word = '$HOME'
    t_WORD_LIST.word.flags = IS_WORD
    t_WORD_LIST.next = NULL
echo "$HOME"
What should be in the list
t_WORD_LIST.word.word = echo
  t_WORD_LIST.word.flags = IS_WORD
  t_WORD_LIST.next = 
    _WORD_LIST.word.word = "$HOME"
    t_WORD_LIST.word.flags = IS_EXPENABLE
    t_WORD_LIST.next = NULL

```
## Objectif
Faire un jeux 2D avec un personnage. Le personnage doit récupérer des item avant de pouvoir sortir.

## Input
Une carte au format .ber

## Recherche
- Apprendre la minilibix -> 
	- Installer pour MAC OS - > OK
- Voir les fonctions de la bibliothèque math avec options de compilation `-lm`

## Avant de commencer  -> DONE
- Update ma libft avec les modifications faite dans pipex. -> OK
- Ajouter mes fonctions de ft_clean et ft_clean2dtable a ma libft -> OK
- Revoir mon makefile pour en faire un plus propre
	- faire sa aussi pour ma libft. -> OK

## Le jeu
- But: Rammasser tout les items et s'echaper
- Controle : W A S D 
- Directions : HAUT BAS DROITE GAUCHE
- Les murs sont des murs
- Les mouvement sont compter et doivent être afficher dans le shell
## Gestion Graphique
- Une image dans une fenêtre 
- Pouvoir changer de fenêtre la réduire
- ESC doit quitter la fenêtre et quitter le programme proprement
- Cliquer sur la croix doit fermer la fenetre et quitter le programme proprement
- Utiliser les images de la Minilibx est obligatoire.

## La carte
- Construite avec 3 éléments : murs, items, espace vide
- La carte peut être composer de 5 caractères:
	- 0 pour un emplacement vide
	- 1 pour les murs
	- C pour un items à collecter
	- E pour une sortie
	- P pour la position de départ du personnage.
### OBLIGATIONS
- la carte **doit avoir** 1 SORTIE , au moins 1 ITEM et 1 POSITION DE DÉPART.
- Forme rectangulaire.
- La carte doit être fermer en étant encadrer par des murs. -> return error.
- Verifier qu'il existe un chemin valide (flood fill)
- Pouvoir parser tout type de carte qui respecte les règles.
## Erreur
- Si une erreur de config est détecter le programme doit quitter avec `ERROR\n`.
- Suivie d'un message d'erreur personaliser.


# Source
Doc minilibix -- lue le 8.02.2024
https://harm-smits.github.io/42docs/libs/minilibx/introduction.html
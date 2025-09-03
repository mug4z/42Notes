A FAIRE UNE FOIS FINIE, revoir mes message d'erreur pour les faire unquimenent avec la fonction ft_printerr
## Etapes
- check de l'extension de la carte. -> OK
- check que l'arg de la carte est pas empty -> OK
- Check du contenue de la carte. ->
	- check que ce soit pas empty -> OK
	- checke qu'il ny ai pas d'element invalide -> OK
- Check les leaks.
### Cas d'erreurs
- L'extension du fichier est pas `.ber`. -> OK
- La carte comporte des element non valide. -OK
- La carte n'est pas rectangulaire. ->OK
- Les bord ne sont pas des murs. -> OK
- La carte ne contient pas -> OK
	- 1 SORTIE 
	- 1 ITEM 
	- 1 POSITION DE DÉPART.

## La SUITE
- remplir la struct qui contient ma map -> OK
- check si elle est rectangulaire. -> OK
- check si elle contient les element minimum. -> OK
- check si elle est faisable. -> OK
## Etapes
- render la map -> A faire
- Render:
	- render le sol
	- render les arbres
	- render les collectible
	- render la sortie
	- render le player.
- Preparer les images en xpm pour les different element de base;
	- Character
	- sol
	- murs
	- Collectible
## Le jeu
- But: Rammasser tout les items et s'echaper
- Controle : W A S D 
- Directions : HAUT BAS DROITE GAUCHE
- Les murs sont des murs
- Les mouvement sont compter et doivent être afficher dans le shell
## Gestion Graphique
- Une image dans une fenêtre  -> oK
- Pouvoir changer de fenêtre la réduire -> OK
- ESC doit quitter la fenêtre et quitter le programme proprement -> oK
- Cliquer sur la croix doit fermer la fenetre et quitter le programme proprement -> OK
- Utiliser les images de la Minilibx est obligatoire. -> OK

# A FAIRE
- Mettre a la norme
- utiliser mlx_putstring pour afficher le compte de pas que le perso fait.
- Ne pas oublier de free a chaque fois de qu'on affiche.
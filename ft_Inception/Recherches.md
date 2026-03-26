# V1
## Technologies
Mariadb it is easier with debian ?
### Docker
Pourquoi quand je fais un docker build sa build une images sans nom ? Et est ce que si une images existe deja je dois la rebuild ?
- Docker compose:
	- docker-compose.yml -> OK
- Dockerfiles. -> OK
- Volumes. -> OK
- docker-network. -> OK
- secrets -> OK
- Best practices.
- container must restart in case of crash.
- Compose up
	- docker creates container and attach it

### Alpine
- penultimate version -> avant derniere version
## Debian (I guess it's better)

### MariaDB
> [!note]
> - Voir comment on ajoute un user et mdp pour mariadb.
> -  Voir comment on ajoute un user et mdp pour administrer la base Wordpress

Il y a un decalage entre l'exec de la command bash et sont application dans la db

### NGINX
- TLSv1.2 
- TLSv1.3

### Wordpress
- php-fpm

# V2
Utiliser les images officielles et les remplacer petit a petit
Mariadb
Wordpress
Nginx

Mettre en place ces container dans la VM.

## VM
Mount the project file into vm
`sudo mount -t vboxsf inception2 inception/`
For the ssh connexion
`apt install openssh-server`

## NGINX
- Ok avec une connection SSL 
>[! warning] Pas encore avec wordpress

Le probleme que nginx ne peut pas aller chercher les fichier de wordpress est lier au volume. Un volume doit pouvoir partager les fichiers.
## Wordpress

https://medium.com/@jealousgx/effortlessly-set-up-wordpress-using-docker-a-detailed-guide-300bf3860d69


## Mariadb

UP AND RUNNING

## POUR LA SUITE
CHANGER petit a petit les container officiel avec les miens.



---
id: Planification
aliases: []
tags: []
---

## Faire des recherches
1. Docker
2. alpine
3.  mariadb 
4. nginx
5. wordpress

[[Recherches]]

## Implementer 
- F
- VM debian.
	- Installer docker pour debian.


>[!error] Volumes must be in the host /home/login/data

>[!warning] NGINX MUST send request to wordpress thus it need to change




## V2

## CHANGER les container par les miens

### Nginx
- [X] Mettre la config que j'ai ajouter dans l'image officiel dans le miens
- [X] Verifier la connexion en https

### Wordpress
- [X] Voir quelle commande est lancer en PID 1
- [X] Ajouter la config avec le container 
- [X] Bien changer le volume partager avec wordpress et NGINX
- [X] Ameliorer le script de lancement
- [X] Ajouter un user non admin
  - wp user create

### Mariadb
- [X] Voir quelle commande est lancer en PID 1
- [X] SELECT user_login FROM wp_users; -> voir si les user sont bien en database.
- Execute le test.sql directement dans mariadb -- mariadb -uroot -pYOLO --database=$SQL_DATABASE_NAME < test.sql 
- Dans le code du docker-entrypoint.sh
  - docker_process_init_files() 
  - docker_process_sql() -- run the sql 
  - docker_exec_client() -- call the client to run the sql

### Check la disponibiliter des container
- healthcheck:
  1. mariadb -> OK

## Verifier la bonne tenue du projet
- [ ] les data son persistante sur la VM 
- [ ] si un container crash il es redemarer automatiquement
- [ ] Tous les user sont creer 
- [ ] Le nom de domaine est le bon
- [ ] *UPLOAD* SUR LE GIT DE 42


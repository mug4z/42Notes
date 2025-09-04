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
- [ ] Ameliorer le script de lancement
- [ ] Ajouter un super user pour l'admin

### Mariadb
- [ ] Voir quelle commande est lancer en PID 1

## Verifier la bonne tenue du projet
- les data son persistante sur la VM 
- si un container crash il es redemarer automatiquement

### Tous les user sont creer

### Check la disponibiliter des container
- healthcheck:
  1. mariadb
  2. wordpress
  3. nginx

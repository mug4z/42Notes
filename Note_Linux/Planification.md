Mettre l'iso et la vm dans goinfre, attention tu dépend du poste.

- Create the VM ->
	- VDI ? -> 
Crée min 2 partition chiffrée


mdp root: Salutsava97

User : tfrily
	mdp : Salutsava97

Encryption partition passphrase : Salutsava97

- partman: outils utiliser pour partitionner le disque.

- hostname : tfrily42 -> OK
- Partition OK
- SSH ->OK
	- port 4242 -> OK
	- interdire la connexion root. -> OK
-  UFW: -> OK
	- Autoriser uniquement le port 4242 -> OK
	- enalble au startup : le fait direct quand on démarre ufw -> OK
- SUDO
	- Installed > OK
	- Ajouter tfrily dans le groupe sudo -> OK
	- Limité a 3 essaie de mdp -> OK
	- Afficher un message en cas de mauvais mdp -> OK
	- archivage input/output a /var/log/sudo/. -> OK
	- Mode tty activer -> OK
	- Les path utilisable par sudo seront restreints. exemple: -> OK /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
- Créer un groupe user42 -> OK
- Creer un nouvelle utilisateur -> 
- Politique de mdp fort:
	-  Votre mot de passe devra expirer tous les 30 jours. -> OK
	- Le nombre minimum de jours avant de pouvoir modifier un mot de passe sera configuré à 2. -> OK
	- L’utilisateur devra recevoir un avertissement 7 jours avant que son mot de passe n’expire. -> OK
	- Votre mot de passe sera de 10 caractères minimums dont une majuscule et un chiffre, et ne devra pas comporter plus de 3 caractères identiques consécutifs. -> OK
	- Le mot de passe ne devra pas comporter le nom de l’utilisateur. -> OK
	- La règle suivante ne s’applique pas à l’utilisateur root : le mot de passe devra comporter au moins 7 caractères qui ne sont pas présents dans l’ancien mot de passe. 
	- Bien entendu votre mot de passe root devra suivre cette politique. -> OK
- monitoring.sh
	- L’architecture de votre système d’exploitation ainsi que sa version de kernel. -> OK
	-  Le nombre de processeurs physiques.  -> OK
	-  Le nombre de processeurs virtuels. -> OK
	-  La mémoire vive disponible actuelle sur votre serveur ainsi que son taux d’utilisation sous forme de pourcentage.  -> free command + awk -> OK
	-  La mémoire disponible actuelle sur votre serveur ainsi que son taux d’utilisation sous forme de pourcentage.  -> df -H + awk -> OK
	-  Le taux d’utilisation actuel de vos processeurs sous forme de pourcentage. -> /proc/stat -> OK
	-  La date et l’heure du dernier redémarrage. -> who b + awk -> OK
	-  Si LVM est actif ou pas.  -> /etc/fstab, /dev/mapper/xyz usage of LVM
	-  Le nombre de connexions actives. -> netstat
	- Le nombre d’utilisateurs utilisant le serveur.  -> w command
	- L’adresse IPv4 de votre serveur, ainsi que son adresse MAC (Media Access Control). -> ip. addr -> OK
	- Le nombre de commande exécutées avec le programme sudo. /sudo.log -> OK
	- Faire en sorte que root lance le script pour avoir tout les logs
- cron le script -> 
- préparer les question.
- apparmor activé -> OK
	- Vérifier ce que c'est et qu'est ce que SELinux
	- permission de tes application.
- Kdump -> c'est quoi ?
- aptitude et apt ?
- pourquoi mettre le groupe sudo ?




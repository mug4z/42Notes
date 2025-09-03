Diff entre Rocky et Debian :
- Debian a une utilisation pour les utilisateur lambda alors que rocky linux est destiné a un publique plus pro.
- Rocky est plus utile pour faire des serveur alors que debian aussi une utilisation Desktop.
Diff entre aptidude et apt what APPArmor is.
- aptitude donne une interface graphique
- aptitude gere les conflit/ de packet
- aptidude affiche les changelog
- APPArmor, gère la securiter des application en definisant quelle ressources system des app peuvent acceder et avec quelle droits. Sa gere les droit application 


## Disk

- **PV** : Physical Volumes. This means the hard disk, hard disk partitions, RAID or LUNs from a SAN which form "Physical Volumes" (or PVs).
- **VG** : Volume Groups. This is a collection of one or more Physical Volumes.

sda1 - sda4: Primary partitions
sda5: logical partitions

## SSH
Fichier de config `/etc/ssh/sshd_config`
	- Permitrootlogin no -> permet d'empecher la connexion ssh avec le user root.
	- Port 4242 -> set le port de ssh a 4242.
Restart le services SSH
	`/etc/init.d/ssh restart`
-  Vérifier que le service tourne bien -> `sudo systemctl status ssh`

## Parfeu (UFW)
- Install : apt-get install ufw
- Defaults settings
```
/sbin/ufw default deny incoming
/sbin/ufw default allow outgoing
```
- Enable pare-feu : `/usr/sbin/ufw enable` active automatiquement ufw quand le système démarre.
- Allow port 4242 -> `/sbin/ufw allow 4242`
- Delete a rule -> `/sbin/ufw/ufw delete [nbr_rule]`

## SUDO
Permet de donner a des utilisateurs le droit d'executer certaine commande root.
- Install : `apt-get install sudo`
- Options de limitation d'essaie de mdp: `passwd_tries` par default c'est 3
- Afficher un message lors de mauvais mdp : `badpass_message="NOPE hacker try again"`
- Archivage des input et output des commandes
```
Defaults log_input // log les input des commandes
Defaults log_output // log les output des commandes
Defaults logfile="/var/log/sudo/sudo.log" // fichier de log pour l'input
Defaults iolog_dir="/var/log/sudo" // Dossier de log pour l'output
Defaults requiretty // Set le mode tty. assure que sudo ne peut etre utiliser uniquement depuis un terminal.
```
	- Open it the files ttyout with zcat or zless because they are compressed with gzip.
- Ajouter un user dans le groupe sudo: `sudo usermod -aG sudo tfrily`
	- -a: add te user to groups. Use only with -G
	- -G: list the groups
- User privilege:
- 
### TTY
Gère les différente console connecter en même temps sur linux
commande `tty`

# User
- Ajouter un utilisateur: `sudo adduser` 
## Groupe
Crée un groupe : `groupadd user42`
- assigner group : `sudo usermod -aG user42 tfrily`
- List group:
	- groups (besoin de ce delog log pour voir les nouveaux groupe)
	- `grep tfrily /etc/group`

## MDP Policy
- Install : `apt -y install libpam-pwquality`
- Changer les jours `sudo vim /etc/login.defs` 
```
# Password aging controls:
#
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password changes.
#	PASS_WARN_AGE	Number of days warning given before a password expires.
#
PASS_MAX_DAYS	30
PASS_MIN_DAYS	2
PASS_WARN_AGE	7
```
- Fichier des règles `/etc/pam.d/common-password`
- `password        requisite                       pam_pwquality.so retry=3 minlen=10 dcredit=-1 ucredit=-1 maxrepeat=3 difok=7 enforce_for_root`
	- minlen : taille minmum du mdp
	- dcredit : nombre de chiffre minimum a avoir quand < 0
	- ucredit : nombre de majuscule a avoir quand < 0
	- maxrepeat: nombre de character consecutive accepter
	- difok : nombre de character qui ne doivent pas etre les meme que l'ancien mdp
- `tfrily ALl=(root) NOPASSWD: /usr/local/bin/monitoring.sh` 
	- dis que l'utilisateur tfrily sur tout les host execute le script en tant que root sans avoir besoin de mettre le mdp.
- Mot de passe root ?
-  Change mdp : `passwd`
- Ne pas oublier de faire sur le user deja crée pour update les regle de mdp et reboot.
```
sudo chage -M 30 <user> 
sudo chage -m 2 <user> 
sudo chage -W 7 <user>
```

## Monitoring.sh
- uname -a Permet de me rendre toute les infos sur mon architecture
- /proc/cpuinfo : Contient les information a propos le cpu.
- free donne des informations sur la RAM
- df donne les infos sur le disk dure.
- /proc/stat avoir les stat du cpu
	- vmstat donne aussi des info sur le cpu
	- top donne aussi des infos sur le cpu 
	- /proc/stat reste le plus précis.
- who -b : donne le last boot 
- /etc/fstab : Linux system's file system , donne les 
- netstat: `apt-get install net-tools` donne les details de connection.
- ip addr: `hostname -I`
	- lo : loopback device virtual network present in all machine.
	- enps : nom de l'interface network.
	- ip addr show scope global: toute les interfaces qui ont un accès vers l'extérieur. 
	- mac address: identifier unique de la carte reseau.
- `journalctl _COM=sudo` : permet d'avoir toutes les commandes qui ont été exec par sudo.
	- Est mieux que sudo.log parce que prend depuis le debut de l'exec de la machine alors que sudo.log date depuis qu'on la setup dans le sudoers.
### CPU USAGE
- idle : A cpu is idle when it is not being used by any program.
- Non-idle task: just mean that when the cpu is used.
- CPU Usage : `(Total time Spent on Non-idle Tasks / Total time)x100`
	- To get the non idle time : Total time - idle time

## Cron
- utiliser le crontab -u root -e 
	- -u: specifie l'utilisateur
	- -e : edit le fichier crontab
- Il y a 1 crontab par user donc si on utilise la commande précédente on execute le script en tant que root.
# Source
[[Source Linux]]
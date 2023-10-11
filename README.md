# Tp01-Installation-Serveurs

## 2 Post Installation

### 2.1 Configuration SSH
Cette étape commence simplement par l'installation de SSH via la commande __apt install ssh__ qui installe tout le package SSH. On a ensuite modifier le fichier sshd_config pour permettre le configuration via le compte root. On a ensuite restart SSH afin qu'il reload et prenne en compte les changements fait sur le fichier de config.

### 2.2 
On peut maintenant tester la connexion vie la machine hote en utilisant __ping__ ainsi que l'adresse ip du serveur,si la machine répond bien, on peut enfin on se connecte à celui ci. 

### 2.3
Via la commande donnée __dpkg -l | wc -l__ on vérifie le nombre de paquet, on en a bien 320 mais on en observe un peu plus suite à l'installatio des packages SSH.

### 2.4
La racine représente moins de 1GO (vérifié avec la commande __df -h__, c'est le résultat d'une installation légère, pour un serveur qui fonctionne efficacement sans rien de superflu. 

### 2.5 Les commandes
La commande __echo $LANG__ permet de voir la langue local utilisé par défault de la machine. <br />
La commande __env__ permet elle de donner toutes les informations de l'environnement courant.<br />
__hostname__ permet elle de donner le nom de la machine ici, "serveur1".<br />
Pour obtenir le domaine il faut simplement utiliser la commande __domainname__, ici "none".<br />
__cat /etc/apt/sources.list | grep -v -E '^#|^$'__ : Cette commande donne tous les liens à partir desquels on installe les packages, tout en supprimant les lignes vide.<br />
__cat /etc/shadow | grep -vE ':\*:|:!\*:'__  : Cette commande donne l'ensemble des mot de passe du systeme en incluant celui de root.<br />
__cat /etc/passwd | grep -vE 'nologin|sync'__ : Cette commande donne l'ensemble des comptes utilisateurs n'aillant pas "nologin" ou "sync", cela est rendu possible grâce au "-v", ici on nous renvois donc seulement le compte "root".<br />
__fdisk -l__ et __fdisk -x__ : Ces deux commandes donnent, pour la première l'ensemble des disques présent sur la machine, ainsi que leurs informations. Pour le seconde, elle donne l'ensemble des partitions sur les disques, ici les 4 créés durant la crétion de la machine virtuel.<br />
__df -h__ : Cette commande, renvoit l'ensemble des chemins présent à la racine, on peut par exemple y trouver les chemins créé à la mise en place des partitions durant la création de la VM.<br />

 ### 3.1 Installation automatique
 __preseed__ : Cette commande sert à installer linux de manière automatique avec une configuration personnalisé, cela permet par exemple de l'installer en réseau sur un ensemble de machine par exemple.<br />

 ### 3.2 Rescue mode
 Pour changer un mot de passe oublier, on peut faire usage du mode "rescue shell", ce mode accessible via Grub au démarrage de la machine permet de modifier le contenu du menu grub afin d'accéder au shell de linux sans mdp, on peut donc ensuite réinitialiser le mdp root<br />

 ### 3.3 Redimensionnement partition
 Dans un premier temps on recréez la partition racine en lui mettant les paramètres de taille voulue. On supprime ensuite l'ensuite l'ancienne (on ne supprime que la partition, pas les données dessus). On choisit le bon fichier système pour la partition et enfin on redimensionne bien le fichier système afin que le système prenne bien en compte la nouvelle taille de la partition, et pour finir on remonte le disque, et on vérifie que le tout à bien été pris en compte.

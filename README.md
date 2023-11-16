⚠️CE PROJET A ÉTÉ RÉALISÉ DANS UN CADRE UNIVERSITAIRE. IL A ÉTÉ DÉPOSÉ SUR CE GIT POUR CORRECTION, LE CODE PEUT DONC CONTENIR DES ERREURS⚠️

# Tp01-Installation-Serveurs

## 2 Post Installation

### 2.1 Configuration SSH
Cette étape commence simplement par l'installation de SSH via la commande apt install ssh qui installe tout le package SSH. On a ensuite modifié le fichier sshd_config pour permettre la configuration via le compte root. On a ensuite restart SSH afin qu'il reload et prenne en compte les changements fait sur le fichier de config.

### 2.2
On peut maintenant tester la connexion via la machine hôte en utilisant ping, ainsi que l'adresse ip du serveur. Si la machine répond bien, on peut enfin s'y connecter.

### 2.3
Via la commande donnée dpkg -l | wc -l , on vérifie le nombre de paquets. On en a bien 320, mais on en observe un peu plus suite à l’installation des packages SSH.

### 2.4
La racine représente moins de 1GO (vérifié avec la commande df -h). C'est le résultat d'une installation légère, pour un serveur qui fonctionne efficacement sans rien de superflu.

### 2.5 Les commandes
La commande echo $LANG permet de voir la langue locale utilisée par défaut de la machine. <br />
La commande env permet, elle, de donner toutes les informations de l'environnement courant. <br />
hostname permet de donner le nom de la machine, ici "serveur1".<br />
Pour obtenir le domaine, il faut simplement utiliser la commande domainname, ici "none".<br />
La commande cat /etc/apt/sources.list | grep -v -E '^#|^$' donne tous les liens à partir desquels on installe les packages, tout en supprimant les lignes vides.<br />
La commande cat /etc/shadow | grep -vE ':*:|:!*:' donne l'ensemble des mots de passe du système en incluant celui de root.<br />

La commande cat /etc/passwd | grep -vE 'nologin|sync' donne l'ensemble des comptes
utilisateurs n'ayant pas "nologin" ou "sync". Cela est rendu possible grâce au "-v". Ici, on nous renvois donc seulement le compte "root".<br />
Les deux commandes fdisk -l et fdisk -x donnent, pour la première l'ensemble des disques présents sur la machine, ainsi que leurs informations. Pour le seconde, elle donne l'ensemble des partitions sur les disques, ici les 4 créés durant la création de la machine virtuelle.<br />
La commande df -h renvoie l'ensemble des chemins présents à la racine. On peut par exemple y trouver les chemins créés à la mise en place des partitions durant la création de la VM.<br />

### 3.1 Installation automatique
La commande preseed sert à installer linux de manière automatique avec une configuration personnalisée. Cela permet par exemple de l'installer en réseau sur un ensemble de machines.<br />

### 3.2 Rescue mode
Pour changer un mot de passe oublié, on peut utiliser le mode "rescue shell". Ce mode, accessible via Grub au démarrage de la machine, permet de modifier le contenu du menu afin d'accéder au shell de linux sans mdp. On peut donc ensuite réinitialiser le mdp root.<br />

### 3.3 Redimensionnement partition
Dans un premier temps, on recréé la partition racine en lui mettant les paramètres de taille voulus. On supprime ensuite l'ancienne (on ne supprime que la partition, pas les données dessus). On choisit le bon fichier système pour la partition et on redimensionne bien le fichier système afin que le système prenne bien en compte la nouvelle taille de la partition. Pour finir, on remonte le disque et on vérifie que le tout à bien été pris en compte.

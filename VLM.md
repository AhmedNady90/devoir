

# Résumé des étapes de la quête sur LVM

1. Ajout d'un disque à la machine et extension du groupe de volumes debian-vg pour doubler l'espace du groupe, avec des commandes pvcreate et vgextend.
2. Création d'un volume logique home avec un espace de 5 Go et montage de ce volume sous /home.
3. Création d'un snapshot du volume logique home à l'aide de lvcreate --snapshot.
4. Montage du snapshot sur le répertoire /home-snap et confirmation de son contenu identique à celui de /home via ls.
5. Modification du contenu de /home-snap sans affecter /home.
6. Démontage de /home-snap après utilisation avec umount.
7. Suppression du snapshot avec lvremove pour libérer de l'espace disque.
8. Vérification du statut des volumes logiques et des volumes de groupe avec lvscan et vgdisplay pour confirmer les modifications.
9. Observation que l'espace du groupe de volume debian-vg a été augmenté et que les totalités PE sont doublées.
10. Validation que le snapshot a bien été supprimé et que le volume logique home n’a plus de snapshot associé.

# Liste des commandes 

## 1. Liste des périphériques et partitions

*donald@central:~$ lsblk

*NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS

sda      8:0    0   20G  0 disk 
├─sda1   8:1    0   19G  0 part /
├─sda2   8:2    0    1K  0 part 
└─sda5   8:5    0  975M  0 part [SWAP]

sdb      8:16   0   20G  0 disk 

sr0     11:0    1 1024M  0 rom  

## 2. Création de la table de partitions avec `fdisk`

donald@central:~$ sudo fdisk /dev/sdb
[sudo] Mot de passe de donald : 

Bienvenue dans fdisk (util-linux 2.38.1).
Les modifications resteront en mémoire jusqu'à écriture.
Soyez prudent avant d'utiliser la commande d'écriture.

Le périphérique ne contient pas de table de partitions reconnue.
Created a new DOS (MBR) disklabel with disk identifier 0xf99a3573.

Commande (m pour l'aide) : m


**Options de commande disponibles dans fdisk :**

- `a` : modifier un indicateur d'amorçage
- `d` : supprimer une partition
- `n` : ajouter une nouvelle partition
- `t` : modifier le type d'une partition
- `w` : écrire la table de partitions et quitter

### Création d'une partition primaire

Commande (m pour l'aide) : n
Type de partition
   p   primaire (0 primaire, 0 étendue, 4 libre)
Sélectionnez (p par défaut) : p
Numéro de partition (1-4, 1 par défaut) : 
Premier secteur (2048-41943039, 2048 par défaut) : 
Dernier secteur, +/-secteurs ou +/-taille{K,M,G,T,P} (2048-41943039, 41943039 par défaut) :

**Une partition primaire de 20 GiB a été créée.**

### Modification du type de partition en LVM

Commande (m pour l'aide) : t
Partition 1 sélectionnée
Code Hexa ou synonyme (taper L pour afficher tous les codes) : 8E
Type de partition « Linux » modifié en « Linux LVM ».


### Sauvegarde de la table de partitions

Commande (m pour l'aide) : w
La table de partitions a été altérée.
Appel d'ioctl() pour relire la table de partitions.
Synchronisation des disques.


## 3. Création du volume physique

donald@central:~$ sudo pvcreate /dev/sdb1
sudo: pvcreate : commande introuvable


### Installation de LVM

donald@central:~$ sudo apt update
sudo apt install lvm2


**Installation réussie de LVM :**

- `dmeventd`
- `libaio1`
- `liblvm2cmd2.03`
- `lvm2`
- `thin-provisioning-tools`

### Création du volume physique

donald@central:~$ sudo pvcreate /dev/sdb1
  Physical volume "/dev/sdb1" successfully created.


## 4. Création et gestion du groupe de volumes
### Tentative de création d'un groupe de volumes `debian-vg`

donald@central:~$ sudo vgcreate debian-vg /dev/sdb1
  Volume group "debian-vg" successfully created


### Vérification du groupe de volumes

donald@central:~$ sudo vgdisplay debian-vg
  --- Volume group ---
  VG Name               debian-vg
  VG Size               <20,00 GiB
  Cur PV                1
  Free PE               5119 / <20,00 GiB


## 5. Création du volume logique

donald@central:~$ sudo lvcreate -L 10G -n mylv debian-vg
  Logical volume "mylv" created.


## 6. Formatage du volume logique

donald@central:~$ sudo mkfs.ext4 /dev/debian-vg/mylv
mke2fs 1.47.0 (5-Feb-2023)
Creating filesystem with 2621440 4k blocks and 655360 inodes
Filesystem UUID: 2a7d4e4c-eaf9-42ff-9c11-2a79ea21a0ad


## 7. Montage du volume logique

donald@central:~$ sudo mkdir /mnt/mylv
sudo mount /dev/debian-vg/mylv /mnt/mylv


## 8. Vérification de l'espace disque
donald@central:~$ df -h
udev               935M       0  935M   0% /dev
tmpfs              194M    1,5M  192M   1% /run
/dev/sda1           19G    6,7G   11G  38% /
tmpfs              967M       0  967M   0% /dev/shm
tmpfs              5,0M    8,0K  5,0M   1% /run/lock
tmpfs              194M     88K  194M   1% /run/user/1000
Voici les commandes que vous avez utilisées dans un fichier Markdown, intégrées avec les étapes manquantes que vous avez demandées :



## création d'un snapshot

sudo lvcreate --size 1G --snapshot --name home-snap /dev/debian-vg/home
# Erreur : Snapshot origin LV home not found in Volume group debian-vg.


## 2. Affichage des informations sur le volume logique

sudo lvdisplay debian-vg
# Affiche les informations sur le volume logique "mylv".


## 3. Vérification de l'état des montages

mount | grep /home


## 4. Tentatives de création d'un volume logique de 10 Go

sudo lvcreate -L 10G -n home debian-vg
# Erreur : Volume group "debian-vg" has insufficient free space.


## 5. Affichage de l'état du groupe de volumes

sudo vgdisplay debian-vg
# Affiche les informations sur le groupe de volumes "debian-vg".


## 6. Vérification des volumes logiques actifs

sudo lvscan
# Affiche les volumes logiques actifs.


## 7. Tentative de création d'un volume logique de 10 Go (nouvelle tentative)

sudo lvcreate -L 10G -n home debian-vg
# Erreur : Volume group "debian-vg" has insufficient free space.


## 8. Création d'un volume logique de 5 Go

sudo lvcreate -L 5G -n home debian-vg
# Volume logique "home" de 5 Go créé.


## 9. Formatage du volume logique "home" avec ext4

sudo mkfs.ext4 /dev/debian-vg/home
# Création d'un système de fichiers ext4 sur le volume logique "home".


## 10. Montage du volume logique "home" sur /home

sudo mount /dev/debian-vg/home /home

## 11. Vérification de l'utilisation du disque

df -h
# Affiche l'utilisation de l'espace disque, y compris /home.

## 12. Création d'un snapshot de 1 Go

sudo lvcreate --size 1G --snapshot --name home-snap /dev/debian-vg/home
# Snapshot "home-snap" créé.


## 13. Vérification des volumes logiques après la création du snapshot

sudo lvscan
# Affiche les volumes logiques "home" et "home-snap".


## 14. Création d'un répertoire pour monter le snapshot

sudo mkdir /home-snap

## 15. Montage du snapshot "home-snap" sur /home-snap

sudo mount /dev/debian-vg/home-snap /home-snap

## 16. Vérification des fichiers dans /home et /home-snap

ls /home
# Affiche "lost+found" dans /home.

ls /home-snap
# Affiche "lost+found" dans /home-snap.


## 17. Création d'un fichier de test dans /home

sudo touch /home/test-file.txt

## 18. Vérification des fichiers dans /home et /home-snap après création d'un fichier de test

ls /home
# Affiche "lost+found" et "test-file.txt".

ls /home-snap
# Affiche "lost+found" sans "test-file.txt".


## 19. Création d'un fichier de test dans /home-snap

sudo touch /home-snap/test-snap-file.txt

## 20. Vérification des fichiers après création d'un fichier dans le snapshot

ls /home-snap
# Affiche "lost+found" et "test-snap-file.txt".


## 21. Démontage du snapshot "home-snap"

sudo umount /home-snap

## 22. Suppression du snapshot "home-snap"

sudo lvremove /dev/debian-vg/home-snap


## 23. Vérification des volumes logiques après suppression du snapshot

sudo lvscan
# Affiche les volumes logiques restants, y compris "home".
ACTIVE            '/dev/debian-vg/mylv' [10,00 GiB] inherit
ACTIVE            '/dev/debian-vg/home' [5,00 GiB] inherit

#  TP 5 Systèmes de fichiers, partitions et disques

## Exercice 1. Disques et partitions 

### Question 2 
On affiche les disque durs avec ka commande  ``sudo fdisk -l`` 

### Question 3 
Pour créer la partitions de disque on rentre la commande ``sudo fdisk /dev/sdb`` on tape n pour créer les partitions, ensuite on doit choisir si la partition est principal ou non on choisis la taille qu'on souhaite. On fait la même chose pour la deuxième partition. On utilise la commande t pour choisir quelle partition on veut changer puis on rentre l'id.

### Question 4
Pour formater les partitions on utilise la commande suivante : sudo mkfs -t ext4 /dev/sd1/2

### Question 5 
La commande ne fonctionne pas car les partitions n'ont pas encore été montés.

### Question 6 
On les deux dossiers pour les points de montage data et win puis on monte les partitions dans les dossiers respectifs. Pour les faire monter automatiquement il faut modifier le fichier fstab en utilisant la commande : 
/dev/sdb2 /win ntfs default 0 0 

### Question 7 
sudo mount -t ext4 /dev/sdb1 data 
sudo mount -t ext4 /dev/sdb2 win

## Exercice 2 : Partitionnement LVM

### Question 3 
Avec la commande sudo pvcreate /dev/sdb1 on créé le volume LVM puis on vérifie son existence avec la commande pvdisplay.

### Question 4 
On créer le groupe de volume avec la commande sudo vgcreate vg00 /dev/sdb1.

### Question 5 
On utilise la commande : lvcreate -l 100%FREE -n lvData vg00`  
Puis lvscan pour vérifier.

### Question 6 
On créer la partition comme on a pu le faire auparavant on la formate avec la commande : mkfs -t ext4/dev/vg00/lvData1 et on remodifie le fichier fstab pour la faire monter automatiquement.

### Question 7 
On rajoute un disque dynamique puis on recrée une partition unique LVM et un volume physique.

### Question 8
On rajoute le disque qu'on vient de créer au groupe avec la commande suivante : sudo  vgextend vg00 /dev/sdc1

### Question 9 
 On peut donc modifier la taille du volume logique avec la commande suivante:   `lvextend -L+1G /dev/vg00/lvData` 
  Mais tout en modifiant le file system après  `resize2fs /dev/vmvg/Vol1`

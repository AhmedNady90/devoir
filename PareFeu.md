# Installer pfSense
Télécharge pfSense 
Créer une machine virtuelle 
Démarrer l'installation de pfSense à partir de l'image ISO
# Configurer les interfaces réseau :

WAN : C'est l'interface qui se connecte à l'extérieur
LAN : C'est l'interface qui connecte ton réseau interne.

# Tester que la machine cliente peut accéder à l'extérieur

 Une fois pfSense configuré, teste la connexion Internet à partir d'une machine cliente sur le réseau LAN.
# Mettre en place une règle de filtrage réseau pour interdire à la machine client de sortir du réseau interne
 Identifier l'adresse IP de la machine client 
#### Créer une règle de filtrage sur pfSense :
Va dans Firewall > Rules.
Sélectionne l'onglet LAN.
Ajoute une nouvelle règle en cliquant sur Add.
##### Dans la configuration de la règle :
Action : Block (Bloquer).
Interface : LAN.
Source : L'IP de la machine cliente (ex : 192.168.1.10).
Destination : Any (n'importe quel réseau).
Port source : Any.
Port destination : Any.
Description : Interdire accès Internet pour la machine cliente.
Enregistre la règle.
# Vérifier que la machine client ne peut plus communiquer avec l'extérieur
ping 8.8.8.8
##### La règle de filtrage mise en place sur pfSense permet de bloquer l'accès à l'extérieur pour une machine spécifique en fonction de son adresse IP source (mon cas, 192.168.1.100). Cette règle bloque toute communication sortante de cette machine, mais ne touche pas les autres machines du réseau local.

![firewallConfig](https://github.com/AhmedNady90/devoir/blob/main/PAREFEU1.PNG)
![configuration_règle](https://github.com/AhmedNady90/devoir/blob/main/FAREWALL2.PNG)
![machineClient_blocquée](https://github.com/AhmedNady90/devoir/blob/main/FAREWALL3.PNG)

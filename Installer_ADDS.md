# Préparation du serveur
Avant de commencer, assure-toi que ton serveur est configuré avec une adresse IP statique et que tu as les privilèges d'administrateur pour installer des rôles.

## Configurer une adresse IP statique :
Ouvre le Panneau de configuration.
Va dans Réseau et partage, puis Modifier les paramètres de la carte.
Clique droit sur la connexion réseau, puis choisis Propriétés.
Sélectionne Protocole Internet version 4 (TCP/IPv4), puis clique sur Propriétés.
Configure une adresse IP statique. Par exemple :
Adresse IP : 172.20.0.100
Masque: 255.255.255.0
## Installation du rôle Active Directory Domain Services (AD DS)
Ouvrir le Gestionnaire de serveur :

Lance le Gestionnaire de serveur (Server Manager) depuis la barre des tâches ou le menu Démarrer.
Ajouter le rôle AD DS :

Dans le Gestionnaire de serveur, clique sur Gérer (en haut à droite), puis sur Ajouter des rôles et fonctionnalités.
Dans l'assistant qui s'ouvre, clique sur Suivant jusqu'à la section "Sélectionner un rôle de serveur".
Coche la case Services de domaine Active Directory (AD DS).
Clique sur Suivant et continue à cliquer sur Suivant jusqu'à arriver à la page de confirmation.
Clique sur Installer pour ajouter le rôle AD DS. L'installation prendra quelques minutes.
Une fois l'installation terminée, ne ferme pas l'assistant, car tu devras promouvoir le serveur en contrôleur de domaine.
## Promouvoir le serveur en contrôleur de domaine
Une fois l'installation terminée, dans le Gestionnaire de serveur, tu verras un message en haut à droite qui te propose de Promouvoir ce serveur en contrôleur de domaine. Clique dessus.

Choisir l'option de promotion :

Sélectionne Ajouter un nouveau domaine dans une nouvelle forêt.
Clique sur Suivant.
Nom du domaine :

Dans la section Nom de domaine racine, entre wilders.lan.
Clique sur Suivant.
Choisir le niveau fonctionnel de la forêt et du domaine :

Laisse les niveaux fonctionnels par défaut pour Windows Server 2012 R2. Ils seront compatibles.
Clique sur Suivant.
Options de contrôleur de domaine :

Laisse les options par défaut (DNS et GC activés).
L'option Réplication du catalogue global doit être activée par défaut.
Clique sur Suivant.
Mot de passe du mode de restauration des services d'annuaire (DSRM) :

Choisis un mot de passe fort pour le compte Mode de restauration des services d'annuaire. Ce mot de passe est utilisé pour restaurer AD en mode hors ligne en cas de problème.
Clique sur Suivant.
Vérification :

L'assistant vérifiera la configuration. Si tout est correct, tu verras une confirmation de la configuration.
Clique sur Installer.
Redémarrage du serveur :

Le serveur redémarrera automatiquement une fois l'installation terminée pour appliquer les modifications et devenir un contrôleur de domaine.
## Vérification du domaine
Après le redémarrage, ton serveur sera le contrôleur de domaine principal du domaine wilders.lan.

Pour vérifier la configuration du domaine :

Ouvre Active Directory Users and Computers.
Tu devrais voir le domaine wilders.lan dans l'arborescence.
![Texte alternatif](https://github.com/AhmedNady90/devoir/blob/main/ADDS.PNG)

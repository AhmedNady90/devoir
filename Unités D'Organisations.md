## Créer l'Unité d'Organisation (OU) "Wilders_students"
Ouvre Active Directory Users and Computers :
Crée l'OU "Wilders_students" :

Dans le panneau de gauche, clique sur wilders.lan pour sélectionner ton domaine.
Fais un clic droit sur wilders.lan, puis sélectionne Nouveau > Unité d'organisation.
Dans la boîte de dialogue qui s'ouvre, entre le nom de l'OU : Wilders_students.
Clique sur OK.
L'OU Wilders_students est maintenant créée dans ton domaine wilders.lan.

## Créer un Groupe d'utilisateurs "Students"
Fais un clic droit sur Wilders_students, puis sélectionne Nouveau > Groupe.
Dans la boîte de dialogue, entre les informations suivantes :
Nom du groupe : Students
Type de groupe : Choisis Sécurisé (par défaut) si ce n'est pas déjà sélectionné.
Portée du groupe : Choisis Global (par défaut).
Clique sur OK.
Le groupe Students est maintenant créé dans l'OU Wilders_students.

## Créer un utilisateur dans le groupe "Students"
Fais un clic droit sur Wilders_students, puis sélectionne Nouveau > Utilisateur.
Dans la boîte de dialogue Nouveau Utilisateur, remplis les champs suivants :

Prénom : Ahmed
Nom d'ouverture de session (nom d'utilisateur) : nady

## Ajouter l'utilisateur au groupe "Students"
Fais un clic droit sur l'utilisateur Ahmed, puis sélectionne Propriétés.
Dans la fenêtre des propriétés, va à l'onglet Membre de.
Clique sur Ajouter.
Tape Students dans le champ de recherche, puis clique sur Vérifier les noms pour confirmer.
Sélectionne Students et clique sur OK.
![Texte alternatif](https://github.com/AhmedNady90/devoir/blob/main/ADDS2.PNG)

##  Créer une GPO nommée "Wilders"
Ouvrir la console de gestion des stratégies de groupe (GPMC) :
Sur un contrôleur de domaine ou un ordinateur avec les outils d'administration, ouvrez le Gestionnaire de stratégie de groupe en exécutant gpmc.msc dans la boîte de dialogue Exécuter (Win + R).
Créer une nouvelle GPO :
Dans l'arborescence de gauche de la console GPMC, cliquez sur Forêts > Domaines > votre domaine (par exemple, example.com).
Faites un clic droit sur Objets de stratégie de groupe et sélectionnez Créer un GPO dans ce domaine, et le lier ici.
Nommez la GPO Wilders.
Cliquez sur OK pour créer et lier la GPO au domaine.
## Modifier la GPO pour restreindre l'accès au Panneau de configuration
Modifier la GPO :

Faites un clic droit sur la GPO Wilders que vous venez de créer et sélectionnez Modifier.
L'Éditeur de gestion de stratégie de groupe s'ouvrira.
Configurer les restrictions pour le groupe Wilders_Students :

Dans l'Éditeur de stratégie de groupe, allez à l'emplacement suivant :

Configuration utilisateur > Paramètres Windows  > Stratégies > Modele d'adminstartion > Panneau de configuration.
Désactiver l'accès au Panneau de configuration :

Désactiver l'accès au Panneau de configuration via l'option "Interdire l'accès aux outils d'administration" :
Dans la section Options de sécurité, recherchez la stratégie "Interdire l'accès aux outils d'administration".
Double-cliquez sur cette stratégie et définissez-la sur Activé.
Cela restreindra l'accès aux outils d'administration, y compris le Panneau de configuration.
![Exemple d'image](https://github.com/AhmedNady90/devoir/blob/main/GPO1.PNG)
## Restreindre cette stratégie au groupe Wilders_Students :

Pour appliquer cette GPO uniquement au groupe Wilders_Students, vous devrez filtrer son application en fonction des groupes.
Allez à la GPO dans la GPMC, faites un clic droit sur Wilders, puis sélectionnez Modifier les délégations.
Ajoutez le groupe Wilders_Students dans la section Filtrage de sécurité et donnez-lui la permission Appliquer la stratégie de groupe.
Cela permettra de cibler cette GPO spécifiquement sur les membres du groupe Wilders_Students.
![Exemple d'image](https://github.com/AhmedNady90/devoir/blob/main/GPO2.PNG)
## Testez avec un utilisateur du groupe Wilders_Students pour vérifier l'application de la restriction.

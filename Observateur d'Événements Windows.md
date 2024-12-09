# Surveillance DNS - Vue personnalisée
Cette vue personnalisée a été configurée dans l'Event Viewer
## Objectif
L'objectif de cette vue est de permettre aux administrateurs de surveiller les activités du serveur DNS, y compris :
- Les démarrages et arrêts du serveur DNS.
- Les erreurs de résolution de noms.
- Les échecs de chargement des zones DNS.
- Les problèmes de réplication DNS.
## Critères de surveillance :
## Format de la vue
- **Niveaux de log** : Critique, Erreur, Avertissement, Information
### Sources d'événements :
- **DNS-Server-Service** : Événements du serveur DNS.
- **DNS Client Events** : Événements liés au client DNS.
- - **Événements critiques** :
  - 2 : Démarrage du serveur DNS
  - 4 : Arrêt du serveur DNS
  - 409 : Erreur de résolution de nom
  - 501, 502 : Échec de chargement de zone
  - 6001, 6002 : Problèmes de réplication DNS

## Fichier XML
Le fichier XML ci-joint peut être importé directement dans l'Event Viewer pour appliquer cette vue personnalisée.


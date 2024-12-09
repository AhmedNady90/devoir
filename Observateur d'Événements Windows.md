# Surveillance DNS - Vue personnalisée

## Critères de surveillance :
- **Événements critiques** :
  - 2 : Démarrage du serveur DNS
  - 4 : Arrêt du serveur DNS
  - 409 : Erreur de résolution de nom
  - 501, 502 : Échec de chargement de zone
  - 6001, 6002 : Problèmes de réplication DNS

## Format de la vue
- **Niveaux de log** : Critique, Erreur, Avertissement, Information
- **Sources** : DNS-Server-Service, DNS Client Events

## Fichier XML
Le fichier XML ci-joint peut être importé directement dans l'Event Viewer pour appliquer cette vue personnalisée.


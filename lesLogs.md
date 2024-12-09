# Installation et configuration du serveur Web (Apache)
sudo apt update
sudo apt install apache2
## Configuration des logs
les fichiers de logs sont dans le fichier de configuration:  /etc/apache2/sites-available/000-default.conf
 # Génération du trafic sur le serveur Web
curl http://localhost
curl http://localhost/404
curl http://localhost/somepage
 Accès à la page d'accueil du serveur via un navigateur (http://localhost)
## Analyse des logs

Après avoir généré du trafic, j'ai analysé les logs générés dans le fichier /var/log/apache2/access.log. 
Voici un extrait des logs d'accès : ![Logs d'acces](chemin/vers/l'image.jpg)
### Identification des requêtes réussies et des erreurs
Requêtes réussies (code 200)
    GET / : La page d'accueil a été accédée avec succès.
    GET /icons/ubuntu-logo.png : L'image ubuntu-logo.png a été livrée correctement.

Erreurs 404 (page non trouvée)
    GET /favicon.ico : L'icône du site favicon.ico n'a pas été trouvée, ce qui a généré une erreur 404.
  ###  Fréquence des adresses IP
 utilse:  awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -nr
 resultat :10 127.0.0.1 ![IP plus frequente](https://github.com/AhmedNady90/devoir/blob/main/IPplus%20Frequente.png)
## Explication de la structure des logs Apache
##### Adresse IP du client : C'est l'adresse IP du client qui fait la requête (ici 127.0.0.1 pour localhost).
##### Date et heure de la requête : La date et l'heure à laquelle la requête a été effectuée, avec le fuseau horaire.
##### Méthode HTTP et URL demandée : La méthode utilisée pour la requête (par exemple, GET) et l'URL demandée.
##### Code de statut HTTP : Le code de statut retourné par le serveur (par exemple, 200 pour succès, 404 pour une erreur).
##### Taille de la réponse : La taille de la réponse envoyée par le serveur (en octets).
##### Referrer : L'URL de la page précédente, si disponible.
##### Agent utilisateur : L'agent utilisateur qui identifie le navigateur ou l'application effectuant la requête.

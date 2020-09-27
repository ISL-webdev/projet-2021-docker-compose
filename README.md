# Institut Saint-Laurent de Promotion Sociale : Projet Web Dynamique (Web Developer 3 | 1084) 

## Annuaire Bien-Être

Repository et Exemples de code liés au cours

--- 

### La configuration de l'infrastructure serveur se fera dans Docker via docker-compose

Les fichiers sources sont stockés sur la machine hôte afin d'accélerer les temps de lecture/écriture et permettre l'indexation dans l'IDE.
La configuration des containers se situe dans le répertoire `.docker`  
    
Nous utiliserons majoritairement 3 containers (services). D'autres services pourront s'ajouter par la suite (ex: un container contenant nodejs pour l'utilisation de Webpack/Encore):
    
   * **database** : se base sur une image mysql-8 ou mariadb et utilise un volume (_data_) pour assurer la persistance des données. Expose le port `3306`
   * **nginx** : le serveur web, devra avoir accès au répertoire `public` de notre projet. Expose les ports `80` et `443` (ssl, pour le https). Les volumés montés sont en lecture seule
   * **php** : `php-7.4` L'interpréteur php communique avec ngnix sur le port `9000` (interne à docker) . Aura accès en lecture à l'entièreté du répertoire du projet
   
Pour démarer le projet :

- Cloner ce repository sur votre machine
- `cd .docker`
- copier le fichier `.docker/.env.dist` vers `.docker/.env` et compléter avec vos paramètres
- exécuter `docker-compose build && docker-compose up -d`
- lorsque les containers sont démarrés, vous pouvez créer un nouveau projet `docker-compose exec symfony new src`
- vous pouvez executer les commandes utiles comme **composer** et **bin/console** de deux manières : 
    - soit à l'intérieur du container => `docker-compose exec php sh` pour se connecter au shell
    - soit à l'extérieur `docker-compose exec php composer require doctrine` ou `docker-compose exec php symfony console cache:clear` 
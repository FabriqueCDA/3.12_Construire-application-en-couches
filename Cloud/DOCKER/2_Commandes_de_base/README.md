
# Commandes de base

La gestions de Docker avec l'interface en ligne de commande CLI   
La doc complète [ici](https://docs.docker.com/engine/reference/commandline/cli/)

Liste des commandes

     docker

Un example la version de docker

     docker -v

Infos docker

     docker info


## Gestion des images

Affichons la liste des images en local - **image ls**

     docker image list



Recherchons une image de NodeJS dans DockerHub- **search**

     docker search node


Installez la dernière image de NodeJS Official - **pull**

     docker pull node:latest


Vérifier l'installation avec `image list`

Lancer et accéder au bash de l'image NodeJS Official - **run**

     docker run -it node:latest bash

```
-i STDIN Ouvert
-t Afficher le terminal
```

Vous êtes maintenant sous linux dans l'image docker, essayer `ls`et `node -v`

Votre image est donc bien dans un environnement Linux avec NodeJS installer.

Pour sortir: `exit`

Et aussi pour détruire le container automatiquement à la fin de l'exécution - **--rm**

     docker run -it --rm node:latest bash

   

## Gestion des containers

Liste des containers actifs - **ps**

     docker ps

List des containers actifs et inactifs  - **ps -a**

     docker ps -a

Dernier container créé  - **ps -l**

     docker ps -l

Démarrer un conteneur - **start**

     docker start IDCONTAINER

Arrêter un conteneur - **stop**

     docker stop IDCONTAINER

Exécuter une commande sur un conteneur démarré - **exec**

     docker exec OPTIONS IDCONTAINER COMMANDE

par exemple connaitre la version de NodeJS sur le container en execution du container node
``` docker exec IDCONTAINER node -v```




## Exercice 1

Trouver l'identifiant du dernier container créé (NodeJs normalement)    
Utiliser la commande Docker `start` pour le relancer     
Executer la commande `bash` dans ce container en utilisant la commande `exec` et l'option `-it`    
Lister les dossiers du container avec `ls`    

## Exercice 2

Tester et chercher la doc des commandes Docker suivantes:
```
rm       
kill   
attach   
restart
purge
system prune
```

et les Options de la commande `run`

```
--name 
--dns 
--net
--add-host 
--link
-i
-t
-p
-d
-e
-c 
-v 
```
## Exercice 3

Dans le container nodeJS copier un programme type console.log("Hello blabla") utilisant node.js,    
créer le fichier js en local et le copier dans le container avec `cp`,    
executer le script avec `docker exec`.   

## Exercice 4

Dans le même ordre d'idée, implémnter un serveur web sur une image docker, en prenant l'exemple de serveur web de nodejs.



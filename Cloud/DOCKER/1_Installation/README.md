
# Docker Installation
> Compétences : 

## Installation sur Ubuntu 20
Mise à jour des paquets   

    sudo apt update

Permettre à apt d'utiliser les paquets sur HTTPS

    sudo apt install apt-transport-https ca-certificates curl software-properties-common

 

Ajout de la clé GPG du dépôt officiel Docker

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

 

Ajoutez le dépot Docker

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
    sudo apt update
 

Vérification du dépôt Docker

    apt-cache policy docker-ce

Réponse si Ok:
````
docker-ce:
  ...
   500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
`````
Final: installons Docker

    sudo apt install docker-ce


## Vérification de l'installation


    sudo systemctl status docker


## Docker sans sudo
    sudo gpasswd -a $USER docker


## Hello-world

Installer et exécuter votre première image docker

     docker run hello-world

L'image sera téléchargée depuis dockerhub puis exécutée.
[Liste des images dans Explorer ici](https://hub.docker.com/)


## Exercice

Retrouver et lire le contenu des 2 fichiers lancant les services/démons de docker (`systemctl`)   
indice: l'un d'eux est `docker.service`

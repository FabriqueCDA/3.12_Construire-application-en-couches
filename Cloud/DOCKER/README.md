# DOCKER

## Les containers

La conteneurisation est une virtualisation légère.     
Contrairement à une machine virtuelle qui utilise un hyperviseur avec son propre noyau lent à démarré et gourmand en ressources, chaque conteneur accède à un seul noyau de système d'exploitation.    
Plusieurs conteneurs peuvent coexister en ayant chhacun un environnement dédié pour gérer une application, ses dépendances, ses bibliothèques et cela en utilisant moins de ressources.   

## La terminologie Docker

**Docker client**   
Il s'agit de la commande docker utilisée pour contrôler la plupart du flux de travail Docker et communiquer avec les serveurs Docker distants.   

**Docker server** 
Il s'agit de la commande dockerd qui est utilisée pour démarrer le processus du serveur Docker qui construit et lance des conteneurs via un client.   

**Docker images** 
Les images Docker se composent d'une ou plusieurs couches de fichiers systèmes et de certaines métadonnées importantes qui contiennent tous les éléments nécessaires pour exécuter une application Dockerisée.
Une seule image Docker peut être copiée sur de nombreux hôtes.
Une image a généralement à la fois un nom et une balise (TAG). La balise est généralement utilisée pour identifier une version particulière d'une image.

**Docker container**   
Un conteneur Docker est un conteneur Linux qui a été instancié à partir d'une image Docker.
Un conteneur spécifique ne peut exister qu'une seule fois, cependant, vous pouvez facilement créer plusieurs conteneurs à partir de la même image.

**Atomic host**        
Un hôte atomique est une petite image de système d'exploitation finement réglée, comme Fedora CoreOS, qui prend en charge l'hébergement de conteneurs et les mises à niveau du système d'exploitation atomique.
 
## Pourquoi sont ils si utilisés ?

Les conteneurs sont plus **rapides**: ils sont également plus légers et plus fiables que les autres formes de virtualisation.

Les conteneurs sont **polyvalents**: ils fonctionnent sous Linux et Windows et sur un certain nombre de spécifications matérielles.

**Pas cher** : en ce qui concerne la technologie de virtualisation, les conteneurs sont relativement peu coûteux à mettre en œuvre.

**Facilité** d'utilisation: les conteneurs aident à simplifier le développement d'applications.

**Flexible et multiplateforme** : le plus grand avantage est peut-être que les conteneurs créent des environnements identiques quel que soit l'environnement.

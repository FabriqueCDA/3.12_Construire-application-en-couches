# Le stockage, un truc dingue
AWS propose plein de types de stockages différents.
Nous avons vu les EBS qui sont des disques de travail qui s'effacent au redémarrage d'une instance.
On va ajouter un plus pérenne à l'une ou l'autre de nos instances. Attention, chaud devant !

## Les types de stockages d'AWS
- S3, Simple Storage Service, le premier créé, le plus utilisé, une base. Permet de stocker des documents de tous types d'une taille maximale de 5To.
- EBS, Elastic Block Storage, sont des disques virtuels plus classiques, on les a déjà utilisés
- enfin, Glacier est un service de stcokage longue durée mais avec un délai de disponibilité plus long. Ce service est dédié.

## Zoom sur S3
Le service fonctionne avec des 'buckets', compartiments en français. Il n'y a virtuellement pas de limite au nombre d'objets que vous pouvez socker ([bien qu'on puisse voir que ça crée de l'abus...](https://linformaticien.com/scaleway-inquiet-de-la-cryptomonnaie-chia/)).
Dans S3, le concept est de créer des compartimenents et d'y stocker des documents dedans. Chaque compartiment a une adresse DNS, un nom et une région.
Chaque document a des métadonnées qui lui sont attachées. Ils ont :
- un ARN pour y accéder avec des services
- une URI S3 interne
- une URL pour l'afficher
- des autorisations d'accès
- et potentiellement des versions
Les compartiments ont le même genre d'informations (comme toutes les ressources et services AWS on pourrait dire).

Ce service ne paye pas de mine de premier abord mais c'est en fait une machine de guerre qui permet de gérer chaque document individuellement avec des accès en fonction de paramètres spécifiques si besoin est. A l'usage, cette technologie s'avère être d'une capacité sans borne pour des développeurs.

> Interlude : on vous laisse vous amuser à créer des compartiments et à mettre des fichiers dedans. On se revoit dans une demie heure pour comparer vos essais. On en profite pour extraire des règles de sécurisation des accès.

### Héberger son site Web sur S3
Si vous faites un site statique avec de l'Ajax, vous pouvez l'héberger sur S3.
Retournez sur un compartiment créé, activez la fonction en bas, 'Hébergement de site Web statique'.
Indiquez le nom du fichier d'index, celui de l'erreur 404 et voilà, c'est fait.

Nous aborderons la question des notifications à notre prochaine session pour aller plus loin sur les services d'AWS.

## Les disques EBS
Ces disques vont permettre la persistance des données. Plus encore, on peut les crypter, en faire des snapshots et on bénéficie d'une haute disponibilité. En effet, ces disques sont dupliqués automatiquement dans les serveurs pour garantir leur persistance et la récupération des données.

Pour en créer, cliquez sur 'Volumes' dans Elastic Block Store. Ajoutez un volume, choisissez 'SSD à usage général', mettez la taille que vous voulez (attention au prix ^^). Comme d'hab', choisissez la zone mais faite attention à ce qu'elle soit la même que l'instance sur laquelle vous voulez la mettre.
Vous pouvez même faire un disque à partir d'un instantané (snapshot) pour le créer avec des données dedans.

Une fois votre volume créé, vous pouvez le sélectionner et dans 'Actions' choisir 'Attacher le volume' pour l'attacher à une instance. Linux va vouloir un disque sous la forme 'dev/sdf' par exemple. Ce choix va compter pour les actions suivantes.

> Attention, attacher un volume à une instance ne va pas dire qu'elle sera reconnue par Linux. C'est votre challenge maintenant. A vous de trouver comment on fait dans Linux.
# Créer une infrastructure pas à pas
> Compétence métier : 
> Construire une application organisée en couches
> Préparer et exécuter le déploiement d’une application

Nous avons vu comment utiliser CloudFormation pour créer un serveur complet avec tous les services attachés.
Le principe de CloudFormation est d'orchestrer tout un ensemble de services pour produire une infrastructure complète. Lors de la création d'une pile vous aurez remarqué les étapes se dérouler.
Nous allons recréer ces différents services et les orchestrer à la main pour apprendre à manipuler AWS plus en détail.

Dans la suite nous allons :
- recréer un serveur EC2 : stockage, balises, sécurité
- ajouter une adresse IP élastique (fixe, les adresses ip de base peuvent changer)
- ajouter un volume pour étendre le stockage et le monter sur le serveur
- la répartition de charge

## Créer un serveur EC2
1 - Dans le service EC2, cliquez sur 'Lancer une instance > Lancer une instance'. On choisit Amazon Linux 2, 64 bits x86 pour pas se galérer sur les logiciels.
Cette instance a un stockage EBS de 8Go non permanent.
2 - On reprend un t2.micro.
3 - On modifie les groupes de sécurité pour donner un accès HTTP. Cliquez sur modifier le groupe de sécurité, avec l'option 'Créez un groupe de sécurité'. Ajoutez les ports 80 et 443, HTTPS et HTTP. UNe fois fait, 'Vérifier et lancer'
4 - Ca vaut le coup de jeter un oeil à 'Modifier les détails de l'instance'. Il y a foule d'option parmis lesquelles, la possibilité de prendre une instance au meilleur prix, de l'intégrer à un réseau et un sous réseau, à l'intégrer à un ensemble scalable... C'est riche et captivant.
5 - Stockage, on ne touche pas. On ne peux ajouter ici que des disques ESB, on en a déjà un, ça suffit. On fera mieux après.
6 - Vous pouvez créer des balises. Elles permettront d'accéder à l'instance par du code.
7 - 'Lancer' vous demande de sélectionner une pair de clés SSH.

Et voilà, l'instance se crée comme tout à l'heure. On a déjà utilisé des éléments que nous avions créé préalablement.

> On se fait un petit intermède. Ajoutez un fichier index.html dans le serveur Web de chaque instance (en accès SSH vers /var/www/html) pour afficher un message lorsqu'on affiche l'adresse de l'instance publique.

## On attache des adresses IP fixes
La première sur une instance sera gratuite, les autres... pas chère mais facturées.
Les adresses IP des instance sont réinitialisées à chaque redémarrage. Dans le processus réseau interne de AWS, elles sont en DHCP comme vos routeurs.
Pour ce faire, rien de plus simple. Dans la page des instances EC2, sur le menu de gauche allez dans 'Adresses IP Elastic', créez une adresse IP en choisissant Amazon.
Une fois créée, sélectionnez là, 'Actions > Associer l'adresse IP Elactic'. Choisissez votre instance, l'adresse privé en lien et cochez la case 'Autoriser la réassociation de cette adresse IP Elastic'.
Et voilà, c'est fait, vos instances ont des IP fixes, comme des grands.

Toute cette démarche est peu ou prou ce que vous faites lorsque vous commandez un VPS chez OVH par exemple.

## ELB, Elastic Load Balancing || Un équilibreur de charge
Nous sommes prêts pour un peu de répartition de charge avec l'équilibreur.
Trouvez le dans les services, ajoutez en un nouveau et voyons quelques options :
1 - on choisit 'HTTP/HTTPS', c'est la grande majorité des usages. 'TCP' est pour les flux plus importants sur des données autres. 'IP' c'est pointu et 'Classic Load Balancer' est pour l'ancien système.
- On lui donne un nom, accessible depuis Internet, IPV4
- Protocole, on ne touche pas
- Notez que VPC est déjà rempli. C'est un réseau privé créé avec votre compte initial. Il servira de support à notre répartiteur
2 - Cliquez sur deux zones. En effet, le répartiteur permet de gérer des répartitions dans plusieurs zones au cas ou une s'effondrerait (suite à un incendie par exemple...). A chaque fois un sous réseau est créé. Passez à la suite
3 - Le groupe de sécurité par défaut nous suffira ici. Il laisse passer tout le trafic (probablement default VPC security group)
4 - On attaque le routage avec un nom. On choisira l'option 'Instance' pour gérer nos instances, le protocole reste sur HTTP, ça nous va bien.
La version du protocole HTTP1 correspond au trafic Web + Web Socket. Pas mieux.
5 - Vérification de l'état dans le routage. Cette option sert à vérifier l'état des instances et à éliminer momentanément une instance qui ne serait pas fonctionnelle à un instant T. Laissez les options de base. 
Notez le code de sécurité, 200, une notion intéressante à considérer sur les renvoies éventuels de ping de vos serveurs.
6 - On ajoute nos cible, les instances qu'on vient de créer et voilà, plus qu'à valider et créer.
# AWS - From scratch
> Compétences : Construire une application organisée en couches, concevoir une application, préparer et exécuter le déploiement d’une application.

## Un serveur Linux en 5 minutes (environ) avec CloudFormations
CloudFormation est un service de AWS, un parmis la multitude, qui permet de créer un serveur EC2 clé en main et de paramétrer tout ce dont vous aurez besoin pour l'utiliser.

### Une clé SSH
Avant de créer notre serveur nous allons nous faire une clé SSH qui nous sera demandée au moment de sa création.
Dans la page du service EC2, sélectionnez l'onglet 'Paires de clés'. Ajoutez-en une. Un fichier vous sera proposé un téléchargement.
En fonction de votre système, choisissez un fichier PEM ou PPK.
Sur Linux, il faudra le place dans le dossier ssh comme suit avec des droits chmod en 400 :
- dossier /home/MonUtilisateur/.ssh
- chmod 400 /home/MonUtilisateur/.ssh/MonFichier.pem

### Créer notre serveur avec CloudFormation
Dans la console AWS recherchez le service CloudFormation (dans le groupe Gestion et gouvernance).
Sur la page du service, cliquez sur Créer une pile. Quelques informations vous seront demandez :
1 - Utiliser un exemple de modèle
2 - Dans la liste 'Exemples de modèles', choisissez le premier LAMP Stack (notez la présence de plein d'autres options)
3 - Cliquez sur 'Suivant'
4 - Renseignez les éléments de base de données (nom, mot de passe...)
5 - Choisissez le type de votre instance ([toutes les infos ici](https://aws.amazon.com/fr/ec2/instance-types/)) (t2.micro est compris dans l'offre gratuite)
6 - Choisissez une paire de clés pour les accès SSH (cf. si après)
7 - On ne touche pas pour l'instant aux configurations > 'Suivant'
8 - Vérifiez les données saisies et lancez votre pile 'Créer une pile'

L'instance va s'initialiser et de créer, ça prend un peu de temps, quelques minutes généralement. Dans le processus, AWS va monter un serveur EC2, créer une base de données RDS (celle dont on aura renseigné les informations), installer LAMP et paramétrer les services Linux.
Notez que la distribution est un Linux Amazon optimisée pour ses services. 

### Notre instance
Dans les services AWS, choisissez EC2. Vous y trouverez une page générique pour accéder à la liste de vos instances EC2 (Instances (en cours d'exécution), Instances), les volumes, les groupes de sécurité (généralement créés par défaut), l'équilibrage de charges (loadbalancer), les paires de clés (pour le SSH).
C'est chargé, riche. Vous aurez des commentaires oraux.
L'onglet 'Instances' vous aurez accès à la liste de vos instance EC2. Cliquez sur celle que vous souhaitez administrer.

Quelques informations sur les instances :
- ID d'instance : l'id de votre instance, utile pour la connexion SSH notamment
- IPv4 : l'adresse IP du serveur
- Adresses IP Elastic : des IP adjointe qui peuvent être attribuées à d'autres instances (pour passer de l'une à l'autre par exemple)
- DNS Ipv4 public : le domaine de votre serveur
- les pendants privés servent dans le réseau local et seront utiles pour l'équilibrage de charges par exemple
- AMI : les AMI sont les images, des serveurs qui sont dipliquées (pour information)

Voilà quelques infos intéressantes.
### Se connecter à son instance
Aller sur la page de votre instance et cliquer en haut à droite sur se connecter. Le lien de connexion est donné dans l'onglet 'Client ssh'.
Utilisez le en remplaçant le fichier pem vers l'adresse locale de votre fichier et hop, vous voilà sur votre serveur.

# Des infos sur le capot
Au plus court, Cloud Formation, un service intégré, facile à utiliser qui vous donnera du clé en main.
[L'aide est ici](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html) mais pas de panique, nous allons l'utiliser ensemble.
Nous allons mettre en oeuvre plusieurs services de AWS pour cette partie du cours. Les voici :
- [EC2 pour créer des serveurs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) (nous restons sur les distributions Linux de AWS)
- [Route 53](https://docs.aws.amazon.com/route53/?id=docs_gateway) pour attacher des domaines
- [RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) et [Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html) pour les bases de données
- Scaler son infrastructure (y aura du clé en main)
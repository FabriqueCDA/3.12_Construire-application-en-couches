# AWS - From scratch
> Compétences : Construire une application organisée en couches, concevoir une application, préparer et exécuter le déploiement d’une application.

## IAM - les droits et autorisations
Le principe des droits et autorisations sur les services de Cloud touchent :
- les utilisateurs
- les groupes d'utilisateurs
- les rôles
- les stratégies (policies)
- les services qui dialoguent entre eux (par exemple une lambda faisant appel à une base de données ou S3)
Jetez un oeil à ce document de [AWS sur IAM](https://docs.aws.amazon.com/fr_fr/IAM/latest/UserGuide/introduction.html)

### Les utilisateurs
Les utilisateurs ont des droits qui leur sont attachés et peuvent être modifiés (ajoutés, enlevés...). Ces droits s'appliquent uniquement à l'utilisateur donné.
### Les groupes
Comme leurs noms l'indiquent, les groupes regroupent des utilisateurs. Des stratégies peuvent leur être attachées. Ils permettent une gestion centralisée des stratégies de sécurité.
### Les rôles
Ce sont des ensembles de stratégies qui sont utilisées pour les services lorsqu'ils doivent fonctionner entre eux. Par exemple, une lambda qui veut faire appel à des données SQL.
### Les stratégies
Une stratégie est attachée à un service et permet d'agir dessus : lecture, écriture, accès partiel, total... Nombre de stratégies pour chaque service. Elles permettent une action millimétrée pour garantir une sécurité maximale.
Toutes les actions que vous mènerez seront en lien avec des stratégies.
### JSON
En arrière plan de tous ces systèmes de paramétrages se trouvent des fichiers JSON. Jetez un oeil sur une stratégie.
Ce sont des paramètres qu'il faudra apprendre à maîtriser petit à petit si vous voulez avancer dans la maîtrise du système.
On les retrouvera un peu partout.
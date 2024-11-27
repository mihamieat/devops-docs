# Introduction à AWS
###  Modèle de déploiement
- L'informatique cloud est la fourniture *à la demande* des resources informatiques, avec un paiement généralement à l'utilisation.
- Avantages AWS :
	- paiement à l'utilisation
	- économies d'échelle
	- scalabilité des resources
	- gain de temps
	- économique
	- disponibilité
### Infrastructure
- AWS a une infra mondiale avec des *datacenters*, des *zones* de disponibilité et des *régions*, choisies en fonction de la *conformité*, de la *latence*, du *prix* et de la *disponibilité* des services.
- Availability zone (AZ) : comprend un ou plusieurs *datacenters* avec une alimentation *électrique*, un *réseau* et une *connectivité* redondants.
- Choisir sa région selon la conformité, la latence, le prix et la disponibilité des services.
### Interaction
- Différent avec une interaction physique où on peut avec un accès directe.
- interface web, cli, SDK
- ***Console*** de gestion AWS
- ***AWS CLI***
- ***API AWS***
### Sécurité
- Modèle de ***responsabilité partagée*** :
- ![[Pasted image 20241125095953.png]]
- AWS est responsable de la sécurité de l'infra cloud.
- l'utilisateur ***root*** a un accès ***illimité*** à tout dans le compte. Il est *essentiel* de ***sécuriser** l'accès*.
- ***MFA*** (multi factor authentication) : couche de sécurité supplémentaire. Elle oblige l'utilisateur à utiliser un mécanisme MFA pris en charge en plus de leurs informations de connexions habituelles.
- ***IAM*** (identity and access management) : service qui *gère les accès au compte* *et aux resources* AWS. *Authentication* & *Authorization*. 
- Un ***utilisateur IAM*** sur AWS représente ***une personne*** ou ***un service*** qui *interagit* avec ***AWS***.
- Un ***group IAM*** est un ***ensemble d'utilisateurs AWS*** qui *héritent* des permissions assignés à ce groupe.
- Pour gérer l'accès et fournir des permissions aux services et ressources AWS, on crée des ***politiques IAM*** et les attache à une identité IAM.
- Les rôles IAM sont identités dans AWS qui, comme les utilisateurs IAM, ont des credentials AWS associées pour signer les demandes.
# AWS Compute
## Intro
- Toutes les entreprises ont besoin de ***capacités de calcul*** pour faire fonctionner leurs *applications*.
- Suivre un modèle de calcul comme un service est beaucoup plus simple pour commencer et soutenir les opérations au fil du temps.
- Options : *VM*, *Containers*, *Serverless*.
## EC2
- Serveurs virtuels : ***Instance EC2***
- provisionner et lancer un ou plusieurs instances EC2.
- Arrêter ou étendre les instances EC2.
- Payer à l'heure.
- Premier setting : sélectionner une ***AMI*** (Amazon Machine Image)
- Instances EC2 : versions actives de ce qui est défini dans une AMI
- Façons de sélectionner une AMI :
	- quick start AMIs
	- AMI AWS Marketplace
	- Mes AMI
	- AMI communautaires
	- Image personnalisée
- Le type et la taille de l'instance déterminent les capacités de calcul, de mémoire et de réseau disponibles. (*c5n.xlarge*)
- Chaque famille d'instances est optimisée pour s'*adapter à différents cas d'utilisation*.
- Localisation : *VPC* par défaut.
- *Scalabilité* : possible d'adapter et de choisir des configs spécifiques pour les VM via des appels API.
- Lifecycle : 
- ![[Pasted image 20241125104702.png]]
## Conteneurs
- Amazon Elastic Container Service (***ECS***) et Amazon Elastic K8s (***EKS***) : interagir avec son infrastructure.
- Vm vs Conteneur : Par rapport aux VM, les conteneurs partagent le même système d'exploitation et le même noyau que l'hôte sur lequel ils sont déployés.
- ***ECS*** : service d'orchestration de conteneurs qui permet de déployer et de gérer facilement des conteneurs.
- ![[Pasted image 20241125105129.png]]
- ***EKS*** : outil adapté pour des conteneurs fonctionnant sur ***K8s***
## Serverless
- Lancer des applications sans infra : opter pour le calcul serverless AWS
- ***AWS Fargate*** : plateforme de calcul serverless pour les conteneurs, utilisable avec ***ECS*** ou ***EKS.***
- ***AWS Lambda*** : service qui permet d'exécuter du code sans avoir à gérer des serveurs ou des conteneurs.

> AWS Lambda is commonly used for serverless computing tasks. Here are the main use cases:
> 1. API and Web Applications
> 
> - Building REST APIs and web backends without managing servers
> - Handling HTTP requests through API Gateway
> - Processing form submissions
> - Authentication and authorization layers
> 
> 2. Data Processing
> 
> - Processing uploads to S3 buckets automatically
> - Image/video processing and resizing
> - Log file analysis
> - ETL (Extract, Transform, Load) operations
> - Real-time data transformations
> - Stream processing with Kinesis
> 
> 3. ***Automation and DevOps***
> 
> - Running scheduled tasks and cron jobs
> - Infrastructure maintenance tasks
> - Automated backup and recovery
> - CI/CD pipeline tasks
> - CloudWatch alarms and notifications
> 
> 4. Integration Tasks
> 
> - Connecting different AWS services
> - Webhook handling
> - Third-party API integrations
> - Email processing
> - SMS and notification handling
> 
> 5. IoT and Mobile Backend
> 
> - Processing IoT sensor data
> - Mobile app backends
> - Push notification services
> - Real-time data updates
> 
> 6. Machine Learning
> 
> - Serving ML models
> - Pre-processing data for ML workflows
> - Running inference on trained models
# AWS networking
## AWS VPC
- C'est une section personnalisable et isolée du cloud AWS où les utilisateurs peuvent lancer des ressources.
- Chaque région a un VPC par défaut
- Communication au sein d'un réseau comme l'envoie d'une lettre par la poste.
- Chaque machine dans un réseau possède un IP
## VPC personnalisé
- Un cloud privé, virtual private cloud (***VPC***) est un ***réseau isolé*** qu'on crée dans le cloud AWS, similaire à un réseautraditionnel dans un datacenter.
- Après la création d'un VPC, il faudra créer des ***sous-réseaux*** à l'intérieur du réseau
- Pour qu'AWS puisse configurer le VPC de manière appropriée, AWS réserve ***cinq adresses*** IP dans chaque sous-réseau.
- Les ***gateways*** sont des passerelles vers des réseaux externes, que ce soit internet, au autre VPC ou VPN.
- Pour établir une connexion physique sécurisée entre le datacenter sur site et le VPC Amazon, on peut utiliser ***AWS Direct Connect***.
- Une ***table de routage*** contient un ensemble de règles, appelées ***routes***, utilisées pour déterminer vers où le trafic réseau est dirigé.
- Une ***ACL réseau*** permet de contrôler le type de trafic ***autorisé*** à *entrer* ou à *sortir* du ***sous-réseau***.
- La couche de sécurité suivante concerne les instances EC2. On peut créer un ***pare-feu virtuel*** appelé ***groupe de sécurité***.
# AWS Storage
- Les services de stockage AWS
	- stockage de fichier : hiérarchie en arborecense
	- stockage de blocs : divise les fichiers en morceaux de données de taille fixe.
	- stockage d'objet : comme les fichiers, sont traités comme une unité de données unique et distincte lorsqu'ils sont stockés.
- ![[Pasted image 20241126091914.png]]
## Stockage dese fichiers
### Amazon EFS
- Elastic File System
- type set-and-forget
- Amazon FSx
## Stockage de blocs
### Amazon EC2 instance store
- ***Volumes EBS*** : agissent de la même manière que les disques externes à plusieurs égards.
- Faire évoluer les volumes EBS :
	- Mise à l'échelle d'EBS
	- Snapshots EBS
## Stockage d'objet
### S3
- Récupérer les données depuis n'importe où dans le web.
- Chaque nom de compartiment doit être unique sur tous les comptes AWS de toutes le régions AWS au sein d'une partition.
- Plusieurs cas d'utilisation : sauvegarde, hébérgement de média, livraison de software, lacs de données, site web statique.
### Sécurité
- S3 ne peut être consulté que par l'utilisateur ou le compte AWS qui a créé cette resource.
### Classe de stockage
- classe de stockage S3 : permettent de modifier le niveau de stockage en fonction des caractéristiques des données.
### Lifecycle
- Pour automatiser le changement de classe de stockage d'objets, on peut configurer leur cycle de vie Amazon S3.
# AWS Databases
## DB relationnelles
- Organisent les données en tables, où les données d'une table peuvent être liées à celles d'autres tables, créant ainsi des relations.
- RDBMS : créer, màj et administrer une DB relationnelle.
- Avantages : manière de stocker, organiser et interroger les données, offrant une multitude d'avantages.
- DB gérée/non gérée
- ![[Pasted image 20241126093943.png]]
## RDS
### Types :
- aurora
- mysql
- mariadb
- postgresql
- oracle
- sqlserver
### Instance de DB
- doit être géré.
- se repose sur le calcul et le stockage.
### Stockage
- volume ***EBS***
### Amazon RDS dans un VPC
- selection du VPC lors de la création des DB
### Backups
- Pour effectuer des sauvegardes régulières des instances RDS, il est possible d'utiliser des sauvegardes automatisées ou des instantanés manuels.
### Sécurité
- Contrôle de l'accès aux resources RDS, tels que les DB sur une instance de DB.
## Sur mesure
- 15 moteurs spécialement conçus pour prendre en charge divers modèles de données.
## DynamoDB
- service de DB NoSQL entièrement géré.
- composants : tables, éléments et attributs.
- simple, sécurisé
# AWS Monitoring, Load Balancing & Scaling
## Introduction
- Objectif : On a besoin d'un moyen de collecter et d'analyser des données sur l'état opérationnel et l'utilisation des resources (***metrics***).
## Amazon CloudWatch
- ***CloudWatch*** est un service de ***surveillance*** et d'observabilité qui ***collecte nos données de ressources*** et fournit des *infos exploitables par nos application*.
- CloudWatch agit comme un lieu centralisé où les ***metrics*** sont *collectées* et *analysées*.
- Comme les DB qu'on crée et qu'on gère nous même, RDS repose sur le ***calcule de stockage***.
- Aves les métriques personnalisées, on peut publier nos propres métriques sur CloudWatch.
- Les ***tableau de bord*** sont des pages d'accueil personnalisables qu'on peut configurer pour la ***visualisation des données*** pour une plusieurs métriques via des ***widgets***, tels qu'un graphique ou du texte.
- ***CloudWatch Logs*** : ***surveiller***, ***stocker*** et ***accéder*** aux `fichiers journaux` à partir d'applications exécutées sur les ***instances EC2***, des fonctions AWS Lambda et d'autres resources.
- ***Alarm CloudWatch*** : lancer automatiquement des actions basées sur des changements d'état soutenus de nos metrics.
## Optimisation
- La disponibilité d'un système est généralement exprimée en pourcentage de dispo au cours d'une année donnée ou en nombre de neuf.
## Routage avec ELB
- Une requête typique pour une application ***démarre à partir du navigateur d'un client***. La requête est ***envoyée*** à un équilibreur de charge (***load balancer***). Ensuite il est ***envoyé à l'une des instances EC2*** qui héberge l'application.
- Le service ELB est composé de trois éléments principaux : 
	- les règles
	- les listeners
	- les groupes cibles
- Types de Load Balancers : 
	- Application Load Balancer
	- Network Load Balancer
	- Gateway Load Balancer
-
## Scaling automatique
- On peut ajouter ou supprimer automatiquement des instances EC2 à l'aide des ***stratégies de mise à l'échelle*** que l'on définit.
- On peut ***améliorer*** la disponibilité et l'accessibilité en ***ajoutant un serveur supplémentaire***. Cependant, l'ensemble du système peut à nouveau devenir indisponible en cas de problème de capacité
- Le service ***EC2 Auto Scaling*** ajout et supprime de la capacité pour maintenir des performances stables et prévisibles au coût le plus bas possible.
- Le service ELB s'intègre parfaitement à EC2 Auto Scaling. Dès qu'une nouvelle instance EC2 est ajoutée ou supprimée du groupe Amazon EC2 Auto Scaling, ELB en est informé.
- Un groupe Auto Scaling aide à définir où EC2 Auto Scaling déploie nos resources.
- Par défaut, un groupe Auto Scaling sera conservé à sa capacité initiale souhaitée. Bien qu'il soit possible de modifier manuellement la capacité souhaitée, vous pouvez également utiliser des politiques de mise à l'échelle.
# Nom de domaine
## Introduction
Un nom de domaine est une ***adresse*** lisible et mémorisable par les humains qui permet d'accéder à un site ou à un service en ligne.
## Contexte
- Une ***adresse IP*** reste compliquée à retenir.
- Les noms de domaine permettent de créer un alias.
## Foncitonnement
### DNS
- Un ***serveur DNS*** est une sorte d'annuaire qui traduit les noms de domaine en adresse IP.
- Lorsqu'un utilisateur saisit un nom de domaine dans un navigateur web, le navigateur envoie une ***requête DNS*** à un serveur de noms de domaine.
- `navigateur` --> `requête DNS` --> `réponse` --> `site affiché`
- Le DNS est une base donnée distribuée et hiérarchique composée de trois niveaux.
- www.google.com :
	- `com` : top-level-domaine (TLD). Représente l'extension du nom de domaine (com, fr, de , org, edu, net)
	- `google` : domaine
	- `www` : sous-domaine. moyen d'organiser et de structurer un sitweb.
- ***registrar*** : entreprise qui enregistre des noms de domaines pour les rendre disponibles pour l'utilisation sur internet. Les registrar permettent l'enregistrement et la gestion des nom de domaine sur internet.
- La durée normale minimale pour un nom de domaine est de ***1 an***.
### Zone DNS
- Une ***zone DNS*** permet de configurer comment le noms de domaines sont associés à une adresse IP. C'est une partie de l'espace de nom de domaine qui est gérée par un serveur DNS.
- ![[Pasted image 20241127093157.png]]
- Dans une zone DNS, on configure différents types d'enregistrements :
	- A (Address) : www.monsite.com --> 192.168.1.1
	- CNAME (Canonical Name) --> blog.monsitge.com --> www.monsite.com
	- MX (Mail Exchange) : où envoyer les e-mails pour monsite.com

### Domaine Information Groper
- La commande `dig` : pour interroger les serveurs DNS et obtenir des informations sur les noms de domaine.
### SSL Certificate
- Un ***certificat SSL*** agit comme une ***carte d'identité numérique***, garantissant la ***sécurité*** d'un site web et la ***protection des données*** des utilisateurs.
- *Let's Encrypt* donne accès à la sécurisation des communication via HTTPS. C'est une ***autorité*** qui *offre des certificats SSL* simples et automatisés. 
## Quiz
- Qu'est ce qu'un nom de domaine ? :
	- un nom générique pour un site web
- Comment les adresses IP sont-elles attribuées ? :
	- Par registre régionaux d'adresse IP
- Quel est le rôle d'un serveur DNS autoritaire ? :
	- Répondre aux requêtes DNS pour les domaines qu'il gère.

default aquaray
`aquaray-ownership-verification=011b7db2d3203725dc69bc6eb9dc1178`

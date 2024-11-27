# Virtualisation
- La ***virtualisation*** permet de créer des environnement
- Fait parti de la phase ***operate*** du cycle DevOps.
- contexte :
	- l'*exécution de plusieurs serveurs physiques* pour les taches légères *gaspille des resources* matériels et énergétiques.
	- Les configurations matérielles fixes posent un autre défi, rendant *difficile l'adaptation* aux besoins changeants des applications.
	- L'allocation manuelle et la gestion des ressources deviennent alors *fastidieuses* et *inefficaces*, entraînant souvent une *sous-utilisation des ressources disponibles*. La virtualisation répond à cette problématique en permettant une ***répartition dynamique des ressources*** selon les besoins, optimisant ainsi l'efficacité globale du système.
	- Garantir que l'application fonctionne de manière cohérente et fiable quel que soit l'environnement sur lequel elle est exécutée.
	- L'exécution simultanée de multiples applications sur un même serveur peut engendrer des conflits et des problèmes de sécurité. La virtualisation résout ce problème en isolant les applications dans des machines virtuelles distinctes, minimisant ainsi les interférences potentielles et renforçant la sécurité globale du système.
	- l'achat et la maintenance de serveurs représentent des dépenses significatives pour les entreprises.
- Fonctionnement :
	- chaque type de virtualisation présente des avantages et des inconvénients, ce qui les rend adaptés à différentes situations et besoins.
	- chaque virtual env fonctionne comme s'il s'agissait d'un ordinateur physique indépendant, avec son propre système d'exploitation et 
	- les conteneurs sont une technologie de virtualisation légère et portable qui permet d'isoler les applications.
# Docker
- ***Docker*** facilite la création d'environnements de développement cohérents et reproductibles, ce qui contribue à la fiabilité du CD et à la gestion de l'infrastructure
- Fait parti de la phase ***build*** du cycle DevOps.
- contexte : 
	- Une application a besoin de pouvoir être lancée de manière stable et constante sur tous ses environnements.
	- un conteneur ne contient pas uniquement l'application, c'est une environnement clos qui embarque plusieurs éléments de configuration/fonctionnement.
	- Les conteneurs fournissent un environnement d'execution identique sur tous les systèmes d'exploitation.
	- Une application a besoin d'être hébergée sur un serveur pour délivrer un service 24h/24.
	- Les applications vont devoir cohabiter sur le meme serveur et donc partage...
	- Pour gagner en stabilité et en souplesse, on cloisonne les applications grâce aux conteneurs.
- Fonctionnement :
	- chaque ***conteneur*** va pouvoir être configuré individuellement au travers d'une ***image*** docker. une image est un ***os minimal*** sur lequel des ***outils*** (python, nginx, node.js...) sont ***pré-installés***.
	- Un conteneur est une ***machine autonome*** dans laquelle on peut exécuter des commandes et qui peut être démarrée, supprimée et dupliquée très rapidement.
	- Les modifications à apporter à un conteneur devront être faites dans le fichier ***Dockerfile*** pour créer une nouvelle image.
	- L'image permet à un conteneur qui est recréé de retrouver toutes ses modifications.
	- l'activité de chaque conteneur peut être monitorée en temps réel. (lots, ui...)
	- ***cycle de vie*** d'un conteneur Docker : *création*, *démarrage*, *execution*, *arrêt*, *suppression*
# Docker compose
- Outil qui permet de définir et de gérer des environnements ***multi-conteneurs***.
- S'inscrit dans la phase Build du cycle devops.
- contexte :
	- plusieurs conteneurs fonctionnent en autonomie.
	- l'utilisation multiple de commandes docker est nécessaire pour administrer les conteneurs --> plus il y a des conteneurs, plus il y'a des risques d'erreurs.
	- compose permet d'***administrer un groupe de conteneurs***, rendant la gestion plus rapide
	- les commandes se font sur un ***groupe*** de conteneurs et non sur un seul conteneur.
	- il possible pour un conteneur de ***communiquer vers l'extérieur***.
	- les conteneurs peuvent ***communiquer entre eux***
- fonctionnement :
	- chaque conteneur est représenté par un service. l'objectif est de regrouper ces services pour former une application complète.
	- service = image
	- fichier ``docker-compose.yml`` associe chaque image avec un service.
	- il est possible de configurer individuellement chaque service dans le ficher `docker-compose.yml`. Cette config écrase ou complete la config par défaut de l'image.
	- les commandes docker sont remplacées par celles de compose. elle permettent maintenant d'agir sur le groupe de service.
	- commande : ```docker compose```
# Docker avancé
- compose permet de ***gérer des environnements complexe*** et de configurer des réseaux personnalisés pour isoler les conteneurs ou gérer les volumes de données pour les rendre persistants.
- ***Build***
- fonctionnement :
	- dans le cadre d'application complexes, on peut souhaiter un séparation des différents éléments sur le réseau.
	- ![[Pasted image 20241112094424.png]]
	- ![[Pasted image 20241112094518.png]]
	- parfois, il est nécessaire de faire persister les données et de les partager entre plusieurs services.
	- ![[Pasted image 20241112094646.png]]
	- les ***volumes docker*** servent à stocker des données de manière persistante en dehors des conteneurs, ce qui permet de partager des données les conteneurs et de les sauvegarder.
	- en fonction de l'environnement de déploiement des conteneurs, il est peut être nécessaire d'avoir des configurations différentes.
	- Les ***variables d'environnement*** sont utilisées pour injecter des configs et des params spécifiques dans les conteneurs lors de leur execution.
	- ![[Pasted image 20241112095020.png]]
	- pour deployer l'application:
		- ```docker compose --env-file d.env up -d```
	- Parfois, on veut deployer certains services sur un environnement et pas sur un autre (e.g. environnement prod et dev)
	- Les ***profils*** sont utilisés pour regrouper des services en fonction de leurs rôles ou de leurs fonctionnalités au sein d'une application.
	- ![[Pasted image 20241112095534.png]]
	- Parfois, on veut déployer certains services sur un environnement et pas sur un autre.
	- contrôle de démarrage :
		- les ***healthcheck*** dans docker compose sont utilisés pour surveiller l'état de santé d'un service et pour déterminer s'il est prêt à recevoir des connexions.
		- ![[Pasted image 20241112100718.png]]
		- ![[Pasted image 20241112100738.png]]
# kubernetes
- se situe dans la phase ***deploy*** dans le cycle devops
- but : assurer la haute disponibilité des services sur plusieurs serveurs.
- contexte :
	- la gestion de différents serveurs est fastidieuse, car il faut intervenir manuellement sur chacun d'eux.
	- k8 permet d'orchestrer tous les conteneurs répartis sur l'ensemble des serveurs de prod. (répartition des charges)
	- k8 est utilisé pour le déploiement d'applications conteneurisées à grande échelle dans les environnements de production.
## pods
un pod est ensemble de containers. equivalent du docker-compose.
![[Pasted image 20241113091706.png]]
- objectif : ***dupliquer les pods*** sur plusieurs serveurs pour garantir leur disponibilité et pour optimiser le trafic.
- Les pods sont administrés à travers des commandes qui sont reçues par le ***master node***.
- Le ***master node*** est un serveur à part dont le seul but est d'orchestrer les pods.
- Un serveur peut contenir plusieurs pods, on parle alors de ***worker node****.
- Pour assurer le principe de haute disponibilité, les pods ne doivent pas être dupliqués sur le même serveur.
- ![[Pasted image 20241113092217.png]]
- c'est le rôle du ***master node*** de répartir équitablement les pods entre les différents worker nodes.
	- ex: si un pod crash, il sera re-créé automatiquement sur un worker node disponible.
## cluster k8
- un cluster désigne le master node + l'ensemble des worker nodes
- ![[Pasted image 20241113092521.png]]
- k8 gère la disponibilité des applications dans un cluster en répartissant automatiquement les charges de travail sur des noeuds sains et redémarre les conteneurs en cas d'échec.
## minikube
- outil pour créer un cluster k8 local sur une seule machine,.
## kubectl
- outil pour configurer un cluster.
## quiz
Quel est l'un des principaux avantages de Kubernetes pour la haute disponibilité ?
a) *La possibilité de déployer des applications sur plusieurs nœuds*


Comment Kubernetes assure-t-il la haute disponibilité ?
b) *En déployant plusieurs instances de chaque conteneur sur différents nœuds*

Comment Kubernetes assure-t-il la résilience en cas de défaillance d'un nœud ?
a)  *En utilisant un système de basculement automatique vers un nœud de secours*

Comment Kubernetes assure-t-il la disponibilité des données ?
b) *En utilisant des outils de sauvegarde et de restauration des données*
## Labels
- Les labels sont des données de type clé/valeur qui sont attachés aux objets permettant de les identifier plus facilement.
- Si vous regardez d’un peu plus près le contenu d’un des fichiers de déploiement que vous avez créé, vous remarquerez que la partie "metadata" contient un tableau "labels" possédant une étiquette "app".
## Namespaces
- Kubernetes est capable de prendre en charge plusieurs clusters virtuels présents sur le même cluster physique, ces clusters virtuels sont appelés des namespaces.
- Les namespaces vont plus loin que la notion de labels, car ils permettent de gérer plusieurs applications ou environnements sur le même cluster, auprès du même master node et en les isolant afin d’assurer un maximum de sécurité, bien évidemment.
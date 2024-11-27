# hosting & cloud
- c'est la façon de ***mettre à disposition*** des applications ***aux utilisateurs***.
- le hosting et le cloud computing offrent des solutions flexibles pour répondre aux besoins de stockage, de calcul et de mise en réseau des entreprises et des utilisateurs.
- s'inscrit dans la phase ***operate*** du cycle DevOps
- contexte:
	- besoin de ***flexibilité*** : pour des raisons de coûts, mais également de scalabilité, une entreprise ne peut pas toujours héberger sa propre infrastructure.
	- puissance à la demande : les clouds providers permettent aux entreprises de dématérialiser leurs infrastructures pour l'adapter au besoin du moment.
- fonctionnement : 
	- ***cloud providers*** (google cloud, microsoft azure, aws...) fournissent les mêmes services et leurs puissances dépendent de leurs data centers répartis dans le monde.
	- service à la carte (services) : serveur de prod, service de stockage, bdd, cdn
	- trafication : utilisation à l'heure. stockage au volume et serveur au temps.
	- la gestion des services se fait au travers l'***interface*** web du cloud provider
	- modèles de déploiement
	- ![[Pasted image 20241118091931.png]]
	- le cloud "***public***" est géré par des fournisseurs externes, offrant accessibilité et élasticité.
	- le cloud "***privé***" offre un contrôle et une sécurité accrus pour les données sensibles.
	- le cloud "***hybride***" combine les avantages des modèles public et privé.
	- le ***multicloud*** utilise divers fournisseurs pour optimiser les performances et réduire les risques.
# cloud computing
- les resources de cloud computing sont hébergés sur des infrastructures distantes, permettant aux utilisateurs d'éviter d'avoir à gérer et à entretenir physiquement le matériel informatique.
- s'inscrit dans la phase operate du cycle DevOps
- contexte :
	- définition : permet aux utilisateurs de déployer et de gérer des apps, des sites web et des services de manière flexible et évolutive
	- les consoles de cloud computing permet de créer et gérer des serveurs virtuels dans le cloud.
	- le cc est un ensemble de services extrêmement versatile et permet de faire, dans le cloud, tout ce qu'un ordinateur classique offre. en possibilités.
	- on peut facilement augmenter ou réduire le nombre d'instance cloud et leurs capacités en fonction des besoins.
	- la flexibilité de l'architecture cloud permet de créer des instances toujours plus proches des besoins liés à leur utilisation.
# aws ec2
- ***EC2*** un service de calcul évolutif d'aws qui permet de lancer et gérer des serveurs virtuels dans le cloud.
- s'inscrit dans la phase ***operate*** du cycle devops.
- fonctionnement :
	- les `AMI`s sont des images pré-configurées avec un os, des apps et des paramètres spécifiques.
	- ***ec2*** propose divers types d'instances pré-configurés qui s'adapterons à tous les besoins.
	- une bonne config réseau permet aux instances ec2 de communiquer avec d'autres resources dans le cloud et sur internet.
	- les groupes de sécurité sont des pare-feu virtuels qui contrôlent le trafic entrant et sortant des instances ec2. (équivalent *iptables* firewall)
	- chaque instance ec2 est associée à un ou plusieurs groups de sécurité.
# google gce
- c'est un service d'infrastructure de calcul qui permet aux utilisateurs de déployer et de gérer des machines virtuelles sur l'infrastructure mondiale google.
- s'inscrit dans la phase ***operate*** du cycle devops.
- fonctionnement :
	- gce propose des instances à usage général, mais aussi à usage spécifique comme le calcul CPU ou GPU et des instances optimisées pour le stockage.
	- gce propose des images disques basiques à montage rapide, mais aussi la possibilité de lancer des conteneurs directement.
	- la config de base du réseau gce est basique mais peut être personnalisée après la config initiale.
# azure vm
- Azure Virtual Machines offre la possibilité de créer et de gérer des machines virtuelles dans le cloud afin d'exécuter diverses charges de travail, des applications simples aux environnements complexes.
- s'inscrit dans la phase ***operate*** du cycle devops.
- fonctionnement : 
	- Les images Azure, comme les AMI AWS, sont des images pré-configurées avec un système d'exploitation, des applications et des paramètres spécifiques.
	- Azure VM propose plusieurs tailles d’instances dédiées à de multiples usages qui pourront s’adapter à tous les besoins.
	- Azure permet de créer des réseaux virtuels complexes pour relier des machines virtuelles entre elles et à d’autres services Azure
	- Les groupes de sécurité ont le même rôle que chez AWS. Chaque instance peut être associée à un ou plusieurs groupes de sécurité.
# cloud database
- Les bases de données dans le cloud permettent aux organisations de bénéficier de la scalabilité, de la performance et de la disponibilité sans les contraintes des infrastructures physiques.
- s'inscrit dans la phase ***operate*** du cycle devops
- contexte :
	- bdd on-premise : système *on-premise* imposent des limites en terme de coûts et de scalabilité.
	- Les bdd gérées offrent une maintenance réduite et une meilleure scalabilité.
	- la sélection entre sql et msql dépend principalement du type de données gérées et des exigences spécifiques de l'app.
	- les bdd sql offrent une structure rigide idéale pour les transactions complexes et garantissent l'intégrité des données à travers des relations fixes.
	- ![[Pasted image 20241119091316.png]]
	- en contraste, nosql, plus flexible, sont optimales pour gérer de grandes quantités de données non structurées avec des modèles de données variés et une scalabilité horizontale.
	- les bases de données gérées offrent une flexibilité et une scalabilité supérieures.
- fonctionnement :
	- architecture sophistiquées pour optimiser la gestion des données.
	- améliorent la scalabilité et la performance grâce à des technologies modernes.
	- l'utilisation du cloud permet de garantir la sécurité des données et respecte les normes de conformité dans les bases de données gérées.
	- l'utilisation de partitions de données pour un répartition efficace des charges est le mécanisme que les bdd gérées dans le cloud utilisent.
# RNPC
- dossier pro parcours de formation
- dossier projet
- soutenance
- compétences évalués
## dossier pro
- rempli selon le model fourni. www.dossierprofessionel.fr
## dossier projet
- projet imposé à réaliser en équipe
- fil conducteur
- dès la fin de formation
- plan :
	- liste des compétences et expliquer comment ils sont utilisés
	- cahier des charges
	- spécification technique
	- description de la démarche et des outils
	- réalisation individuelles
	- description d'une situation de travail qui a nécessité une recherche durant le travail.
- soutenance (30 min)
	- support de présentation
	- contexte
	- présentation de l'appli
	- présentation d'un exemple du travail réalisé individuellement.
	- présentation d'un exemple de recherche
	- synthèse et conclusion
## soutenance
 - 30 min d'etude d'une doc technique en anglais.
 - 15 min de lecture du dossier par le jury (à imprimer)
 - 30 min de présentation du projet
 - 30 min d'entretien technique
 - 20 min d'échange sur le projet professionnel
## conseils
- être honnête sur les difficultés
- préparer chaque sujet évalué
- réviser tous les sujets (même les sujets basiques)
- venir avec son ordi avec tous les configs.
# cloud storage
- Le Cloud Storage permet de stocker des données sur des serveurs distants accessibles via internet, offrant flexibilité, évolutivité et économies de coût significatives.
- le stockage local fait référence à la conservation des données à proximité de l'utilisateur.
- s'inscrit dans la phase operate du cycle devops
- contexte : 
	- le stockage local peut présenter des limites en capacité et en gestion.
	- cout en énergie, matériel, compétences.
	- ![[Pasted image 20241120091407.png]]
- fonctionnement :
	- le stockage d'objet regroupe les documents en les liant à des métadonnées. il est optimisé pour les bases de données trasactionnelles.
	- le stockage de fichiers facilite le partage et la gestion collaborative des données.
	- les disques virtuels fournissent un stockage de bloc persistant pour les applications exigeantes.
	- ***architecture*** cloud storage : conçue pour maximiser la dispo et la robustesse.
	- ***redondance*** : assure la protection et la disponibilité continue des données.
	- ***réplication*** : augmente la sécurité et l'accessibilité des données à travers le globe.
	- avantage de la réplication : permet une récupération rapide des données en cas de panne.
	- ***performances*** : dépend de la latence et du débit.
	- ***sécurité*** : des mesures rigoureuses protègent les données dans le cloud storage.
# objet cloud storage
- principales solutions de stockage d'objet : aws s3, gcloud cloud storage, azure blob storage.
- s'inscrit dans la phase operate du cycle devops
- contexte :
	- le stockage d'objets s'adapte dynamiquement aux besoins de stockage de ses utilisateurs.
	- Avec une durabilité extrême et une protection robuste des données, les services de stockage d’objets sont conçus pour répondre aux exigences les plus strictes en matière de sécurité et de disponibilité des données
	- ![[Pasted image 20241120094149.png]]
- fonctionnement :
	- les services de stockage optimisent automatiquement la durabilité, la disponibilité et l'évolutivité
	- les objets sont regroupés dans des ***buckets*** équivalents à des conteneurs de stockage logiques.
	- l'utilisation de balises, règles de cycles de vie et la gestion des versions permettent un contrôle précis des données stockées.
	- la mise en place de politiques de cycle de vie dans les ***buckets*** permet d'automatiser la gestion des données.
	-  consistance des données
	- les services de stockage d'objet proposent des garanties de consistance qui permet aux applications de compter sur des données précises et à jour.
	- sécurité + conformité
# content delivery network (cdn)
- série de serveurs distribués qui permettent de fournir rapidement des contenus aux utilisateurs, en fonction de leur localisation géo.
- s'inscrit dans la phase operate du cycle devops
- contexte :
	- dans une archi centralisées, les utilisateurs peuvent subir une latence élevée, dégradant l'expérience utilisateur.
	- une infra centralisée peut limiter la scalabilité et augmenter les coûts opérationnels.
	- gestion de la bande passante : la gestion de la bande passante est plus complexe dans une infra centralisée.
	- sécurité : l'absence du cdn expose à des risques de securités accrus, comme les attaques ddos
- fonctionnement :
	- les cdn utilisent le routage intelligent pour gérer efficacement le trafic et la charge.
	- les cdn maintiennent de multiples copies des données à travers le monde pour une livraison rapide.
	- les cdn utilisent le caching pour réduire le temps de réponse et la bande passante.
	- les cdn réduisent la taille des fichiers pour accélérer la livraison du contenu.
	- les cdn supportent le streaming dynamique pour une expérience utilisateur optimale.
	- cdn protègent et assurent la continuité du service contre les attaques ddos.
# PaaS & Serverles
- Les solutions de déploiement telles que CI/CD dans le cloud, ***PaaS***, et ***Serverless***, permettent aux développeurs de minimiser les tâches répétitives et de réduire les erreurs manuelles. Facilité d'implémentation.
- s'inscrit dans la phase ***deploy*** du cycle devops.
- contexte :
	- les systèmes on-premise sont coûteux et rigides, limitant la rapidité d'innovation.
	- Le ***Serverless*** et le ***PaaS*** élimine la gestion de l'infrastructure et accélèrent le déploiement.
	- en fonction des différents facteurs, les apps déployés sur internet peuvent voir leur charge varier.
	- dès qu'une application est déployée sur internet, elle peut être la cible d'attaques malveillants, mais son système de déploiement aussi.
	- Les pipelines CI/CD rationalisent et automatisent les processus de développement et de déploiement.
	- ![[Pasted image 20241121091619.png]]
	- Le ***Serverless*** élimine la nécessité de gérer des serveurs, optimisant les opérations et les coûts.
	- ![[Pasted image 20241121091830.png]]
	- Les plateformes ***PaaS*** fournissent les outils nécessaires pour développer, tester, et déployer des apps efficacement.
	- ![[Pasted image 20241121091957.png]]
	- *dans le cadre d'un processus DevOps, un pipeline est toujours la meilleure option*
	- fonctionnement
		- services ***serverless*** : exécutent du code en réponse à des ***events*** sans gestion de serveur.
		- services ***PaaS*** : fournissent des *environnements de dev* et d'*hébergement gérés*.
		- PaaS vs Serverless : *rôles similaires* mais leur *fonctionnement est différente*.
		- L'utilisation d'un service de CI/CD dans le cloud facilite des déploiement rapides et cohérents dans les environnements Serverless et PaaS
		- Comme les solutions cloud, ***AppRunner*** a la capacité de s'*adapter automatiquement* à la demande.
		- ***Sécurité*** : Serverless et PaaS intègrent des *pratiques de sécurité avancées* pour protéger les apps.
		- GitLab CI offre des fonctionnalités de CI/CD plus avancées par rapport à AWS CodePipeline.
# Linode
- ***Linode*** est une plateforme cloud qui offre une gamme complète de services, allant de la ***provision de machines virtuelles*** (VM) à l'***orchestration de conteneurs***, en passant par la ***provision de bases de données*** et le ***stockage d'objets***.
- S'inscrit dans la phase ***Operate*** dans le cycle DevOps.
- Linode fournit une plateforme d'infrastructure cloud fiable et évolutive pour héberger, déployer et gérer des applications web et des services.
## Provision de VM
- Linode permet aux utilisateurs de ***provisionner des machines virtuelles*** (VM) de manière rapide et simple. Les ***VM Linode*** sont dotées d'***adresses IP*** *statiques permanentes*, garantissant une stabilité et une accessibilité constante pour les applications déployées.
## Orchestration des conteneurs
- En plus de la provision de VM, Linode offre des fonctionnalités avancées pour l'***orchestration de conteneurs***. Les utilisateurs peuvent ***déployer***, gérer et ***mettre à l'échelle*** des *applications conteneurisées* de manière efficace, offrant une flexibilité supplémentaire pour les architectures basées sur des conteneurs.
## Provision de Bases de Données
- Linode propose des solutions pour la ***provision de bases de données***, permettant aux utilisateurs de ***déployer*** et de ***gérer des bases de données*** de manière simplifiée. Cette fonctionnalité est essentielle pour les applications nécessitant un stockage structuré des données.
## Stockage d'objets
- Linode facilite également le ***stockage d'objets***, fournissant des services de ***stockage en nuage*** pour les *données non structurées*. Cela permet aux utilisateurs de *stocker* et de *récupérer* des objets, tels que des images, des vidéos ou des fichiers, de manière fiable et évolutive.
## Fonctionnement
- Linode propose ***divers systèmes d'exploitation*** et des ***configurations personnalisables*** pour répondre aux besoins des applications déployées.
## Adresses IP Statiques Permanent
- Les VM Linode sont attribuées avec des ***adresses IP statiques permanentes***, garantissant une accessibilité constante. Cela est crucial pour les applications et les services en ligne nécessitant une connectivité stable et prévisible.
## Solutions Flexibles
- Linode se distingue par son approche flexible, permettant aux utilisateurs de choisir parmi une variété de configurations de ressources en fonction de leurs besoins spécifiques. Que ce soit pour des petites applications personnelles ou des environnements d'entreprise complexes, Linode offre des solutions adaptées à différentes échelles.
# Hackathon
## frontend
Task suggestion
### **Step 1: Create an S3 Bucket**
1. Go to the **S3 Console**.
2. Click **Create Bucket**.
3. Name your bucket (e.g., `my-hackathon-app`) and choose a region.
4. Enable **Block all public access** during creation.
5. Upload your static files (HTML, CSS, JS, etc.) into the bucket.
---
### **Step 2: Configure S3 for Static Website Hosting**

1. Navigate to your bucket.
2. Go to the **Properties** tab.
3. Enable **Static website hosting**:
    - Select "Enable."
    - Enter your **index document** (e.g., `index.html`) and optional **error document** (e.g., `404.html`).

---

### **Step 3: Configure Bucket Permissions**

1. Go to the **Permissions** tab.
2. Add a **Bucket Policy** to allow CloudFront to access files:

```json
{
	"Version": "2012-10-17",
	 "Statement":
	 [
		 {
			 "Effect": "Allow",
			 "Principal": "*",
			 "Action": "s3:GetObject",
			 "Resource": "arn:aws:s3:::hackatweet-frontend/*"
		}
	]
}
```

---
### **Step 4: Set Up CloudFront**

1. Go to the ***CloudFront* Console**.
2. Click **Create Distribution**.
3. Choose **Web** and configure:
    - **Origin Domain Name**: Select your S3 bucket.
    - **Viewer Protocol Policy**: Redirect HTTP to HTTPS.
4. Save and deploy your distribution.
    - It may take a few minutes to propagate.
---
### **Step 5: Use a Custom Domain (Optional)**
1. In **Route 53**, configure a domain to point to your CloudFront distribution:
    - Add an **Alias Record** to your CloudFront URL.
2. Enable HTTPS via AWS Certificate Manager (ACM):
    - Request a certificate for your domain.
    - Associate it with your CloudFront distribution.
---
### **Step 6: Test and Deploy**

- Access your site using the CloudFront distribution URL (or your custom domain).
- Verify assets load quickly and correctly.
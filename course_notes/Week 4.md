## Table des matières

## Déploiement continue
 - But : ***automatiser*** et ***accélérer*** le ***processus de mise en prod*** des applications + qualité.
 - S'inscrit dans la phase ***deploy*** dans le cycle devops
 - contexte :
	 - chaque évolution ou correction fait l'objet d'une mise en prod
	 - la config de l'environnement de prod et souvent tres different de l'environnement de développement. L'application risque de ne pas avoir le meme comportement.
	 - La creation d'un environnement de test permet d'avoir un environnement qui correspond à celui de la production.]
	 - Mise en place d'une *pipeline* nécessaire.
- Fonctionnement :
	- Le déploiement continue représente les automatisations mises en place impliquant le serveur de production.
	- Fonctionne avec le fichier config ``.gitlab-ci.yml`` 
	- Exemple d'automatisations : Déploiement sur un serveur de prod ; execution des tests de montée en charge.
	![[Pasted image 20241104093414.png]]
	 - Les services d'hebergement peuvent proposer leur propre service de déploiement auto, sans passer par gitlab ci/cd.
## Config de deploiement d'un site statice Jekyll
```yml
# The Docker image that will be used to build your app
image: ruby:3.2
# Functions that should be executed before the build script is run
before_script:
  - gem install bundler
  - bundle install
pages:
  script:
    - bundle exec jekyll build -d public
  artifacts:
    paths:
      # The folder that contains the files to be exposed at the Page URL
      - public
  rules:
    # This ensures that only pushes to the default branch will trigger
    # a pages deploy
    - if: $CI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
```
 - l'URL généré est stocker dans "`Deploy` > `Pages`"
# Load testing
 - But : s'assurer que l'application peut gérer efficacement une grande quantité d'utilisateurs simultanés.
 - S'inscrit dans la phase deploy dans le cycle devops
 - Contexte :
	 - une appli prévu pour 100 utilisateurs ne peut fonctionner avec 1000
	 - il faut simuler des utilisateurs pour déterminer les limites de l'application et du serveur de production
	 - -> il faut optimiser le code de l'appli ou la puissance des serveurs
## Rappel Django
```sh
poetry new my_django_project
cd my_django_project
poetry add django
poetry run django-admin startproject src .
poetry run python manage.py migrate # to create database.
poetry run python manage.py createsuperuser # to create a superuser.
poetry run python manage.py runserver # to run the server
```
ou alors avec venv
```sh
python3 -m venv .venv
pip install django
django-admin startproject my_project
```
## Rappel venv python
```sh
python3 -m venv .venv
source env/bin/activate
```
## locust
- Permet de fournir un écosystème facilitant la gestion et l'execution des tests de montée en charge.
- Resultat de locust : 
	 - Nombre de requêtes réussies / échouées
	 - Temps de réponse du serveur
```sh
pip install locust
locust --headless --users 10 --spawn-rate 1 -H http://IP:PORT -t 15s
```
## .gitlab-ci.yml
```yml
image: nikolaik/python-nodejs:latest
stages:
	- load

load_testing:
	stage: load
	script: locust --headless --users 10 --spawn-rate 1 -H http://localhost:3000 -t 5s
```
# SonarQube, qualité et sécurité du code
Un code propre et sécurisé est important pour garantir la fiabilité, la performance et la durabilité d'une application.
S'inscrit dans la partie build du cycle devops.
- contexte : certains bugs ne provoquent pas le crash direct de l'appli, mais peuvent nuire à sa stabilité.
- La mauvaise conception de certaines parties du code peuvent compliquer l'évolution de fonctionnalités.
- Un code vulnérable permettrait à une personne malveillante d'accéder à des infos.
- Il faut des outils capables.
## Sonarqube
- Analyse le code d'un projet local ou distant grace à son dépôt Git.
- s'integre dans une pipeline de ci.
### Arborescence du projet
```sh
workdir
├── project_dir
├── sonar_scanner
└── sonarqube
```
## SonarQube Cloud
### Configuration des projets sur sonar
- s'inscrire avec gitlab
- fournir le token personnel
- ajouter les variable  ci/cd de sonar
.gitlab-ci.yml
```yml
stages:
- code_scanning

variables:
SONAR_USER_HOME: "${CI_PROJECT_DIR}/.sonar" # Defines the location of the analysis task cache
GIT_DEPTH: "0" # Tells git to fetch all the branches of the project, required by the analysis task

sonarcloud-check:
	stage: code_scanning
	image:
	name: sonarsource/sonar-scanner-cli:latest
	entrypoint: [""]
	cache:
	key: "${CI_JOB_NAME}"
	paths:
		- .sonar/cache
	script:
		- sonar-scanner
	only:
		- merge_requests
		- develop
		- main
		- prod
```

# Azure
- S'inscrit dans la phase **manage** du cycle devops
- Plateforme complète de gestion du cycle de vie des applications.
- Utilisé par des grandes entreprises.
- solution de simplicité (comme windows).
- ChatOps : Permet une integration avec des outils de chat (Teams, Slack).
- Fonctionnement : une vue centralisée pour suivre et gérer les activités d'un projet.
- Boards : conçus pour aider les équipes à gérer et à suivre les travaux en utilisant des tableaux Kanban.
- Work Items : Avoir une vue complète des tâches à réaliser dans un projet.
- Sprint : tableau Kanban qui permet de visualiser l'avancement des travaux.
- Cards : permet de visualiser le travail restant et de gérer les capacités de l'équipe pendant la durée du sprint.
- Repos : similaire à Gitlab, Github
- Pipelines : Comme Gitlab, Azure automatise le processus de build et de déploiement.
- Deux types de pipeline : YML et pipelines classiques.
- Test Plans : Les équipes peuvent créer différents types de tests, tels que les tests manuels, les tests exploratoires, les tests automatisés etc. et définir les étapes détaillées pour chaque scénario.
- Artifacts : utilisé pour la gestion des packages, des artefacts et des dependences liés au sw development. Permet de créer, tester et publier de packages de code.
- Les agents : equivalent des runners Gitlab
- Etapes : 
	- Créer une organisation sur Azure
	- installer un agent
## Practical
INSTALLATION DE L’AGENT AZURE DEVOPS

👉 Téléchargez l’agent Azure DevOps sur votre VM. Désarchivez le fichier .tar.gz et lancez la configuration de l’agent.

👉 Installez l’agent en tant que service utilisant votre utilisateur engineer et lancez-le.

DÉMARRER UN PIPELINE YML

👉 Créez un fichier azure-pipelines.yml à la racine de votre projet.

👉 Configurez votre pipeline en utilisant votre agent local afin d’effectuer les actions suivantes  :

- Copier les fichiers du projet vers le répertoire ~/myFlaskApp
- Lancer le projet sur votre VM
```sh
pip install -r requirements.txt
flask --app webapp run
```

DÉMARRER UN PIPELINE “CLASSIQUE”

👉 Créez un nouveau projet “My Classic Flask App”.

👉 Activez les pipelines classiques au niveau de votre organisation.

👉 Créez un pipeline en utilisant l’éditeur graphique de pipeline afin qu’il utilise votre agent local et qu’il effectue les mêmes actions que le pipeline précédent.
### azure-pipelines.yml
```yml
trigger:
	- main
pool:
	name: MyPool
	demands:
	- agent.name -equals YOUR_AGENT_NAME
jobs:
	- job: Deploy_Flask_App

		displayName: 'Deploy Flask App'
		pool: MyPool
		steps:
	- task: UsePythonVersion@0
		inputs:
		versionSpec: '3.x'
		addToPath: true
	- script: |
		echo "Copie des fichiers du projet vers ~/myFlaskApp"
		mkdir -p ~/myFlaskApp
		cp -R * ~/myFlaskApp
	displayName: 'Copier les fichiers du projet vers ~/myFlaskApp'
	- script: |
		echo "Lancer le projet Flask"
		cd ~/myFlaskApp
		python3 -m venv venv
		source venv/bin/activate
		pip install -r requirements.txt
		nohup flask run --host=0.0.0.0 &
	displayName: 'Lancer le projet Flask'
	```
# Projet W4
- Application de reservation de train.
- but : mettre en place un frontend et un backend pour l'application
- binder les deux avec un depot distant
- reconfigurer les projets pour avec un gitlab flow (branches main, prod et feature)
- importer un fichier json dans la base de données mongodb + manipuler les variables d'environnement
- test d'integration (cypress)
- test de monté en charge (locust)
- But final, configurer le projet et mettre en place un gitlab flow
## difficultés
## notes
```sh
mongoimport --uri mongodb+srv://miham:XIFbvJrHOsCVTuzs@cluster0.qawqx.mongodb.net/tickethack --collection trips --type json --file ~/Downlad/trips.json --jsonArray
```
- working ci config
```yml
stages:
	- test
variables: CONNECTION_STRING: "mongodb+srv://miham:XIFbvJrHOsCVTuzs@cluster0.qawqx.mongodb.net/tickethack"
test_backend:
	stage: test
	image: cypress/browsers:latest
	script:
		- yarn install
		- yarn start & npx wait-on http://localhost:3000
		- yarn run test
	only:
		- main
		- develop
		- prod
		- feature/*
```
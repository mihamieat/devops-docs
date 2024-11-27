# Table des matière
# Git avancé
[Explain Git with D3](https://onlywei.github.io/explain-git-with-d3/#branch)

```bash
# creer un repo en lignes de commande
git init
git add .
git commit -m "Initial commit"
git push --set-upstream git@gitlab.com:mihamieat/dummy-repo2.git main
```
## Tags
[Git - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
- Créer un tag
```bash
git tag -a v1.4 -m "my version 1.4"v
```
- visioner un tag
```bash
git show v1.4
```
- uploader les tags sur le repo distant
```bash
git push origin --tag
```
- Faire une branche depuis un tag
```bash
git checkout -b version2 v2.0.0
```
- Supprimer un tag local
```bash
git tag -d v1.0.0
```
- Supprimer un tag sur le repo distant
```bash
git push origin --delete v1.0.0
```
# Le ticketing avec Jira
- Se définit dans la partie planification du cycle devops
# CI/CD
## Intégration continue
### Définition
- Dans la partie ***Build***, ***Test***, ***Release*** (Rendre accessible le sw).
- Chaque ***evolution*** (correction, ajout de fonctionnalités) fera l’objet d’une ***mise en production***.
> _sprint_ : course rapide sur un cycle court.
- But à chaque changement de code, on évite les risques de bug.
- L’integration et le déploiement continu sont des méthodes de contrôle et de verification du pipeline de mise en production.
- En fluidifiant la pipeline de mise en production, les devs **gagnent beaucoup de temps**. Cela permet de faire évoluer l’application plus souvent, on parle alors d’***iterations courte***.
- ***CI*** : représente les ***automatisations*** mises en place impliquant le ***code source***.
- ***CD*** : représente les ***automatisations*** mises en place impliquant le ***serveur de production***.
- Le ***YAML*** est un format de fichier important dans la CI/CD.
- Exemple de tests automatiques:
	- linter
	- dependences
	- contraintes (indentations…)
	- Tests unitaires.
### Step-by-step :
- cloner le repo
- créer un fiche de configuration (.gitlab-ci.yml) avec les premieres instructions
```yaml
stages:
	- stage1
jobs:
	stage: stage1
	script:
		- pwd
		- ls -la
```
- faire un commit pour ajouter le fichier de configuration et faire un push.
## Résumé
Voici un résumé bref des informations importantes sur l'intégration continue (CI) et le déploiement continu (CD) :
- **Intégration Continue (CI)** : Processus automatisé pour tester et intégrer les modifications de code fréquemment.
- **Pratiques de Développement** : Itérations courtes permettant une rétroaction rapide et une détection précoce des bugs.
- **Mise en Place avec GitLab** : Utilisation de pipelines CI/CD et de fichiers YAML pour automatiser les tests et la construction du code.
- **Merge Requests et CI** : Intégration des tests automatisés dans les merge requests pour améliorer la qualité du code.
- **Processus Automatisé** : Inclut le clonage du repo, la configuration de l'automatisation, et le lancement de l'automatisation via GitLab.
# Framework de test
## Cypress
- S’inscrit dans la phase ***test*** dans le cycle de Devops.
- Le test joue un role pour assurer la ***qualité***, la ***fiabilité*** et la ***stabilité*** tout au long du ***lifecycle*** du sw.
- contexte: chaque modification peut engendrer des bugs.
- 3 types de test:
	- tests unitaires, test de syntax
	- tests d’integration
	- tests end-to-end E2E
- Ces tests peuvent être exécutés automatiquement via des outils dédiés.
- L’exécution des tests pourra être déclenchée au push.
- Merge bloqué si le test ne passe pas.
- ***Cypress***, tests end to end.
- Cypress utilise un environnement Node.js.
### Installer npm
```sh
sudo apt remove nodejs npm -y

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash  
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p

source ~/.bashrc  
nvm install stable

nvm use stable
```
### Installer yarn
```sh
npm install -g yarn
```
### Initialiser un Nodejs
```sh
npm init -y
```
### Configurer les scripts dans package.json
```json
# package.json
{
...
	"scripts": {
	
	  "test": "npx cypress run --config video=false", 
	
	  "cypress:open": "npx cypress open"
	
	},
...
}
```
### Executer cypress
```sh
yarn run cypress:open
```
## Jest
- S’inscrit dans la phase de ***test*** du cycle devops.
- Contexte : résoudre des fonctionnalités mal développées et des fonctionnalités qui cassent des autres.
- Jest permet de rédiger des tests unitaires et des tests d’intégration.
# Runner
- Installer gitlab-runner sur votre VM
- Sur Gitlab, aller dans `Build` > `Runners` du groupe.
- Ajouter un nouveau runner pour le groupe. Suivez ensuite les instructions pour configurer votre runner (Attention à bien cocher la case “Run untagged job”). Au moment de sélectionner un executor, choisissez “shell”.
- Lancer le runner localement :
```bash
gitlab-runner run
```
- Créer un projet et mettre le meme tag que configuré dans GitLab
```yaml
stages:
	- checking

checking_job:
	stage: checking
	tags:
		- test # same tag as the runner
```
- Executer la pipeline
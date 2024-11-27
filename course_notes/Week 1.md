## Le materiel informatique
### Terminal & Scripting
- Le DevOps doit savoir la notion de ***hardware*** pour connaître les fonctions composantes.
- Notion de DevOps apparu en 2009.
- DevOps = ***Développement + Operation***
### Le materiel informatique
- La carte mere : circuite où brancher ses composants.
- Le processeur (CPU) : effectue les operations de calcul.
- La RAM : mémoire court terme de l’ordinateur. Fichier qu’on va pas forcément sauvegarder (ficher système)
- La carte réseau : permet de connecter au réseau des autres ordinateurs.
- Le disque dur : stockage des fichiers à long terme.
- Carte graphique: s’occupe du traitement graphique / calculs
## Linux
OS ***opensource***.
- deux grandes familles d’OS :
	- Base unix: Linus, macOS
	- Base MsDOS : Windows
- Sous linux il y’a des distributions : ***Debian***, Ubuntu (basé sur Debian), Fedora, Red Hat
- Debian est la plus standardisé.
- apt: système de gestion de package utilisé par Debian pour l’installation, la mise à jour et la gestion des logiciels.
```python
sudo apt update
sudo apt upgrade
sudo apt install curl
```
- sudo : utilisateur administrateur (qui a les droits sur tout, faire attention à l’utilisation)
- Debian versions ***serveur***, que des lignes de commande.
- Interface graphique pour faire des tests comme utilisateurs finaux.
## Debian
- C’est une des distributions de Linux.
- Utilisation non commerciale car opensource.
- L’utilisation de Debian se définit dans le cycle operate DevOps. Utilisé dans la gestion des machines.
### Definition de Debian
- Distribution Linux communautaire.
- Debian est à la base de plusieurs “sous” distributions.
### Structure des dossiers
- Dans linux, tout est dossier.
- Voici une brève description des dossiers essentiels de Linux :
	- ``/bin`` : Contient les exécutables essentiels du système
	- ``/boot`` : Fichiers nécessaires au démarrage du système
	- ``/dev`` : Fichiers représentant les périphériques
	- ``/etc`` : Fichiers de configuration du système
	- ``/home`` : Répertoires personnels des utilisateurs
	- ``/lib`` : Bibliothèques partagées essentielles
	- ``/media`` : Point de montage pour les périphériques amovibles
	- ``/mnt`` : Point de montage temporaire
	- `/opt` : Logiciels optionnels
	- `/proc` : Système de fichiers virtuel pour les informations du noyau
	- `/root` : Répertoire personnel de l'utilisateur root
	- `/sbin` : Exécutables système importants
	- `/tmp` : Fichiers temporaires
	- `/usr` : Programmes et données partagés en lecture seule
	- `/var` : Données variables comme les logs et les spools
- `alias`, manière d’écrire un raccourci.
- `PS1`, personnalisation du prompt (peut etre écrit dans ~/.bashrc)
- variable d’environnement: `export VARIABLE=”value”`
- `PATH`, ensemble de chemin. Chemin absolue ou relatif. ”/” = absolue
- la variable d’environnement `$PATH`
- ajouter un chemin supplémentaire :
```python
export PATH=$PATH/usr/local/sbin
```
- ``/usr/local/sbin`` a été ajouté
- ``systemd``, système d’initialisation des process.
- ``openssh``, outils pour se connecter à des serveurs à distance.
- ``awk``, langage de traitement par ligne de fichiers “plats”. pouvoir recupérer des colones, des noms des lignes dans un fichier. outils pour traiter les sorties consoles.
## Le cycle DevOps
- ***Integration*** et ***déploiement continue***.
- Esprit de ***fluidifier*** le travail.
- Contexte avant le devops. Avant le travail était manuel et tres peu d’automatisation.
- Encourage une collaboration entre les équipes de développement et d’operation.
## Le terminal
- structure de la commande : `nom de la commande options paramètres`
## Commandes système et pipelines
```sh
whoami
ps
kill
df
history
ip addr show
curl
cat
find
```
- `&&` permet d’executer deux commandes l’une à la suite de l’autre.
- `|` pipe, permet de faire passer les résultats d’une commande à une autre commande.
## Scripting
- Créer des bout de code pour automatiser des tâches.
- Permet de se concentrer sur des taches plus complexes.
- Aspect customization des scripts.
## Les droits Linux
### Users
- user, group, others
### Droits fichier
`-rwxrwxrwx`
### octale
droit d’execution = 1
droit d’écriture = 2
droit de lecture = 4
### chmod
```sh
chmod o=r— script.sh
chmod 744 script.sh
```
### chown
```sh
sudo chown paul:devops script.sh
```
### id
```sh
# nom du groupe principal
id -ng
# resultat : devops

# nom de tous les groupes
id -nG
# resultat : devops developers

```
## Crontab
[Crontab.guru - The cron schedule expression generator](https://crontab.guru/every-5-minutes)
## Python
### Python dans le contexte de DevOps
- Utilisé dans la phase de code
- Utile pour l’automatisation, le traitement de données, operations mathématiques.
- structure de données linéaire
### Boucle
```python
for i in range(0, 100):
	...
# Tableau d'index de 0 à 99.
```
### conditions
```python
if ... :
	...
elif ...:
  ...
elif ...:
...
elif ...:
  ...
else: # Else est un condition de fallback, il est à utiliser en dernier
	...
```
## Tâches système avec Python
- S’inscrit dans la phase ***operate***.
- Bash est efficace pour des taches système simple mais a des limites. Syntaxe difficile à lire
### Subprocess
***Module*** qui permet à Python de créer de nouveaux ***processus***.
```bash
# original shell script

sort fichier_source.txt > output_file.txt
```
```python
# equivalent in Python

import subprocess
with open("sorted_output.txt", "w") as output_file:
	subprocess.run("sort fichier_source.txt, shell=True, stdout=output_file)
```

- `subprocess.run([”liste de commande à executer”])`

In Python, `subprocess` is preferred over `os` for handling system-level operations such as executing external commands because it provides more powerful and flexible functionality. Here’s why `subprocess` is often used instead of `os`:

1. **Flexibility and Control**:
    - `subprocess` provides better control over input, output, and error streams through features like `Popen` and `communicate`, whereas `os.system()` only allows for simple command execution with less control over these streams.
2. **Security**:
    - Using `subprocess` is more secure because it allows you to pass arguments as a list, avoiding the need to construct a shell command as a string. This reduces the risk of shell injection attacks, which is a security risk with `os.system()` where you pass the entire command as a string.
3. **Return Codes and Error Handling**:
    - With `subprocess`, you can directly capture return codes, output, and errors. For example, you can use `subprocess.run()` or `subprocess.Popen()` to get the output, errors, and return code in a structured way, making error handling more efficient. In contrast, `os.system()` only returns the exit status of the command.
4. **Cross-Platform Compatibility**:
    - `subprocess` is designed to work consistently across different operating systems, while `os.system()` may have platform-specific behaviors and limitations.
5. **Deprecated Features**:
    - Some of the `os` functions like `os.popen()` are considered outdated or less preferable than the `subprocess`equivalents.

In summary, `subprocess` is more modern, flexible, secure, and easier to use for managing system-level command execution, making it a better choice in most cases over the older `os`-based methods.
### os
- Utile pour renommer des fichiers.
```bash
import os

if os.path.isfile("path"):
	print(

```
### shutil
- pour la manipulation des fichiers.
## Backend
- Role du backend : chercher les infos et faire des calculs.
### API & Webservice
- Le backend est dans le cadre du code dans le cycle DevOps.
- Envoyer des infos ou recevoir.
- Application Programming Interface.
- Les APIs sont partout.
- Exemples: carte de google, réseaux sociaux, moyens de paiement…
- Webservice est une architecture ou les programmes ne tournes pas dans le même environnement.
- Fonctionnement : l’application envoie une requête vers le ws; le ws traite la demande ; le ws envoie une réponse à l’application.
### Backend & Rest API
- Toujours dans la phase code du cycle DevOps
- Role : écouter les demandes pour y repondre
- Rest : Requetes stateles. Le serveur ne garde pas d’information sur la requête/son état
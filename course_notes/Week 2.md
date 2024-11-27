## La base de donnée
- Partie ***operate*** du cycle de devops
- Deux type principaux : ***Relationnelle*** et ***NoSQL***
- Les bases de données sont essentielles pour la ***gestion et le stockage des données***
- Avantages des bases de données :
    - Organisation ***structurée*** des données
    - Stockage efficace de ***grandes quantités de données***
    - ***Accès simultané*** pour plusieurs utilisateurs
    - Fonctionnalités de sécurité avancées
- Opérations ***CRUD*** : Create, Read, Update, Delete
- Types principaux de bases de données :
    - ***Relationnelles*** : pour ***données structurées***, supportent bien les transactions
    - ***NoSQL*** : flexibles, pour ***données non structurées*** ou ***semi-structurées***
    - Autres types : en mémoire, graphiques, orientées objet, etc.
- Choix entre relationnel et NoSQL dépend des besoins spécifiques du projet
- ***PostgreSQL*** se distingue par sa conformité SQL et ses performances pour les requêtes complexes
# Réseaux
S’inscrit dans la phase ***planification*** dans le cycle devops.
## GNS3
- Permet d’***emuler*** le materiel réseaux.
- Espace de virtualisation du réseau
## Switch
- Permet d’envoyer directement la requête au bon destinataire. Résau local
## Routeur
- Permet d’interconnecter différents réseaux informatique. (par internet)
## DHCP
- Permet d’attribuer dynamiquement une adresse IP.
## Firewall
- Agit comme un filtre. Filtre le trafic des requêtes. filtre les adresses ip, les protocoles, les ports…
# Adresses IP
- Les réseaux jouent un role pour permettre la communication entre les appareils.
## Serveur DNS
- C’est un serveur qui va traduire un nom de domaine ([google.com](http://google.com/)) en adresse IP (8.8.8.8)
## Ports
- Il est possible d’avoir plusieurs services sur la meme adresse IP grace aux ports. Mettre un serveur BDD, un service Web…
## Les protocoles
- Les protocoles sont des langages normalisés. (HTTP, FTP, SMTP, SSH…) Ces protocoles débutent une fois que la connexion entre les machine est établie.
# Administration système
## Administration du serveur
- S’inscrit dans la phase ***gestion*** dans le cycle devops.
- contexte : mise en place d’un serveur, modification de configuration, installation d’un service, maintenance, debug
- Le but est de prendre la main a distance des serveurs.
- Moyen connexion ssh
- SSH : voir le concept de clé publique, clé privée
- pour assurer la sécurité d’une connexion, on commence par générer une île depuis le poste du client.

```bash
ssh-keygen -f clientkey -N ""
```

- on peut donc venir recupérer notre cle publique

```bash
cat clientkey.pub
```

- modifier les clés autorisés

```bash
ssh-copy-id -i clientkey <user>@<host>
```

- se connecter au serveur

```bash
ssh -i clientkey <user>@<host>
```

- Fichier dans le serveur pour ajouter une nouvelle clé client :

```bash
# copy pub keys to
~/.ssh/authorized_keys
```

## Sécurité informatique
- S’inscrit dans la partie ***sécurité*** dans le cycle DevOps.
- Vaste sujet complexe qui couvre les réseaux, machine, logiciel et service, humain…
- Le Hacking est un des outils pour sécuriser son infrastructure
- Pour une sécurité efficace, il faut être le plus proactif possible (modifier constamment les configurations)
# GIT
- Important dans la démarche de partage de l’amelioration informatique.
> VCS utilisé : Gitlab
S’inscrit dans la partie ***gestion*** (Manage) dans le cycle DevOps. (mais pas seulement)
- permet de savoir
    - qui a modifé
    - quand à eu lieu la modification
    - qu’est ce qui a été modifié
    - pourquoi la modification a été réalisée
- facilite le travail collaboratif
- Permet de traquer chaque modification apportée à un fichier.
## cli
Git est une outil en ligne de commande. Il s’utilise dans le terminale.
## Commit
- Point de restauration
```bash
git add -u
git commit -m "refactor: action target file or code"
git push origine <remote_branch>
git status
git show <commit_id>
```
## Depot (repository, repo)
Les différents commits sont stockés sur l’ordinateur. Le lieu de stockage s’appelle un dépôt (repo).
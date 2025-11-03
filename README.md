# Exercice 2 - Option "Docker"

## Préparer son environnement

Pour démarrer votre machine virtuelle, lancer les commandes suivantes:

```bash
terraform init
terraform apply
```

Vous pouvez ensuite suivre l'avancée du déploiement via la commande suivante:

```bash
docker logs -f openclassrooms-p6-exo2
```

Votre machine virtuelle sera disponible lorsque vous verrez le message suivant s'afficher:

```shell
Ubuntu 24.04 LTS openclassrooms ttyS0
```

Vous devriez pouvoir ensuite vous connecter en SSH via la commande suivante:

```bash
ssh -o PreferredAuthentications=password openclassrooms@127.0.0.1 -p 2222
```

Le mot de passe par défaut est `openclassrooms`. Le compte `openclassrooms` fait partie des `sudoers`.

La connexion SSH fonctionne ? Vous êtes prêt pour réaliser l'exercice 2.

> **Note** N'hésitez pas à copier votre clé SSH sur la machine afin de simplifier votre connexion à celle-ci (notamment pour simplifier les opérations avec Ansible).

## Déploiement avec Ansible

Une fois la machine virtuelle démarrée et accessible, vous pouvez utiliser Ansible pour automatiser le déploiement de l'application Angular.

### Comment ça marche ?

Ansible est un outil qui permet d'automatiser la configuration et le déploiement. Le playbook `ansible/deploy.yml` effectue trois étapes principales :

1. **Installation de Node.js** : Installe Node.js et npm nécessaires pour construire l'application Angular
2. **Construction de l'application** : Clone le dépôt GitHub, installe les dépendances et construit l'application Angular
3. **Configuration de Nginx** : Installe et configure Nginx comme serveur web pour servir l'application

### Exécution

Depuis le répertoire racine du projet, exécutez :

```bash
ansible-playbook -i ansible/hosts ansible/deploy.yml
```

Cette commande va automatiquement :
- Installer tous les outils nécessaires sur la machine virtuelle
- Construire l'application Angular depuis le dépôt GitHub
- Configurer Nginx pour servir l'application sur le port 80

Une fois le déploiement terminé, vous pouvez accéder à l'application Angular en ouvrant http://localhost dans votre navigateur.

## À la fin de l'exercice

Pensez à faire un `terraform destroy` afin de supprimer toutes les ressources créées.

## Ressources

### Configuration par défaut

Le port `80 (TCP)` de la machine est exposé sur votre machine hôte. Ainsi, depuis votre machine hôte, si vous ouvrez l'URL http://localhost vous devriez vous connecter sur le port 80 de la machine virtuelle (par défaut aucun serveur HTTP n'est installé, vous aurez donc une erreur avant de finaliser l'exercice).

Une interface VNC est également disponible à l'adresse http://localhost:8006 (attention cependant, cette interface utilise un clavier QWERTY).

### Liens

- https://powersj.io/posts/ubuntu-qemu-cli/

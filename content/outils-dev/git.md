---
tags:
  - git
draft: "false"
title: git
---

# GIT

Git est un système de contrôle de version distribué qui permet de suivre les modifications apportées à des fichiers et de collaborer efficacement sur des projets de développement. Voici un guide détaillé pour comprendre et utiliser Git.

## 1. Introduction À Git

Git est principalement utilisé pour gérer des projets de développement de code source. Son avantage principal réside dans sa capacité à permettre à plusieurs utilisateurs de travailler simultanément sur un projet sans se perdre dans les versions du code.

### Avantages De Git

- **Contrôle de version** : Garder un historique complet de toutes les modifications apportées à un projet.
- **Travail collaboratif** : Plusieurs personnes peuvent travailler sur un même projet sans se chevaucher.
- **Branches** : Créer des branches pour tester des fonctionnalités ou résoudre des bugs sans perturber la branche principale.
- **Distribué** : Chaque utilisateur a une copie complète de l'historique du projet.

## 2. Installation De Git

### Sur Windows

1. Téléchargez Git depuis [https://git-scm.com/](https://git-scm.com/).
2. Lancez l'installateur et suivez les instructions par défaut.
3. Vous pouvez utiliser Git via Git Bash ou l'intégrer à un IDE comme Visual Studio Code.

### Sur Mac

1. Ouvrez Terminal.
2. Exécutez la commande `brew install git` (si vous avez Homebrew installé).
3. Sinon, téléchargez-le depuis [Git SCM](https://git-scm.com/).

### Sur Linux

1. Sur Ubuntu/Debian : `sudo apt install git`
2. Sur Fedora : `sudo dnf install git`

## 3. Configuration De Git

Une fois Git installé, il est nécessaire de configurer votre nom et votre adresse e-mail, qui seront utilisés pour associer vos commits à votre identité.

```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

## 4. Création D'un Repository (Dépôt Git)

### Créer Un Nouveau Dépôt Git

1. Dans votre terminal, allez dans le répertoire de votre projet.
2. Initialisez un dépôt Git avec :

```bash
git init
```

Cela crée un dossier `.git` caché dans votre répertoire, où Git stocke toutes les informations de version.

### Cloner Un Dépôt Existant

Si vous voulez travailler sur un projet existant, vous pouvez cloner un dépôt Git distant (par exemple, depuis GitHub) :

```bash
git clone https://github.com/username/projet.git
```

Cela crée une copie locale du projet dans votre répertoire de travail.

## 5. Travailler Avec Les Fichiers

### Ajouter Des Fichiers Au Suivi De Git

Pour ajouter un fichier à Git, vous devez l'indexer (ou le "stager") :

```bash
git add fichier.txt
```

Ou pour ajouter tous les fichiers modifiés :

```bash
git add .
```

### Vérifier L'état Des Fichiers

Pour voir les fichiers qui ont été modifiés mais pas encore commités :

```bash
git status
```

### Commit Des Modifications

Une fois que vous avez ajouté vos fichiers, vous pouvez les valider avec un commit. Un commit représente un enregistrement de l'état actuel du projet.

```bash
git commit -m "Message décrivant les modifications"
```

## 6. Gestion Des Branches

Les branches sont utilisées pour développer des fonctionnalités ou des corrections sans affecter la branche principale (souvent appelée `main` ou `master`).

### Créer Une Nouvelle Branche

```bash
git branch nouvelle-branche
```

### Basculer Entre Les Branches

```bash
git checkout nouvelle-branche
```

Ou vous pouvez combiner les deux commandes en une :

```bash
git checkout -b nouvelle-branche
```

### Fusionner Une Branche

Pour fusionner une branche dans la **branche actuelle** (par exemple, pour intégrer une fonctionnalité ou un correctif) :

```bash
git merge nouvelle-branche
```

### Supprimer Une Branche

Une fois une branche fusionnée et inutilisée, vous pouvez la supprimer :

```bash
git branch -d nouvelle-branche
```

## 7. Travailler Avec Des Dépôts Distant

Git permet de travailler avec des dépôts distants comme GitHub, GitLab ou Bitbucket.

### Ajouter Un Dépôt Distant

Lors de la création d'un dépôt local, vous pouvez ajouter un dépôt distant pour pousser (envoyer) vos modifications.

```bash
git remote add origin https://github.com/username/projet.git
```

### Pousser Des Modifications Vers Un Dépôt Distant

```bash
git push origin main
```

### Récupérer Des Modifications Depuis Un Dépôt Distant

Pour obtenir les dernières modifications du dépôt distant sans affecter vos fichiers locaux :

```bash
git fetch
```

Si vous voulez directement intégrer ces modifications dans votre branche actuelle, vous utilisez `git pull` :

```bash
git pull origin main
```

## 8. Gérer Les Conflits De Fusion

Les conflits se produisent lorsque Git ne peut pas fusionner automatiquement deux branches. Git marquera les parties du fichier en conflit, et vous devrez les résoudre manuellement.

### Résoudre Un Conflit

1. Ouvrez les fichiers conflictuels. Git marque les conflits avec des délimiteurs comme `<<<<<<<`, `=======`, et `>>>>>>>`.
2. Modifiez le fichier pour choisir quelle version conserver.
3. Après avoir résolu le conflit, vous devez ajouter les fichiers résolus :

```bash
git add fichier.conflict
```

4. Ensuite, faites un commit pour enregistrer la résolution du conflit.

## 9. Voir l'Historique

Git garde une trace de l'historique des commits. Vous pouvez voir l'historique avec la commande :

```bash
git log
```

Cette commande affiche tous les commits, avec des informations comme l'ID du commit, l'auteur, la date et le message.

Si vous voulez voir l'historique sous forme de graphique (utile pour les branches) :

```bash
git log --graph --oneline --decorate --all
```

## 10.Revenir À Un État Précédent

Parfois, vous devrez revenir à un commit précédent.

### Annuler Un Commit Local (non-poussé)

Si vous avez fait un commit local que vous souhaitez annuler, utilisez :

```bash
git reset --soft HEAD~1
```

Cela réinitialise l'état à un commit précédent, mais garde vos fichiers dans l'état où ils étaient.

Si vous voulez complètement annuler les modifications, vous pouvez utiliser :

```bash
git reset --hard HEAD~1
```

### Revenir à Un Commit Spécifique

Pour revenir à un commit particulier, utilisez :

```bash
git checkout <commit-hash>
```

## 11. Gestion Des Tags

Les tags sont des marqueurs utilisés pour signaler des versions importantes du projet.

### Créer Un Tag

```bash
git tag v1.0
```

### Lister Les Tags

```bash
git tag
```

### Pousser Un Tag Vers Un Dépôt Distant

```bash
git push origin v1.0
```

## 12. Trucs Et Astuces

- **Stashing** : Si vous travaillez sur des modifications mais que vous devez changer de branche, vous pouvez "stash" vos modifications pour les appliquer plus tard.

  ```bash
  git stash
  ```

- **Diff** : Pour voir les différences entre les modifications non commises et l'état actuel des fichiers.

  ```bash
  git diff
  ```

- **Alias** : Vous pouvez créer des alias pour des commandes Git fréquemment utilisées afin de les rendre plus courtes. Exemple :

  ```bash
  git config --global alias.st status
  ```

## Conclusion

Git est un outil puissant pour la gestion de version, et bien que cela puisse sembler complexe au début, une fois que vous comprenez les bases, vous pouvez travailler de manière plus productive sur des projets de développement collaboratifs. L'important est de bien comprendre les concepts de commits, branches et merges pour éviter les erreurs et gérer efficacement le code.

Ce guide vous donne les bases nécessaires, mais il existe beaucoup d'autres fonctionnalités avancées que vous pouvez explorer au fur et à mesure que vous progressez avec Git.

---
draft: "false"
tags:
  - docker
title: docker
---

# DOCKER

## Qu'est-ce Que Docker ?

Docker permet aux développeurs de conditionner une application avec toutes ses dépendances dans un conteneur léger et portable. Cela garantit que l'application fonctionne de manière cohérente, quel que soit l'environnement (développement, test, production) dans lequel elle est exécutée. Docker a été initialement conçu pour Linux, mais il est désormais compatible avec Windows et macOS, ainsi que divers services cloud comme AWS et Azure.

## Composants Clés De Docker

1. **Docker Engine** : Le cœur de Docker, un moteur client-serveur qui gère la création, l'exécution et la suppression des conteneurs. Il comprend :
   - **Docker Daemon** : Un service qui s'exécute en arrière-plan pour gérer les objets Docker (images, conteneurs, réseaux).
   - **API REST** : Permet aux applications de communiquer avec le daemon pour exécuter des commandes.
   - **Docker CLI** : Une interface en ligne de commande utilisée pour interagir avec le daemon.

2. **Docker Compose** : Un outil qui permet de définir et de gérer des applications multi-conteneurs à l'aide de fichiers YAML, facilitant ainsi le déploiement d'environnements complexes.
3. **Docker Hub** : Un registre public où les utilisateurs peuvent partager et télécharger des images Docker. C'est un lieu centralisé pour stocker des images.
4. **Docker Swarm** : Une fonctionnalité d'orchestration qui permet de gérer des clusters de conteneurs, facilitant l'équilibrage de charge et le déploiement à grande échelle.

## Comment Fonctionne Docker ?

### Architecture Basée Sur Le Noyau Linux

Docker repose sur des fonctionnalités du noyau Linux telles que les groupes de contrôle (cgroups) et les espaces de noms (namespaces). Ces technologies permettent d'isoler les processus dans des conteneurs, garantissant qu'ils s'exécutent indépendamment les uns des autres tout en partageant le même noyau du système d'exploitation. Cela optimise l'utilisation des ressources sans compromettre la sécurité[2][3].

### Création Et Gestion Des Conteneurs

- **Images Docker** : Les conteneurs sont créés à partir d'images Docker, qui sont des modèles statiques contenant tout ce qui est nécessaire pour exécuter une application (code, bibliothèques, dépendances). Les images sont organisées en couches, permettant une gestion efficace du stockage et un téléchargement incrémentiel[5][6].
  
- **Exécution des conteneurs** : Lorsqu'un conteneur est lancé à partir d'une image, il démarre instantanément car il n'a pas besoin d'un système d'exploitation complet. Chaque conteneur a son propre système de fichiers, sa propre pile réseau (avec une adresse IP unique) et peut avoir des ressources limitées définies pour le processeur et la mémoire[5][6].

### Déploiement Et Orchestration

Docker facilite le déploiement d'applications sur différentes infrastructures (serveurs physiques, machines virtuelles ou cloud). Grâce à des outils comme Docker Compose et Docker Swarm, il est possible de gérer plusieurs conteneurs en même temps, permettant une scalabilité rapide et un équilibrage de charge efficace.

## Quels Problèmes Docker a Résolut?

Docker résout plusieurs problèmes courants dans le développement et le déploiement d'applications :

1. **Problème de dépendances** : les applications ont souvent des dépendances spécifiques, telles que des bibliothèques ou des frameworks, qui doivent être installées et configurées correctement pour fonctionner. Docker permet de packager ces dépendances avec l'application, ce qui élimine les problèmes de compatibilité et de configuration.
2. **Problème d'environnement** : les applications peuvent nécessiter des environnements spécifiques pour fonctionner, tels que des versions spécifiques de langages de programmation ou de bibliothèques. Docker permet de créer des environnements isolés et personnalisés pour chaque application, ce qui élimine les problèmes d'environnement.
3. **Problème de portabilité** : les applications peuvent être difficiles à déployer sur différents systèmes et environnements, en raison de différences de configuration ou de compatibilité. Docker permet de déployer des applications de manière portable et fiable sur différents systèmes et environnements.
4. **Problème de sécurité** : les applications peuvent présenter des risques de sécurité si elles partagent des ressources ou des données avec d'autres applications. Docker permet de créer des conteneurs isolés et sécurisés pour chaque application, ce qui réduit les risques de sécurité.
5. **Problème de scalabilité** : les applications peuvent nécessiter une scalabilité horizontale ou verticale pour gérer des charges de travail importantes. Docker permet de créer des conteneurs qui peuvent être facilement mis à l'échelle pour gérer des charges de travail croissantes.
6. **Problème de gestion des ressources** : les applications peuvent nécessiter des ressources spécifiques, telles que de la mémoire ou des processeurs, pour fonctionner. Docker permet de gérer les ressources de manière efficace et de les allouer aux conteneurs en fonction de leurs besoins.
7. **Problème de collaboration** : les équipes de développement peuvent avoir des difficultés à collaborer sur des projets complexes, en raison de différences de configuration ou de compatibilité. Docker permet de créer des environnements de développement isolés et personnalisés pour chaque membre de l'équipe, ce qui facilite la collaboration et la communication.

En résumé, Docker résout les problèmes de dépendances, d'environnement, de portabilité, de sécurité, de scalabilité, de gestion des ressources et de collaboration, ce qui permet aux développeurs de créer, de déployer et de gérer des applications de manière efficace et fiable.

## Concepts Fondamentaux De Docker

Pour bien comprendre Docker, il est essentiel de se familiariser avec ses concepts clés :

### 1. Images Docker

Une **image Docker** est un package immuable contenant tout ce qu'une application nécessite pour fonctionner. Elle est construite à partir d'autres images, souvent basées sur des systèmes d'exploitation comme `alpine` ou `ubuntu`. Les images sont créées à partir d'un fichier appelé **Dockerfile**, qui contient les instructions nécessaires à leur construction[1][3].

### 2. Conteneurs

Les **conteneurs** sont des instances d'images qui exécutent les applications. Chaque conteneur possède son propre système de fichiers, sa pile réseau, et des limitations de ressources. Contrairement aux machines virtuelles, les conteneurs partagent le même noyau du système d'exploitation hôte, ce qui les rend plus légers et rapides à démarrer[2][4].

### 3. Dockerfile

Le **Dockerfile** est un fichier script contenant des instructions pour construire une image Docker. Chaque instruction dans le Dockerfile crée une nouvelle couche dans l'image, ce qui permet à Docker de réutiliser les couches inchangées lors des constructions ultérieures, optimisant ainsi le processus[1][5].

### 4. Volumes

Les **volumes** sont utilisés pour stocker des données générées et utilisées par les conteneurs. Ils permettent de conserver les données même si le conteneur est supprimé ou recréé, offrant ainsi une persistance des données.

### 5. Réseaux

Docker utilise des **réseaux virtuels** pour connecter les conteneurs entre eux et avec l'extérieur. Cela permet une communication sécurisée et isolée entre les différents services déployés dans des conteneurs.

## Virtual Machine Vs Docker

Voici une comparaison entre les machines virtuelles et Docker en termes plus simples :

### Machines Virtuelles

- C'est comme avoir un ordinateur dans un ordinateur
- Chaque machine virtuelle a son propre système d'exploitation et ses propres ressources (mémoire, processeur, etc.)
- Les machines virtuelles sont isolées les unes des autres et du système hôte
- Elles sont souvent utilisées pour les environnements de production, les tests et les développements

### Docker

- C'est comme avoir une petite boîte qui contient une application et ses dépendances
- Les conteneurs Docker partagent les mêmes ressources que le système hôte (mémoire, processeur, etc.)
- Les conteneurs Docker sont isolés les uns des autres, mais pas complètement du système hôte
- Docker est souvent utilisé pour les environnements de développement, les tests et les déploiements

## Docker Image Vs Docker Container

Dans Docker, il y a deux concepts importants : les images et les conteneurs.

**Docker Images**

- Une image Docker est un modèle de conteneur qui contient le code, les bibliothèques et les dépendances nécessaires pour exécuter une application.
- Les images Docker sont créées à partir d'un fichier Dockerfile qui définit les instructions pour construire l'image.
- Les images Docker sont stockées dans un registre Docker, tel que Docker Hub, qui permet de partager et de télécharger des images.
- Les images Docker sont immuables, ce qui signifie qu'elles ne peuvent pas être modifiées une fois créées.

**Docker Containers**

- Un conteneur Docker est une instance d'une image Docker qui est en cours d'exécution.
- Les conteneurs Docker sont créés à partir d'une image Docker et contiennent les mêmes fichiers et dépendances que l'image.
- Les conteneurs Docker sont isolés les uns des autres et du système hôte, ce qui signifie qu'ils ont leur propre espace de nommage, leur propre système de fichiers, etc.
- Les conteneurs Docker peuvent être démarrés, arrêtés, supprimés et réutilisés.

**Différences clés**

- **Immutabilité** : les images Docker sont immuables, tandis que les conteneurs Docker peuvent être modifiés.
- **Instance** : les conteneurs Docker sont des instances d'images Docker.
- **État** : les conteneurs Docker ont un état, tandis que les images Docker n'en ont pas.
- **Cycle de vie** : les conteneurs Docker ont un cycle de vie (création, démarrage, arrêt, suppression), tandis que les images Docker n'ont pas de cycle de vie.

Voici un exemple pour illustrer la différence :

- Imaginez que vous avez une image Docker pour un serveur web.
- Vous créez un conteneur Docker à partir de cette image et vous le démarrez.
- Le conteneur Docker est maintenant en cours d'exécution et vous pouvez y accéder via un navigateur web.
- Si vous modifiez le code du serveur web, vous devez créer une nouvelle image Docker et un nouveau conteneur Docker pour refléter les changements.

J'espère que cela aide à clarifier les choses !

## Les Registres Docker

Un **registre Docker** est un service qui permet de stocker et de distribuer des images Docker, qui sont des paquets auto-suffisants contenant tout le nécessaire pour exécuter une application. Ces registres centralisent les images, facilitant leur gestion et leur partage entre développeurs et équipes de développement.

### Fonctionnalités D'un Registre Docker

- **Stockage d'images** : Les registres hébergent des images Docker, organisées en dépôts, où chaque dépôt contient différentes versions d'une image, identifiées par des balises (tags) [1][2].
- **Distribution d'images** : Les utilisateurs peuvent télécharger (pull) des images depuis le registre ou y envoyer (push) leurs propres images .
- **Contrôle de version** : Grâce aux balises, il est possible de gérer efficacement les différentes versions d'une image, ce qui est crucial pour le déploiement et la mise à jour des applications .

### Types De Registres Docker

1. **Publics** : Comme **Docker Hub**, ces registres sont accessibles à tous et permettent de partager facilement des images .
2. **Privés** : Ces registres sont utilisés pour stocker des images dans un environnement sécurisé, souvent sur site ou dans le cloud privé, permettant un meilleur contrôle d'accès et une gestion des ressources .

### Exemples De Registres Docker

- **Docker Hub** : Le registre officiel et public de Docker.
- **Google Container Registry** : Un service de Google pour héberger des images.
- **Amazon Elastic Container Registry (ECR)** : Un service géré par Amazon pour stocker des images Docker .

En résumé, un registre Docker joue un rôle essentiel dans le développement moderne d'applications conteneurisées en fournissant une infrastructure pour le stockage, la gestion et la distribution des images.

## Pourquoi Utiliser Des Images Officielles Docker ?

Les images officielles de Docker présentent plusieurs avantages :

1. **Documentation claire** :
   - Les images officielles sont accompagnées d'une documentation détaillée, ce qui facilite leur compréhension et leur utilisation. Cela permet aux développeurs de rapidement trouver les informations dont ils ont besoin pour déployer et configurer leurs applications.

2. **Meilleures pratiques** :
   - Ces images sont conçues en suivant les meilleures pratiques de développement et de sécurité. Cela inclut des configurations optimisées, des mises à jour régulières et des pratiques de sécurité recommandées, ce qui contribue à réduire les vulnérabilités potentielles.

3. **Conçues pour les cas d'utilisation les plus courants** :
   - Les images officielles sont créées pour répondre aux besoins des cas d'utilisation les plus fréquents dans la communauté Docker. Cela signifie qu'elles sont souvent bien adaptées pour des applications populaires et largement utilisées, ce qui facilite leur intégration dans divers projets.

En résumé, utiliser des images officielles permet de bénéficier d'une base solide et fiable pour le développement d'applications conteneurisées, tout en garantissant une meilleure sécurité et une documentation adéquate.

## Les Tags Sur Docker

### Qu'est-ce Qu'un Tag ?

Un tag est une chaîne de caractères qui est associée à une image Docker. Les tags sont utilisés pour identifier les différentes versions d'une image et pour les distinguer les unes des autres.

### Types De Tags

Il existe deux types de tags sur Docker :

- **Tags nommés** : Les tags nommés sont des tags qui ont un nom spécifique, par exemple `latest`, `stable`, `dev`, etc. Ces tags sont utilisés pour identifier les différentes versions d'une image.
- **Tags numériques** : Les tags numériques sont des tags qui ont un numéro de version, par exemple `1.0`, `2.0`, `3.0`, etc. Ces tags sont utilisés pour identifier les différentes versions d'une image.

### Utilisation Des Tags

Les tags sont utilisés pour :

- **Identifier les versions d'une image** : Les tags permettent de identifier les différentes versions d'une image et de les distinguer les unes des autres.
- **Gérer les mises à jour** : Les tags permettent de gérer les mises à jour d'une image en créant de nouveaux tags pour les nouvelles versions.
- **Déployer des applications** : Les tags permettent de déployer des applications en utilisant les tags pour identifier les versions de l'image à déployer.

### Exemples De Tags

Voici quelques exemples de tags :

- `latest` : Ce tag est utilisé pour identifier la version la plus récente d'une image.
- `stable` : Ce tag est utilisé pour identifier la version stable d'une image.
- `dev` : Ce tag est utilisé pour identifier la version de développement d'une image.
- `1.0`, `2.0`, `3.0` : Ces tags sont utilisés pour identifier les différentes versions d'une image.

### Commandes Docker Pour Les Tags

Voici des exemples simples pour chaque commande Docker avec un tag spécifique :

- `docker tag` :
    
    bash
    
    `docker tag image_originale:1.0 nouvelle_image:1.1`
    
    Cela crée un nouveau tag `1.1` pour l’image `image_originale:1.0`.
    
- `docker push` :
    
    bash
    
    `docker push nouvelle_image:1.1`
    
    Cette commande pousse l’image taguée `nouvelle_image:1.1` vers un registre.
    
- `docker pull` :
    
    bash
    
    `docker pull image_exemple:2.0`
    
    Cela télécharge l’image `image_exemple` avec le tag `2.0` depuis un registre.
    
- `docker run` :
    
    bash
    
    `docker run -d --name mon_conteneur image_exemple:2.0`
    
    Cette commande lance un conteneur nommé `mon_conteneur` à partir de l’image `image_exemple:2.0`.
    

### Meilleures Pratiques Pour Les Tags

Voici quelques meilleures pratiques pour les tags :

- **Utiliser des tags clairs et descriptifs** : Les tags doivent être clairs et descriptifs pour que les utilisateurs puissent comprendre ce qu'ils représentent.
- **Utiliser des tags pour les versions** : Les tags doivent être utilisés pour identifier les différentes versions d'une image.
- **Utiliser des tags pour les environnements** : Les tags doivent être utilisés pour identifier les différents environnements dans lesquels une image est déployée.

## Les Commandes Docker

Voici un guide rapide sur les commandes Docker les plus courantes :

**Gestion des conteneurs**

- `docker run <image>` : Exécute un nouveau conteneur à partir d'une image
- `docker start <conteneur>` : Démarre un conteneur arrêté
- `docker stop <conteneur>` : Arrête un conteneur en cours d'exécution
- `docker restart <conteneur>` : Redémarre un conteneur
- `docker rm <conteneur>` : Supprime un conteneur

**Gestion des images**

- `docker pull <image>` : Télécharge une image à partir d'un registre (par exemple, Docker Hub)
- `docker push <image>` : Envoie une image vers un registre
- `docker build <répertoire>` : Construit une image à partir d'un Dockerfile
- `docker tag <image> <nouveau_nom>` : Renomme une image
- `docker rmi <image>` : Supprime une image

**Informations et débogage**

- `docker ps` : Affiche la liste des conteneurs en cours d'exécution
- `docker logs <conteneur>` : Affiche les journaux d'un conteneur
- `docker inspect <conteneur>` : Affiche des informations détaillées sur un conteneur
- `docker exec <conteneur> <commande>` : Exécute une commande à l'intérieur d'un conteneur

**Réseaux et volumes**

- `docker network create <réseau>` : Crée un réseau
- `docker network connect <réseau> <conteneur>` : Connecte un conteneur à un réseau
- `docker volume create <volume>` : Crée un volume
- `docker volume mount <volume> <conteneur>` : Monte un volume dans un conteneur

**Autres commandes**

- `docker info` : Affiche des informations sur la configuration de Docker
- `docker version` : Affiche la version de Docker
- `docker login` : Se connecte à un registre de conteneurs

Ces commandes sont les plus couramment utilisées, mais il en existe bien d'autres. Vous pouvez utiliser la commande `docker --help` pour afficher la liste complète des commandes disponibles.

## Comment Créé Un Image Docker

Voici un guide rapide sur comment créer une image Docker :

### Étape 1 : Créer Un Fichier `Dockerfile`

Un fichier `Dockerfile` est un fichier texte qui contient les instructions pour créer une image Docker. Créez un nouveau fichier nommé `Dockerfile` dans le répertoire racine de votre projet.

### Étape 2 : Définir la Base De L'image

La première instruction dans le fichier `Dockerfile` est `FROM`, qui définit la base de l'image. Vous pouvez utiliser une image existante comme base, par exemple :

```dockerfile
FROM ubuntu:latest
```

Cela signifie que votre image sera basée sur l'image Ubuntu la plus récente.

### Étape 3 : Définir Les Instructions De Construction

Les instructions suivantes dans le fichier `Dockerfile` définissent les étapes de construction de l'image. Voici quelques exemples d'instructions courantes :

- `RUN` : Exécute une commande shell dans le conteneur.
- `COPY` : Copie des fichiers du répertoire actuel dans le conteneur.
- `ADD` : Copie des fichiers du répertoire actuel dans le conteneur et décompresse les archives.
- `ENV` : Définit une variable d'environnement dans le conteneur.
- `WORKDIR` : Définit le répertoire de travail dans le conteneur.

Voici un exemple de fichier `Dockerfile` :

```dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y nginx

COPY index.html /var/www/html/

ENV PORT 80

WORKDIR /var/www/html

CMD ["nginx", "-g", "daemon off;"]
```

Cela signifie que l'image sera basée sur Ubuntu, installera Nginx, copiera un fichier `index.html` dans le répertoire `/var/www/html`, définira la variable d'environnement `PORT` à 80, définira le répertoire de travail à `/var/www/html` et exécutera la commande `nginx` avec les options `-g` et `daemon off;`.

### Étape 4 : Construire L'image

Une fois que vous avez créé le fichier `Dockerfile`, vous pouvez construire l'image en exécutant la commande suivante :

```bash
docker build -t mon-image .
```

Cela signifie que Docker construira l'image à partir du fichier `Dockerfile` et l'enregistrera sous le nom `mon-image`.

### Étape 5 : Vérifier L'image

Une fois que l'image est construite, vous pouvez vérifier qu'elle est correcte en exécutant la commande suivante :

```bash
docker images
```

Cela affichera la liste des images disponibles, y compris la nouvelle image que vous venez de créer.

### Étape 6 : Exécuter L'image

Enfin, vous pouvez exécuter l'image en exécutant la commande suivante :

```bash
docker run -p 80:80 mon-image
```

Cela signifie que Docker exécutera l'image `mon-image` et mappera le port 80 du conteneur sur le port 80 de votre machine hôte.

Voilà ! Vous avez créé une image Docker et l'avez exécutée.

[[Guide de création d'un server node avec Docker]]

## Docker Compose

Docker Compose est un outil de Docker qui permet de définir et de lancer des applications multi-conteneurs. Il permet de créer des fichiers de configuration qui définissent les services, les réseaux et les volumes nécessaires pour lancer une application.

### Avantages De Docker Compose

Les avantages de Docker Compose sont :

- **Simplification de la configuration** : Docker Compose permet de définir les services, les réseaux et les volumes nécessaires pour lancer une application dans un seul fichier de configuration.
- **Gestion des dépendances** : Docker Compose permet de gérer les dépendances entre les services et de lancer les services dans le bon ordre.
- **Réutilisation des configurations** : Docker Compose permet de réutiliser les configurations pour différents environnements, tels que le développement, les tests et la production.

### Fichier De Configuration De Docker Compose

Le fichier de configuration de Docker Compose est appelé `docker-compose.yml`. Il est écrit en YAML et définit les services, les réseaux et les volumes nécessaires pour lancer une application.

Voici un exemple de fichier `docker-compose.yml` :

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "80:80"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://user:password@db:5432/database
  db:
    image: postgres
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=database
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
  db-data:
```

Ce fichier définit deux services : `web` et `db`. Le service `web` est construit à partir du répertoire courant et expose le port 80. Il dépend du service `db` et utilise la variable d'environnement `DATABASE_URL` pour se connecter à la base de données. Le service `db` utilise l'image Postgres et définit les variables d'environnement pour la base de données. Il utilise également un volume pour stocker les données de la base de données.

### Commandes De Docker Compose

Voici quelques commandes de Docker Compose :

- `docker-compose up` : Lance les services définis dans le fichier `docker-compose.yml`.
- `docker-compose down` : Arrête les services définis dans le fichier `docker-compose.yml`.
- `docker-compose ps` : Affiche les services définis dans le fichier `docker-compose.yml`.
- `docker-compose logs` : Affiche les journaux des services définis dans le fichier `docker-compose.yml`.
- `docker-compose exec` : Exécute une commande dans un conteneur défini dans le fichier `docker-compose.yml`.

### Meilleures Pratiques Pour Docker Compose

Voici quelques meilleures pratiques pour Docker Compose :

- **Utiliser des noms de services clairs et descriptifs** : Les noms de services doivent être clairs et descriptifs pour que les utilisateurs puissent comprendre ce qu'ils représentent.
- **Utiliser des variables d'environnement** : Les variables d'environnement doivent être utilisées pour définir les paramètres des services, tels que les mots de passe et les adresses de base de données.
- **Utiliser des volumes** : Les volumes doivent être utilisés pour stocker les données des services, tels que les données de base de données.
- **Utiliser des réseaux** : Les réseaux doivent être utilisés pour connecter les services entre eux.

[[Comment créer un fichier docker-compose.yml]]

## Ressources

<https://www.youtube.com/watch?v=pg19Z8LL06w>

<iframe width="560" height="315" src="https://www.youtube.com/embed/MIWH2CpVyXs?si=HZf04pRKs8uF0F6X" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/rIrNIzy6U_g?si=jy6vYCFrBUuQuX_P" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Example Pratique (non testé)

Voici un exemple complet d'une API REST Node.js avec Docker, incluant la gestion des variables d'environnement, le build et l'exécution :

---

### **Structure Du Projet**

```
mon-api/
├── src/
│   ├── app.js
│   └── routes/
│       └── api.js
├── .env
├── .dockerignore
├── Dockerfile
├── docker-compose.yml
└── package.json
```

---

### **1. Fichier `app.js` (API De base)**

```javascript
const express = require('express');
const dotenv = require('dotenv');

dotenv.config(); // Charge les variables d'environnement

const app = express();
const port = process.env.PORT || 3000;

// Middleware
app.use(express.json());

// Route simple
app.get('/', (req, res) => {
  res.send(`API en cours d'exécution (Version: ${process.env.APP_VERSION})`);
});

// Route avec variable d'environnement
app.get('/config', (req, res) => {
  res.json({
    apiKey: process.env.API_KEY,
    environment: process.env.NODE_ENV
  });
});

// Démarrer le serveur
app.listen(port, () => {
  console.log(`Serveur démarré sur le port ${port}`);
});
```

---

### **2. Fichier `.env`**

```ini
PORT=3000
API_KEY=ma-super-cle-secrete
NODE_ENV=development
APP_VERSION=1.0.0
```

---

### **3. Fichier `Dockerfile` (Multi-stage Build)**

```dockerfile
# Étape 1 : Build de l'application
FROM node:18-alpine AS builder

WORKDIR /app

# Copie des fichiers de dépendances
COPY package*.json ./

# Installation des dépendances (production seulement)
RUN npm ci --only=production

# Copie du code source
COPY . .

# Étape 2 : Image finale
FROM node:18-alpine

ENV NODE_ENV=production

WORKDIR /app

# Copie des dépendances et du code depuis le builder
COPY --from=builder /app /app

# Exposition du port (utilise la variable PORT de .env)
EXPOSE ${PORT}

# Commande de démarrage
CMD ["node", "src/app.js"]
```

---

### **4. Fichier `.dockerignore`**

```
node_modules
npm-debug.log
.env.local
.git
```

---

### **5. Fichier `docker-compose.yml`**

```yaml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "${HOST_PORT}:${CONTAINER_PORT}"
    environment:
      - PORT=${CONTAINER_PORT}
      - API_KEY=${API_KEY}
      - NODE_ENV=${NODE_ENV}
      - APP_VERSION=${APP_VERSION}
    volumes:
      - ./src:/app/src
    networks:
      - api-network

networks:
  api-network:
    driver: bridge

volumes:
  node-modules:
```

---

### **6. Workflow Complet**

#### **Étape 1 : Créer Un Fichier `.env` Pour Docker Compose**

```ini
# .env (au même niveau que docker-compose.yml)
HOST_PORT=3000
CONTAINER_PORT=3000
API_KEY=secret123
NODE_ENV=production
APP_VERSION=1.0.0
```

#### **Étape 2 : Construire l'image**

```bash
docker-compose build
```

#### **Étape 3 : Démarrer Le conteneur**

```bash
docker-compose up -d
```

#### **Étape 4 : Tester l'API**

```bash
curl http://localhost:3000
# Résultat : "API en cours d'exécution (Version: 1.0.0)"

curl http://localhost:3000/config
# Résultat : {"apiKey":"secret123","environment":"production"}
```

---

### **Explications Clés**

1. **Variables d'environnement** :
   - Utilisation de `dotenv` pour charger le fichier `.env` en développement.
   - Dans Docker, les variables sont injectées via `docker-compose.yml` ou la ligne de commande.

2. **Sécurité** :
   - Le `.env` n'est **pas** copié dans l'image finale (grâce à `.dockerignore`).
   - Les secrets sont passés au runtime via `environment` dans Docker Compose.

3. **Bonnes Pratiques** :
   - Utilisation d'une image Alpine légère.
   - Build multi-stage pour réduire la taille de l'image finale.
   - Séparation claire des dépendances (`npm ci --only=production`).

4. **Débogage** :
   - Accéder au conteneur :

	 ```bash
     docker exec -it mon-api-api-1 sh
     ```

   - Voir les logs :

	 ```bash
     docker-compose logs -f
     ```

---

### **Commandes Alternatives (Sans Docker Compose)**

#### **Build manuel**

```bash
docker build -t mon-api:1.0 .
```

#### **Exécution Avec variables**

```bash
docker run -d \
  -p 3000:3000 \
  -e PORT=3000 \
  -e API_KEY=secret123 \
  -e NODE_ENV=production \
  --name mon-api \
  mon-api:1.0
```

---

### **Évolution Possible**

- Ajouter une base de données (PostgreSQL/MySQL) dans `docker-compose.yml`.
- Configurer un reverse proxy avec Nginx.
- Utiliser Docker Secrets pour les données sensibles.

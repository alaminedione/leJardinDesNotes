---
title: npm
draft: "false"
tags:
---

# Npm (Node Package Manager)

## **1. Qu'est-ce Que Npm ?**

**npm** est le gestionnaire de packages par défaut de **Node.js**. Il permet :
- D'installer des packages (bibliothèques) pour vos projets.
- De gérer les dépendances.
- De publier vos propres packages pour les partager avec la communauté.

---

## **2. Installation De npm**

**npm** est inclus automatiquement avec Node.js. Vous pouvez vérifier si npm est installé sur votre machine avec :

```bash
node -v  # Vérifie la version de Node.js
npm -v   # Vérifie la version de npm
```

Pour mettre à jour npm à la dernière version :

```bash
npm install -g npm
```

---

## **3. Initialisation D'un Projet npm**

Pour créer un nouveau projet avec npm :

1. Placez-vous dans votre dossier de projet :

   ```bash
   mkdir mon-projet
   cd mon-projet
   ```

2. Initialisez un fichier `package.json` qui contiendra les métadonnées du projet :

   ```bash
   npm init
   ```

   Répondez aux questions ou utilisez l'option `-y` pour tout accepter par défaut :

   ```bash
   npm init -y
   ```

---

## **4. Installer Des packages**

### A. Installer Un Package Localement

Pour installer une dépendance uniquement pour votre projet :

```bash
npm install <nom-du-package>
```

Le package sera ajouté dans le dossier `node_modules` et référencé dans `package.json` sous `dependencies`.

### B. Installer Un Package Globalement

Pour rendre un package disponible partout sur votre machine :

```bash
npm install -g <nom-du-package>
```

### C. Installer Une Version Spécifique

Si vous avez besoin d'une version particulière d'un package :

```bash
npm install <nom-du-package>@<version>
```

Exemple :

```bash
npm install express@4.18.2
```

---

## **5. Scripts npm**

Les scripts npm permettent d'exécuter des commandes définies dans `package.json`.

### Ajouter Un Script

Dans `package.json` :

```json
"scripts": {
  "start": "node index.js",
  "test": "mocha"
}
```

### Exécuter Un Script

Pour lancer un script :

```bash
npm run <nom-du-script>
```

Exemple :

```bash
npm run start
```

Pour des scripts prédéfinis comme `start` ou `test`, vous pouvez simplement écrire :

```bash
npm start
```

---

## **6. Gestion Des dépendances**

### A. Ajouter Une Dépendance En Tant Que Dépendance De Production

Par défaut, toutes les dépendances sont ajoutées sous `dependencies` :

```bash
npm install <nom-du-package>
```

### B. Ajouter Une Dépendance De Développement

Pour une dépendance utilisée uniquement pendant le développement (ex : linters, outils de test) :

```bash
npm install <nom-du-package> --save-dev
```

Elle sera ajoutée sous `devDependencies`.

### C. Supprimer Une Dépendance

Pour désinstaller un package :

```bash
npm uninstall <nom-du-package>
```

---

## **7. Mise à Jour Des dépendances**

Pour vérifier les mises à jour disponibles des packages :

```bash
npm outdated
```

Pour mettre à jour un package à sa dernière version :

```bash
npm update <nom-du-package>
```

Pour mettre à jour toutes les dépendances :

```bash
npm update
```

---

## **8. Fichiers importants**

### A. `package.json`

Contient les informations du projet et les dépendances. Exemple minimal :

```json
{
  "name": "mon-projet",
  "version": "1.0.0",
  "description": "Un projet simple Node.js",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "mocha": "^10.0.0"
  }
}
```

### B. `package-lock.json`

- Ce fichier garantit que les versions des packages restent identiques sur toutes les machines.
- **Ne pas le modifier manuellement**.

---

## **9. Création De Vos Propres packages**

### A. Créez Un Fichier Principal (ex : `index.js`)

Ajoutez-y vos fonctions ou classes à exporter.

### B. Configurez `package.json`

Ajoutez les métadonnées nécessaires, comme `name`, `version`, et `main` (pointant vers le fichier principal).

### C. Publiez Le Package

1. Connectez-vous à npm (nécessite un compte) :

   ```bash
   npm login
   ```

2. Publiez le package :

   ```bash
   npm publish
   ```

---

## **10. Gestion Des Versions (SemVer)**

npm suit la convention **SemVer (Semantic Versioning)** pour les versions :

```
MAJOR.MINOR.PATCH
```

- **MAJOR** : Modifications non rétrocompatibles.
- **MINOR** : Nouvelles fonctionnalités rétrocompatibles.
- **PATCH** : Corrections de bugs.

Exemple : `1.4.2`

- **1** : MAJOR
- **4** : MINOR
- **2** : PATCH

---

## **11. Commandes utiles**

### A. Afficher la Liste Des Packages Installés

Pour les packages locaux :

```bash
npm list
```

Pour les packages globaux :

```bash
npm list -g
```

### B. Supprimer Le Dossier `node_modules`

Si vous voulez nettoyer toutes les dépendances :

```bash
rm -rf node_modules
```

Puis réinstallez-les :

```bash
npm install
```

### C. Nettoyer Le Cache Npm

Pour résoudre des problèmes liés au cache :

```bash
npm cache clean --force
```

---

## **12. Alternatives Populaires à npm**

- **Yarn** : Plus rapide et doté de fonctionnalités supplémentaires.
- **pnpm** : Économise de l'espace disque grâce à un mécanisme de partage de dépendances.

---

Avec ce guide, vous êtes prêt à utiliser npm efficacement pour gérer vos projets Node.js ! Si vous avez des questions ou souhaitez approfondir une partie, n'hésitez pas à demander.

 **npx** fait partie de **npm**, mais il a une fonction distincte et complémentaire.

## **npx ** (Node Package eXecute)

**npx** est un outil livré avec **npm** à partir de la version **5.2.0** (sortie en 2017). Il permet d'exécuter facilement des packages Node.js sans avoir à les installer globalement ou localement dans votre projet.

---

### **Pourquoi Utiliser Npx ?**

1. **Exécuter des outils sans installation préalable :**
	
	- Avec `npx`, vous pouvez exécuter un package directement sans l'installer, ce qui est idéal pour les outils que vous utilisez rarement.
		
	- Exemple : Créer une application React avec `create-react-app` :

		```bash
        npx create-react-app mon-projet
        ```

		Cela télécharge et exécute temporairement le package `create-react-app`.

2. **Tester des versions spécifiques de packages :**
	
	- Exemple : Lancer une version précise de `eslint` :

		```bash
        npx eslint@7.32.0 .
        ```

3. **Gérer les conflits de version :**
	
	- Vous pouvez exécuter une version temporaire d'un package sans interférer avec d'autres projets utilisant une version différente.
4. **Exécuter des scripts Node.js instantanément :**
	
	- npx peut exécuter directement un fichier JavaScript :

		```bash
        npx node -e "console.log('Hello World')"
        ```

---

### **Principales Différences Entre Npm Et npx**

|**Caractéristique**|**npm**|**npx**|
|---|---|---|
|**Installation de packages**|Utilisé pour installer des packages localement (`npm install`) ou globalement (`npm install -g`).|Télécharge et exécute un package temporairement sans l'installer.|
|**Exécution de commandes**|Nécessite souvent l'installation préalable d'un package global ou local (exemple : `npm install -g eslint`).|Permet d'exécuter un package directement sans installation préalable (exemple : `npx eslint .`).|
|**Conflits de version**|Peut entraîner des conflits si plusieurs projets utilisent différentes versions d'un package.|Télécharge et utilise la version spécifiée sans interférer avec d'autres projets.|
|**Inclus avec npm**|Oui, depuis le début.|Oui, mais uniquement à partir de npm 5.2.0 et supérieur.|

---

### **Exemples D'utilisation De npx**

### 1. Lancer Un Outil Temporaire

Exemple : Créer un projet React :

```bash
npx create-react-app mon-projet
```

### 2. Tester Un Package Spécifique

Si vous voulez tester une commande spécifique avec une version particulière :

```bash
npx json-server@0.16.3 --watch db.json
```

### 3. Exécuter Un Fichier Local

Si vous avez un fichier script JavaScript local, vous pouvez le lancer avec :

```bash
npx ./mon-script.js
```

### 4. Utiliser Des Utilitaires Uniques

Exemple : Servir un projet statique avec `serve` :

```bash
npx serve
```

---

### **Conclusion**

**npx** est un outil puissant intégré à npm, conçu pour simplifier l'exécution de packages sans installation permanente. Il est particulièrement utile pour les outils à usage unique ou occasionnel. Si vous utilisez déjà npm, il est fortement recommandé d'explorer les possibilités offertes par **npx**.

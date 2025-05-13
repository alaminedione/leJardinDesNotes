---
title: Architecture Client-Serveur
tags:
  - System Design
  - Architecture Client-Serveur
draft : false
---

# Architecture Client-Serveur

**Présentation**
L'architecture client-serveur est un modèle fondamental dans le développement d'applications web. Elle divise les tâches entre les "clients", qui demandent des informations ou des services, et les "serveurs", qui fournissent ces informations ou services.

**Principes Clés**
- Le client initie la communication en envoyant une requête au serveur.
- Le serveur écoute les requêtes entrantes, les traite et renvoie une réponse au client.
- Cette séparation des préoccupations permet une gestion plus efficace des ressources et une meilleure évolutivité.

**Composants Principaux**
- **Client:** Une application (comme un navigateur web, une application mobile) qui envoie des requêtes.
- **Serveur:** Un système qui reçoit les requêtes, exécute la logique métier et renvoie des réponses.

**Guides d'utilisation**
Dans ce modèle, le client n'a pas besoin de connaître les détails internes du fonctionnement du serveur, seulement comment communiquer avec lui via un protocole défini (comme HTTP). Le serveur gère les ressources et les données, répondant aux demandes de plusieurs clients simultanément.

**Exemples de Code (Hono)**
Voici un exemple simple d'un serveur Hono qui répond à une requête GET :

```typescript
import { Hono } from 'hono';

const app = new Hono();

app.get('/', (c) => {
  return c.text('Bonjour depuis le serveur Hono!');
});

export default app;
```

Côté client (conceptuel, utilisant fetch API dans un navigateur):

```javascript
async function fetchData() {
  try {
    const response = await fetch('http://localhost:3000/'); // Remplacez par l'adresse de votre serveur
    const data = await response.text();
    console.log(data); // Affiche "Bonjour depuis le serveur Hono!"
  } catch (error) {
    console.error('Erreur lors de la récupération des données:', error);
  }
}

fetchData();
```

**Diagramme Mermaid**
```mermaid
graph LR
    Client -- Requête --> Serveur
    Serveur -- Réponse --> Client
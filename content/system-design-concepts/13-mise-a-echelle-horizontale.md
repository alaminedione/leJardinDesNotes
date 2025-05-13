---
title: Mise à l'échelle Horizontale
tags:
  - System Design
  - Mise à l'échelle Horizontale
draft : false
---

# Mise à l'échelle Horizontale (Horizontal Scaling)

**Présentation**
La mise à l'échelle horizontale, également appelée "scaling out", consiste à augmenter la capacité d'un système en ajoutant davantage de serveurs ou de machines pour distribuer la charge de travail. C'est une approche courante pour construire des systèmes hautement disponibles et évolutifs.

**Principes Clés**
- Ajout de plusieurs machines identiques ou similaires.
- La charge de travail est répartie entre les machines.
- Améliore la disponibilité et la résilience (si une machine tombe en panne, les autres peuvent prendre le relais).
- Permet de gérer des charges de trafic très importantes.
- Nécessite un mécanisme pour distribuer les requêtes entrantes (par exemple, un équilibreur de charge).

**Composants Principaux**
- **Multiples Serveurs:** Un groupe de machines exécutant la même application ou le même service.
- **Équilibreur de Charge (Load Balancer):** Un composant qui distribue les requêtes entrantes entre les serveurs disponibles.

**Guides d'utilisation**
La mise à l'échelle horizontale est essentielle pour les applications qui connaissent une croissance significative du trafic ou qui nécessitent une haute disponibilité. Elle est plus flexible et potentiellement plus rentable à grande échelle que la mise à l'échelle verticale. Cependant, elle introduit de la complexité, notamment la nécessité de gérer l'état partagé entre les serveurs (si l'application n'est pas sans état) et la mise en place d'un équilibreur de charge.

**Exemples de Code (Hono)**
Pour qu'une application Hono puisse être mise à l'échelle horizontalement, elle doit être conçue pour être sans état (stateless). Cela signifie qu'elle ne doit pas stocker d'informations spécifiques à la session utilisateur en mémoire sur un serveur particulier. Toutes les informations d'état doivent être stockées dans un système externe partagé, comme une base de données ou un cache distribué.

Voici un exemple conceptuel d'une application Hono sans état :

```typescript
import { Hono } from 'hono';
// Importation conceptuelle d'un client de cache distribué (par exemple, Redis)
// import cache from './cache';

const app = new Hono();

app.get('/user/:userId/settings', async (c) => {
  const userId = c.req.param('userId');
  // Récupérer les paramètres utilisateur d'un cache distribué ou d'une base de données
  // const settings = await cache.get(`user:${userId}:settings`) || await db.userSettings.get(userId);

  // Simulation de paramètres utilisateur
  const settings = { theme: 'dark', language: 'fr' };

  return c.json(settings);
});

app.post('/user/:userId/settings', async (c) => {
  const userId = c.req.param('userId');
  const newSettings = await c.req.json();
  // Enregistrer les nouveaux paramètres dans un cache distribué et/ou une base de données
  // await cache.set(`user:${userId}:settings`, newSettings);
  // await db.userSettings.update(userId, newSettings);

  return c.json({ status: 'settings updated', userId: userId, settings: newSettings });
});

export default app;
```
*Note : Dans cet exemple, l'état de l'utilisateur (ses paramètres) n'est pas stocké dans la mémoire de l'application Hono, mais serait géré par un service externe, ce qui permet à n'importe quelle instance de l'application Hono de traiter la requête.*

**Diagramme Mermaid**
```mermaid
graph LR
    Utilisateurs -- Requêtes --> LoadBalancer[Équilibreur de Charge]
    LoadBalancer -- Distribue --> Serveur1[Serveur Hono 1]
    LoadBalancer -- Distribue --> Serveur2[Serveur Hono 2]
    LoadBalancer -- Distribue --> Serveur3[Serveur Hono 3]

    Serveur1 -- Accède à l'état partagé --> ÉtatPartagé[Base de Données / Cache Distribué]
    Serveur2 -- Accède à l'état partagé --> ÉtatPartagé
    Serveur3 -- Accède à l'état partagé --> ÉtatPartagé
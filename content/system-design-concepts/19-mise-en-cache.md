---
title: Mise en Cache
tags:
  - System Design
  - Mise en Cache
  - Caching
draft : false
---

# Mise en Cache (Caching)

**Présentation**
La mise en cache est une technique qui consiste à stocker des copies de données fréquemment consultées dans un emplacement de stockage temporaire et rapide (le cache), généralement la mémoire vive (RAM). L'objectif est de réduire le temps d'accès aux données en évitant de les récupérer à chaque fois depuis une source plus lente, comme une base de données ou un disque.

**Principes Clés**
- Stockage temporaire de données pour un accès rapide.
- Réduit la latence et améliore le débit.
- Diminue la charge sur la source de données principale.
- Nécessite une stratégie pour gérer la cohérence entre le cache et la source de données (invalidation, TTL).

**Composants Principaux**
- **Cache:** L'emplacement de stockage rapide (par exemple, Redis, Memcached, cache en mémoire de l'application).
- **Source de Données:** L'emplacement d'origine des données (par exemple, base de données, service externe).
- **Stratégie de Cache:** Les règles qui déterminent comment les données sont stockées, récupérées et invalidées dans le cache (par exemple, Cache-Aside, Read-Through, Write-Through, Write-Back).
- **TTL (Time-to-Live):** Une durée après laquelle les données dans le cache sont considérées comme périmées et doivent être rafraîchies.

**Guides d'utilisation**
La mise en cache est efficace pour les données qui sont lues beaucoup plus fréquemment qu'elles ne sont écrites. Elle peut être implémentée à différents niveaux d'une architecture système : côté client (navigateur), côté DNS, côté CDN, côté application (en mémoire ou distribué), et côté base de données. Le choix de la stratégie de cache et de l'outil de cache dépend des exigences de cohérence, de performance et de scalabilité.

**Exemples de Code (Hono avec Cache - Conceptuel)**
Une application Hono peut interagir avec un système de cache distribué (comme Redis) pour stocker et récupérer des données fréquemment utilisées.

Voici un exemple conceptuel montrant comment une application Hono pourrait utiliser une stratégie Cache-Aside avec Redis :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importation conceptuelle d'un client Redis
// import redisClient from './redisClient';
// Importation conceptuelle d'un client de base de données
// import db from './db';

const app = new Hono();

app.get('/products/:productId', async (c) => {
  const productId = c.req.param('productId');
  const cacheKey = `product:${productId}`;

  try {
    // 1. Vérifier le cache
    // let product = await redisClient.get(cacheKey);

    let product = null; // Simulation: produit non trouvé dans le cache

    if (product) {
      console.log('Produit trouvé dans le cache');
      return c.json(JSON.parse(product)); // Désérialiser si stocké en JSON
    }

    // 2. Si non trouvé dans le cache, lire depuis la base de données
    console.log('Produit non trouvé dans le cache, lecture depuis la DB');
    // product = await db.products.findById(productId);

    // Simulation: produit trouvé dans la DB
    product = { id: productId, name: `Produit ${productId}`, price: 100 };

    if (product) {
      // 3. Stocker dans le cache pour les futures requêtes (avec TTL)
      // await redisClient.set(cacheKey, JSON.stringify(product), 'EX', 3600); // Cache pendant 1 heure
      console.log('Produit stocké dans le cache');
      return c.json(product);
    }

    return c.json({ message: 'Produit non trouvé' }, 404);

  } catch (error) {
    console.error('Erreur de cache ou DB:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});

export default app;
```
*Note : L'implémentation réelle nécessiterait un client Redis configuré et une logique de sérialisation/désérialisation si vous stockez des objets complexes.*

**Diagramme Mermaid**
```mermaid
graph LR
    Client -- Requête --> ApplicationHono[Application Hono]
    ApplicationHono -- 1. Vérifier Cache --> Cache[Cache (Redis/Memcached)]
    Cache -- Cache Hit --> ApplicationHono
    Cache -- Cache Miss --> ApplicationHono
    ApplicationHono -- 2. Lire DB --> BaseDeDonnees[Base de Données]
    BaseDeDonnees -- Données --> ApplicationHono
    ApplicationHono -- 3. Écrire Cache --> Cache
    ApplicationHono -- Réponse --> Client
---
title: Sharding de Base de Données
tags:
  - System Design
  - Sharding
  - Base de Données
draft : false
---

# Sharding de Base de Données (Sharding)

**Présentation**
Le sharding est une technique de partitionnement horizontal des données qui consiste à diviser une grande base de données en morceaux plus petits et plus gérables, appelés shards, et à les distribuer sur plusieurs serveurs de base de données. Cela permet de gérer des volumes de données massifs et d'augmenter les performances en répartissant la charge de lecture et d'écriture.

**Principes Clés**
- Division d'une base de données logique en plusieurs bases de données physiques (shards).
- Chaque shard contient un sous-ensemble des données totales.
- Les requêtes sont dirigées vers le shard approprié en fonction d'une clé de sharding.
- Améliore la scalabilité horizontale pour les opérations de lecture et d'écriture.
- Réduit la quantité de données qu'un seul serveur de base de données doit gérer.

**Composants Principaux**
- **Shards:** Les partitions individuelles de la base de données.
- **Clé de Sharding (Shard Key):** Une ou plusieurs colonnes utilisées pour déterminer comment les données sont distribuées entre les shards. Le choix de la clé de sharding est crucial pour une distribution uniforme des données et des requêtes.
- **Logique de Routage:** Le mécanisme (souvent intégré dans l'application, un proxy de base de données ou une couche de sharding) qui dirige les requêtes vers le shard correct en fonction de la clé de sharding.

**Guides d'utilisation**
Le sharding est généralement mis en œuvre lorsque la taille de la base de données devient trop importante pour être gérée efficacement par un seul serveur, même avec la réplication. Il est essentiel de choisir une clé de sharding appropriée qui permet une distribution équilibrée des données et minimise les requêtes qui nécessitent d'interroger plusieurs shards (requêtes "cross-shard"). Le sharding introduit de la complexité dans la gestion et les requêtes de base de données.

**Exemples de Code (Hono avec Sharding DB - Conceptuel)**
Dans une architecture shardée, l'application Hono doit être consciente de la logique de sharding pour diriger les requêtes vers le bon shard. Cela implique généralement d'inclure la clé de sharding dans les requêtes de base de données et d'utiliser une bibliothèque ou un service qui gère le routage vers le shard approprié.

Voici un exemple conceptuel montrant comment une application Hono pourrait interagir avec une base de données shardée en utilisant un ID utilisateur comme clé de sharding :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importation conceptuelle d'un client de base de données shardée
// import shardedDb from './shardedDb'; // Client qui gère le routage vers les shards

const app = new Hono();

// Route pour obtenir les données d'un utilisateur (lecture)
app.get('/users/:userId', async (c) => {
  const userId = c.req.param('userId');
  try {
    // Le client shardedDb utiliserait userId pour déterminer le shard
    // const userData = await shardedDb.users.findById(userId);

    // Simulation de données utilisateur
    const userData = { id: userId, name: `Utilisateur ${userId}`, shard: `shard_${parseInt(userId) % 4}` }; // Simulation avec 4 shards

    if (userData) {
      return c.json(userData);
    }
    return c.json({ message: 'Utilisateur non trouvé' }, 404);
  } catch (error) {
    console.error('Erreur DB shardée:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});

// Route pour créer un nouvel utilisateur (écriture)
app.post('/users', async (c) => {
  const newUser = await c.req.json();
  // Supposons que newUser.id est la clé de sharding
  if (!newUser.id) {
      return c.json({ message: 'ID utilisateur manquant pour le sharding' }, 400);
  }
  try {
    // Le client shardedDb utiliserait newUser.id pour déterminer le shard
    // const result = await shardedDb.users.insert(newUser);
    const addedUser = { ...newUser, shard: `shard_${parseInt(newUser.id) % 4}` }; // Simulation
    return c.json(addedUser, 201);
  } catch (error) {
    console.error('Erreur écriture DB shardée:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});


export default app;
```
*Note : L'implémentation réelle du client de base de données shardée (`shardedDb` dans l'exemple) est complexe et dépend du SGBD et de la stratégie de sharding.*

**Diagramme Mermaid**
```mermaid
graph TD
    Client -- Requête (avec Shard Key) --> ApplicationHono[Application Hono]
    ApplicationHono -- Routage basé sur Shard Key --> LogiqueSharding[Logique de Sharding]
    LogiqueSharding -- Dirige la requête --> ShardA[Shard A]
    LogiqueSharding -- Dirige la requête --> ShardB[Shard B]
    LogiqueSharding -- Dirige la requête --> ShardC[Shard C]

    ShardA -- Données --> LogiqueSharding
    ShardB -- Données --> LogiqueSharding
    ShardC -- Données --> LogiqueSharding

    LogiqueSharding -- Résultat --> ApplicationHono
    ApplicationHono -- Réponse --> Client
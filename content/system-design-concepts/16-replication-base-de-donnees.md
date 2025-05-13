---
title: Réplication de Base de Données
tags:
  - System Design
  - Réplication de Base de Données
  - Replication
draft : false
---

# Réplication de Base de Données (Replication)

**Présentation**
La réplication de base de données consiste à créer et maintenir des copies identiques d'une base de données sur plusieurs serveurs. Cela permet d'améliorer la disponibilité des données, la tolérance aux pannes et les performances en distribuant la charge de lecture.

**Principes Clés**
- Maintien de copies synchronisées des données sur plusieurs serveurs (répliques).
- Améliore la disponibilité : si un serveur tombe en panne, les autres répliques peuvent prendre le relais.
- Améliore les performances de lecture : les requêtes de lecture peuvent être distribuées sur plusieurs répliques.
- Introduit des défis de cohérence : assurer que toutes les répliques ont les données les plus récentes (cohérence éventuelle ou forte).

**Composants Principaux**
- **Réplique Primaire (Master):** Le serveur principal qui gère toutes les opérations d'écriture (INSERT, UPDATE, DELETE).
- **Répliques Secondaires (Read Replicas / Slaves):** Les copies de la base de données qui gèrent généralement les opérations de lecture (SELECT).
- **Mécanisme de Réplication:** Le processus par lequel les modifications de la réplique primaire sont copiées vers les répliques secondaires (synchrone ou asynchrone).

**Guides d'utilisation**
La réplication est couramment utilisée pour les applications à forte charge de lecture. Les requêtes d'écriture sont dirigées vers la réplique primaire, tandis que les requêtes de lecture sont réparties entre les répliques secondaires. Cela permet de décharger la réplique primaire et d'augmenter le débit global des lectures. La configuration de la réplication dépend du SGBD utilisé (par exemple, MySQL Replication, PostgreSQL Streaming Replication, MongoDB Replica Sets).

**Exemples de Code (Hono avec Réplication DB - Conceptuel)**
Dans une architecture utilisant la réplication de base de données, l'application Hono doit être configurée pour diriger les requêtes d'écriture vers la réplique primaire et les requêtes de lecture vers les répliques secondaires. Cela se fait généralement au niveau de la configuration de la connexion à la base de données ou en utilisant une bibliothèque d'accès aux données qui prend en charge la réplication.

Voici un exemple conceptuel montrant comment une application Hono pourrait diriger les requêtes vers différentes connexions DB :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importations conceptuelles des clients DB
// import primaryDb from './primaryDb'; // Connexion à la réplique primaire (écritures)
// import readReplicaDb from './readReplicaDb'; // Connexion aux répliques secondaires (lectures)

const app = new Hono();

// Route pour créer un nouvel article (écriture)
app.post('/articles', async (c) => {
  const newArticle = await c.req.json();
  try {
    // Utiliser la connexion à la réplique primaire pour l'écriture
    // const result = await primaryDb.articles.insert(newArticle);
    const addedArticle = { id: Math.random().toString(36).substring(7), ...newArticle }; // Simulation
    return c.json(addedArticle, 201);
  } catch (error) {
    console.error('Erreur écriture DB:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});

// Route pour obtenir un article (lecture)
app.get('/articles/:id', async (c) => {
  const articleId = c.req.param('id');
  try {
    // Utiliser la connexion aux répliques secondaires pour la lecture
    // const article = await readReplicaDb.articles.findById(articleId);
    const article = { id: articleId, title: 'Titre Article', content: 'Contenu...' }; // Simulation
    if (article) {
      return c.json(article);
    }
    return c.json({ message: 'Article non trouvé' }, 404);
  } catch (error) {
    console.error('Erreur lecture DB:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});

export default app;
```
*Note : La gestion de la logique de basculement (failover) en cas de défaillance de la réplique primaire est gérée par le SGBD ou des outils de gestion de cluster, pas directement dans le code Hono.*

**Diagramme Mermaid**
```mermaid
graph TD
    Client -- Requête Écriture --> ApplicationHono[Application Hono]
    ApplicationHono -- Écriture --> RépliquePrimaire[Réplique Primaire (Master)]
    RépliquePrimaire -- Réplication --> RépliqueSecondaire1[Réplique Secondaire 1]
    RépliquePrimaire -- Réplication --> RépliqueSecondaire2[Réplique Secondaire 2]

    Client -- Requête Lecture --> ApplicationHono
    ApplicationHono -- Lecture --> RépliqueSecondaire1
    ApplicationHono -- Lecture --> RépliqueSecondaire2

    RépliqueSecondaire1 -- Données --> ApplicationHono
    RépliqueSecondaire2 -- Données --> ApplicationHono
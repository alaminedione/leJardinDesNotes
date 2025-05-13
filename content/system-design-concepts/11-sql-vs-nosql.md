---
title: SQL vs NoSQL
tags:
  - System Design
  - SQL
  - NoSQL
draft : false
---

# SQL vs NoSQL

**Présentation**
Le choix entre les bases de données SQL (relationnelles) et NoSQL (non relationnelles) est une décision d'architecture cruciale qui dépend des besoins spécifiques d'une application en termes de structure des données, de scalabilité, de performance et de cohérence.

**Principes Clés**
- **Bases de Données SQL:**
    - Modèle de données relationnel avec schéma fixe (tables, lignes, colonnes).
    - Utilise SQL pour interroger et gérer les données.
    - Respecte généralement les propriétés ACID (Atomicité, Cohérence, Isolation, Durabilité), garantissant une forte cohérence.
    - Scalabilité verticale (mise à l'échelle sur un seul serveur plus puissant) et horizontale (réplication, sharding) possibles mais parfois plus complexes.
- **Bases de Données NoSQL:**
    - Modèles de données variés (clé-valeur, document, colonne large, graphe).
    - Schéma flexible ou dynamique.
    - Ne respecte pas toujours les propriétés ACID strictes, favorisant souvent la disponibilité et la tolérance aux partitions (modèle BASE - Basically Available, Soft state, Eventually consistent).
    - Scalabilité horizontale généralement plus facile et native.

**Composants Principaux**
- **SQL:** Tables, lignes, colonnes, clés primaires/étrangères, relations, requêtes SQL.
- **NoSQL:** Collections/Documents, clés/valeurs, nœuds/relations (pour les bases de données graphes), requêtes spécifiques au modèle.

**Guides d'utilisation**
- **Utilisez SQL si:** Vos données sont très structurées et relationnelles, vous avez besoin d'une forte cohérence des transactions, et la structure des données est relativement stable. Exemples : systèmes bancaires, plateformes e-commerce (pour les commandes).
- **Utilisez NoSQL si:** Vous avez besoin d'une grande scalabilité horizontale, vos données sont non structurées ou semi-structurées, la flexibilité du schéma est importante, ou vous avez des besoins de performance spécifiques (par exemple, lectures/écritures rapides à grande échelle). Exemples : profils utilisateurs, catalogues de produits (avec attributs variés), données de capteurs, réseaux sociaux.
Il est courant d'utiliser une approche polyglotte, combinant différents types de bases de données pour différentes parties d'une application.

**Exemples de Code (Hono avec différents accès DB - Conceptuel)**
Comme mentionné précédemment, Hono ne gère pas directement l'accès aux bases de données. L'exemple ci-dessous montre conceptuellement comment différentes routes Hono pourraient interagir avec différents types de bases de données en utilisant des bibliothèques appropriées.

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importations conceptuelles des clients DB
// import sqlDb from './sqlDb'; // Client pour DB SQL
// import nosqlDb from './nosqlDb'; // Client pour DB NoSQL

const app = new Hono();

// Route interagissant avec une DB SQL (conceptuel)
app.get('/sql/orders/:orderId', async (c) => {
  const orderId = c.req.param('orderId');
  try {
    // const order = await sqlDb.query('SELECT * FROM orders WHERE id = ?', [orderId]);
    const order = { id: orderId, item: 'Livre', amount: 25.50, userId: 123 }; // Simulation
    return c.json(order);
  } catch (error) {
    console.error('Erreur SQL DB:', error);
    return c.json({ message: 'Erreur SQL DB' }, 500);
  }
});

// Route interagissant avec une DB NoSQL (conceptuel)
app.get('/nosql/profiles/:userId', async (c) => {
  const userId = c.req.param('userId');
  try {
    // const userProfile = await nosqlDb.collection('profiles').findOne({ userId: userId });
    const userProfile = { userId: userId, username: `user_${userId}`, bio: 'Développeur' }; // Simulation
    return c.json(userProfile);
  } catch (error) {
    console.error('Erreur NoSQL DB:', error);
    return c.json({ message: 'Erreur NoSQL DB' }, 500);
  }
});

export default app;
```
*Note : Remplacez la logique simulée par l'utilisation de bibliothèques réelles pour interagir avec vos bases de données SQL et NoSQL.*

**Diagramme Mermaid**
```mermaid
graph TD
    AppHono[Application Hono]
    SQLDB[Base de Données SQL]
    NoSQLDB[Base de Données NoSQL]

    AppHono -- Requêtes structurées --> SQLDB
    AppHono -- Requêtes flexibles --> NoSQLDB

    SQLDB -- Données relationnelles --> AppHono
    NoSQLDB -- Données non relationnelles --> AppHono
---
title: Indexation de Base de Données
tags:
  - System Design
  - Indexation de Base de Données
  - Database Indexing
draft : false
---

# Indexation de Base de Données (Database Indexing)

**Présentation**
L'indexation de base de données est une technique utilisée pour améliorer la vitesse de récupération des données à partir d'une base de données. Un index est une structure de données qui permet de localiser rapidement les lignes d'une table sans avoir à parcourir chaque ligne, de manière similaire à l'index d'un livre.

**Principes Clés**
- Accélère les opérations de lecture (SELECT).
- Ralentit les opérations d'écriture (INSERT, UPDATE, DELETE) car l'index doit également être mis à jour.
- Nécessite de l'espace de stockage supplémentaire pour l'index lui-même.
- L'efficacité de l'indexation dépend des colonnes indexées et des types de requêtes.

**Types d'Index**
Il existe plusieurs types d'index, chacun adapté à des cas d'utilisation spécifiques :
- **Index Clustered (Groupé):** Détermine l'ordre physique de stockage des données dans la table. Une table ne peut avoir qu'un seul index groupé. Les recherches sur la colonne indexée sont très rapides.
- **Index Non-Clustered (Non-Groupé):** Crée une structure de données séparée qui contient les valeurs indexées et des pointeurs vers l'emplacement réel des données. Une table peut avoir plusieurs index non-groupés.
- **Index Unique:** Assure que toutes les valeurs dans la colonne indexée sont uniques, empêchant les doublons.
- **Index Composite (Multi-colonnes):** Créé sur plusieurs colonnes. Utile pour les requêtes qui filtrent ou trient sur plusieurs colonnes. L'ordre des colonnes dans l'index est important.
- **Index Full-Text (Texte Intégral):** Utilisé pour la recherche de texte libre dans de grandes quantités de texte.
- **Index Spatial:** Utilisé pour les données géospatiales.

**Composants Principaux**
- **Index:** La structure de données (souvent un arbre B-tree) qui stocke les valeurs des colonnes indexées et les pointeurs vers les lignes de données correspondantes.
- **Colonnes Indexées:** Les colonnes sur lesquelles l'index est créé.
- **SGBD:** Le système de gestion de base de données qui gère les index.

**Guides d'utilisation**
L'indexation doit être appliquée judicieusement aux colonnes fréquemment utilisées dans les clauses `WHERE`, `JOIN`, `ORDER BY` et `GROUP BY` des requêtes de lecture. Il est important de ne pas sur-indexer une base de données, car cela peut dégrader les performances d'écriture et consommer un espace disque excessif. L'analyse des requêtes lentes est essentielle pour identifier les opportunités d'indexation.

**Bonnes Pratiques d'Indexation**
- **Indexez les colonnes fréquemment utilisées dans les clauses `WHERE`, `JOIN`, `ORDER BY`, `GROUP BY`.**
- **Évitez la sur-indexation:** Trop d'index peuvent dégrader les performances d'écriture et consommer de l'espace disque.
- **Choisissez le bon type d'index:** Un index B-tree est un bon point de départ, mais d'autres types peuvent être plus appropriés pour des cas spécifiques.
- **Considérez les index composites:** Pour les requêtes qui filtrent sur plusieurs colonnes. L'ordre des colonnes est crucial.
- **Surveillez les performances:** Utilisez les outils de surveillance du SGBD pour analyser l'utilisation des index et identifier les requêtes lentes.
- **Reconstruisez les index si nécessaire:** Les index peuvent se fragmenter avec le temps, ce qui peut affecter leurs performances.
- **N'indexez pas les colonnes avec peu de valeurs distinctes:** L'indexation sur des colonnes avec une faible cardinalité (ex: `gender`) est généralement inefficace.

**Exemples de Code (Hono avec Indexation DB - Conceptuel)**
L'indexation est configurée au niveau de la base de données elle-même, et non dans le code de l'application Hono. Cependant, les requêtes exécutées par l'application Hono bénéficieront de l'indexation appropriée dans la base de données sous-jacente.

Voici un exemple conceptuel montrant une route Hono qui exécute une requête qui bénéficierait d'un index sur la colonne `email` dans une table `users` :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importation conceptuelle d'un client de base de données SQL
// import sqlDb from './sqlDb';

const app = new Hono();

app.get('/users/by-email', async (c) => {
  const email = c.req.query('email');
  if (!email) {
    return c.json({ message: 'Paramètre email manquant' }, 400);
  }

  try {
    // Cette requête bénéficierait d'un index sur la colonne 'email'
    // const user = await sqlDb.query('SELECT id, name FROM users WHERE email = ?', [email]);

    // Simulation de données utilisateur
    const user = { id: 123, name: 'Nom Utilisateur', email: email }; // Simulation

    if (user) {
      return c.json(user);
    }
    return c.json({ message: 'Utilisateur non trouvé' }, 404);
  } catch (error) {
    console.error('Erreur de base de données:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});

export default app;
```
*Note : L'index sur la colonne `email` serait créé en utilisant des commandes SQL (par exemple, `CREATE INDEX idx_user_email ON users (email);`) exécutées directement sur la base de données, indépendamment du code Hono.*

**Diagramme Mermaid**
```mermaid
graph TD
    ApplicationHono[Application Hono] -- Requête (SELECT WHERE email=...) --> SGBD[SGBD]
    SGBD -- Utilise l'Index --> Index[Index sur 'email']
    Index -- Pointeur vers données --> TableUtilisateurs[Table Utilisateurs]
    TableUtilisateurs -- Données --> SGBD
    SGBD -- Résultat --> ApplicationHono
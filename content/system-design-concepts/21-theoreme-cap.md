---
title: Théorème CAP
tags:
  - System Design
  - Théorème CAP
  - CAP Theorem
draft : false
---

# Théorème CAP (CAP Theorem)

**Présentation**
Le théorème CAP (Consistency, Availability, Partition Tolerance) est un principe fondamental des systèmes distribués. Il stipule qu'il est impossible pour un système de données distribué de garantir simultanément les trois propriétés suivantes : Cohérence, Disponibilité et Tolérance aux Partitions. En cas de partition réseau, un système doit choisir entre la Cohérence et la Disponibilité.

**Principes Clés**
- **Cohérence (Consistency):** Chaque lecture reçoit la donnée la plus récente ou une erreur. Toutes les répliques contiennent la même version des données.
- **Disponibilité (Availability):** Chaque requête reçoit une réponse (sans garantie que ce soit la donnée la plus récente). Le système reste opérationnel même si certains nœuds sont défaillants.
- **Tolérance aux Partitions (Partition Tolerance):** Le système continue de fonctionner malgré les pannes de communication (partitions réseau) entre les nœuds. Les partitions réseau sont inévitables dans un système distribué.

**Guides d'utilisation**
Étant donné que la tolérance aux partitions est généralement une exigence non négociable dans les systèmes distribués modernes (les pannes réseau se produisent), le théorème CAP implique que vous devez choisir entre la Cohérence et la Disponibilité en cas de partition.
- **Systèmes CP (Cohérence + Tolérance aux Partitions):** Privilégient la cohérence. En cas de partition, le système peut devenir indisponible pour certaines requêtes afin de garantir que les données renvoyées sont cohérentes. Exemples : bases de données relationnelles distribuées (certaines configurations), ZooKeeper, Consul (en mode cohérent).
- **Systèmes AP (Disponibilité + Tolérance aux Partitions):** Privilégient la disponibilité. En cas de partition, le système reste disponible pour les requêtes, mais il peut renvoyer des données potentiellement obsolètes. La cohérence est atteinte éventuellement (Eventual Consistency). Exemples : la plupart des bases de données NoSQL (Cassandra, DynamoDB, MongoDB - par défaut), systèmes DNS.

**Exemples de Code (Hono et CAP - Conceptuel)**
Le théorème CAP est un concept d'architecture système et ne se traduit pas directement par du code Hono spécifique. Cependant, la conception de votre application Hono et la manière dont elle interagit avec les bases de données ou d'autres services distribués doivent tenir compte des compromis CAP faits par ces services.

Par exemple, si votre application Hono utilise une base de données AP, vous devez être conscient que les lectures peuvent renvoyer des données obsolètes pendant une courte période après une écriture, et votre logique applicative doit pouvoir gérer cela.

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importation conceptuelle d'un client de base de données AP (par exemple, DynamoDB)
// import apDb from './apDb';

const app = new Hono();

app.get('/user-profile/:userId', async (c) => {
  const userId = c.req.param('userId');
  try {
    // Lecture depuis une base de données AP.
    // Les données peuvent être éventuellement cohérentes.
    // const userProfile = await apDb.profiles.get(userId);

    // Simulation de données de profil potentiellement obsolètes
    const userProfile = { userId: userId, status: 'actif', last_update: new Date().toISOString() }; // Simulation

    // Dans une application réelle, vous pourriez afficher un avertissement
    // si last_update est trop ancien, ou implémenter une logique pour gérer la cohérence éventuelle.

    return c.json(userProfile);
  } catch (error) {
    console.error('Erreur DB AP:', error);
    // En cas de partition, la DB AP pourrait toujours répondre (Disponibilité)
    return c.json({ message: 'Service de profil disponible (données potentiellement non à jour)' });
  }
});

export default app;
```
*Note : La gestion de la cohérence éventuelle dans le code applicatif peut impliquer des techniques comme la lecture de vos propres écritures (read-your-writes consistency) ou l'utilisation de versions de données.*

**Diagramme Mermaid**
```mermaid
graph TD
    subgraph "Théorème CAP"
        C[Cohérence]
        A[Disponibilité]
        P[Tolérance aux Partitions]
    end

    P -- Inévitable en système distribué --> Choix[Choisir entre C et A]

    Choix -- Si Cohérence > Disponibilité --> SystèmeCP[Système CP]
    Choix -- Si Disponibilité > Cohérence --> SystèmeAP[Système AP]

    SystèmeCP -- En cas de Partition --> Indisponibilité[Peut devenir Indisponible]
    SystèmeAP -- En cas de Partition --> CohérenceEventuelle[Cohérence Éventuelle]
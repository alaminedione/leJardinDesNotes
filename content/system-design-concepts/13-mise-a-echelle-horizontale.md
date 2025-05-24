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

**Avantages et Inconvénients**

**Avantages:**
- **Haute Disponibilité et Résilience:** Si une instance tombe en panne, les autres peuvent continuer à fonctionner, assurant la continuité du service.
- **Scalabilité Quasi Illimitée:** Permet de gérer des charges de trafic massives en ajoutant simplement plus de serveurs.
- **Rentabilité:** Peut utiliser du matériel moins cher et plus standardisé.
- **Flexibilité:** Permet d'adapter la capacité en fonction des fluctuations de la demande (auto-scaling).
- **Isolation des Pannes:** Une panne sur une instance n'affecte pas directement les autres.

**Inconvénients:**
- **Complexité Accrue:** Nécessite une gestion de la répartition de charge, de la synchronisation des données et de la cohérence de l'état.
- **Gestion de l'État:** Les applications doivent être conçues pour être sans état (stateless) ou utiliser des systèmes d'état partagé (bases de données distribuées, caches).
- **Latence Inter-serveurs:** La communication entre les instances peut introduire une latence supplémentaire.
- **Coût Opérationnel:** La gestion d'un grand nombre d'instances peut être plus complexe et nécessiter des outils d'orchestration (Kubernetes).

**Composants Principaux**
- **Multiples Serveurs:** Un groupe de machines exécutant la même application ou le même service.
- **Équilibreur de Charge (Load Balancer):** Un composant qui distribue les requêtes entrantes entre les serveurs disponibles.

**Guides d'utilisation**
La mise à l'échelle horizontale est essentielle pour les applications qui connaissent une croissance significative du trafic ou qui nécessitent une haute disponibilité. Elle est plus flexible et potentiellement plus rentable à grande échelle que la mise à l'échelle verticale. Cependant, elle introduit de la complexité, notamment la nécessité de gérer l'état partagé entre les serveurs (si l'application n'est pas sans état) et la mise en place d'un équilibreur de charge.

**Considérations pour la Conception d'Applications Évolutives Horizontalement**
Pour qu'une application puisse bénéficier pleinement de la mise à l'échelle horizontale, elle doit être conçue avec les principes suivants à l'esprit :
- **Statelessness (Sans État):** Les instances de l'application ne doivent pas stocker d'informations spécifiques à la session utilisateur en mémoire. Tout état doit être externalisé vers des services partagés (bases de données, caches distribués, files de messages).
- **Partage de Rien (Share-Nothing Architecture):** Chaque instance de l'application est indépendante et ne partage pas de ressources locales avec d'autres instances.
- **Idempotence:** Les opérations doivent pouvoir être répétées plusieurs fois sans causer d'effets secondaires indésirables. C'est important pour la résilience en cas de réessais de requêtes.
- **Conception Modulaire/Microservices:** Décomposer l'application en services plus petits et indépendants facilite la mise à l'échelle de chaque service individuellement.
- **Utilisation d'un Équilibreur de Charge:** Indispensable pour distribuer le trafic de manière égale entre les instances.
- **Gestion des Sessions:** Utiliser des bases de données de sessions partagées (ex: Redis, Memcached) ou des jetons (JWT) pour gérer l'état de la session utilisateur.
- **Files de Messages:** Utiliser des files de messages (ex: Kafka, RabbitMQ) pour la communication asynchrone entre les services et pour découpler les composants.

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
graph TD
    subgraph Clients
        C1(Client 1)
        C2(Client 2)
        C3(Client 3)
    end

    subgraph Équilibreur de Charge
        LB[Équilibreur de Charge]
    end

    subgraph Instances d'Application
        S1[Serveur App 1]
        S2[Serveur App 2]
        S3[Serveur App 3]
    end

    subgraph État Partagé
        DB[Base de Données / Cache Distribué]
    end

    C1 -- Requête --> LB
    C2 -- Requête --> LB
    C3 -- Requête --> LB

    LB -- Distribue --> S1
    LB -- Distribue --> S2
    LB -- Distribue --> S3

    S1 -- Accède/Met à jour --> DB
    S2 -- Accède/Met à jour --> DB
    S3 -- Accède/Met à jour --> DB

    S1 -- Réponse --> LB
    S2 -- Réponse --> LB
    S3 -- Réponse --> LB

    LB -- Réponse --> C1
    LB -- Réponse --> C2
    LB -- Réponse --> C3
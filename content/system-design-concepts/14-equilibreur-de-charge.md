---
title: Équilibreur de Charge
tags:
  - System Design
  - Équilibreur de Charge
  - Load Balancer
draft : false
---

# Équilibreur de Charge (Load Balancer)

**Présentation**
Un équilibreur de charge est un dispositif ou un logiciel qui distribue le trafic réseau entrant sur un groupe de serveurs backend, appelés pool de serveurs. Il garantit qu'aucune machine individuelle n'est surchargée, améliorant ainsi la réactivité et la disponibilité de l'application.

**Principes Clés**
- Distribution du trafic entrant sur plusieurs serveurs.
- Amélioration des performances en évitant la surcharge d'un serveur unique.
- Augmentation de la disponibilité et de la fiabilité en redirigeant le trafic loin des serveurs défaillants.
- Permet une maintenance sans interruption en retirant temporairement des serveurs du pool.

**Composants Principaux**
- **Trafic Entrant:** Les requêtes des clients.
- **Équilibreur de Charge:** Le point d'entrée unique qui reçoit le trafic.
- **Pool de Serveurs Backend:** Le groupe de serveurs (exécutant des applications comme Hono) qui traitent les requêtes.
- **Algorithmes de Répartition:** Les règles utilisées par l'équilibreur de charge pour décider quel serveur doit recevoir la prochaine requête (par exemple, Round Robin, Moins de Connexions, Hachage IP).
- **Vérifications de Santé (Health Checks):** Mécanismes pour vérifier si les serveurs backend fonctionnent correctement.

**Guides d'utilisation**
Les équilibreurs de charge sont essentiels dans les architectures à haute disponibilité et à mise à l'échelle horizontale. Ils peuvent opérer au niveau de la couche réseau (Layer 4) en se basant sur les adresses IP et les ports, ou au niveau de la couche application (Layer 7) en se basant sur des informations plus détaillées comme les en-têtes HTTP ou les cookies. L'intégration avec une application Hono se fait en plaçant l'équilibreur de charge devant les instances de l'application Hono.

**Exemples de Code (Hono)**
L'application Hono elle-même n'a pas besoin de code spécifique pour fonctionner derrière un équilibreur de charge. Elle écoute simplement les requêtes sur son port configuré. L'équilibreur de charge gère la distribution du trafic vers les différentes instances de l'application Hono.

Voici un exemple simple d'une application Hono qui fonctionnerait derrière un équilibreur de charge :

```typescript
import { Hono } from 'hono';

const app = new Hono();

// Cette application peut être déployée sur plusieurs serveurs.
// Un équilibreur de charge dirigerait le trafic vers ces instances.
app.get('/hello', (c) => {
  // Pourrait éventuellement inclure l'ID de l'instance pour le débogage
  // const instanceId = process.env.INSTANCE_ID || 'inconnu';
  return c.text('Bonjour depuis une instance de l\'application Hono!');
});

export default app;
```
*Note : L'équilibreur de charge est configuré séparément de l'application Hono. La configuration de l'équilibreur de charge spécifierait les adresses IP ou les noms d'hôte des serveurs exécutant l'application Hono.*

**Diagramme Mermaid**
```mermaid
graph LR
    Client -- Requête --> LoadBalancer[Équilibreur de Charge]
    LoadBalancer -- Algorithme de Répartition --> ServeurA[Serveur A (Hono)]
    LoadBalancer -- Algorithme de Répartition --> ServeurB[Serveur B (Hono)]
    LoadBalancer -- Algorithme de Répartition --> ServeurC[Serveur C (Hono)]

    ServeurA -- Réponse --> LoadBalancer
    ServeurB -- Réponse --> LoadBalancer
    ServeurC -- Réponse --> LoadBalancer

    LoadBalancer -- Réponse --> Client

    LoadBalancer -- Vérification de Santé --> ServeurA
    LoadBalancer -- Vérification de Santé --> ServeurB
    LoadBalancer -- Vérification de Santé --> ServeurC
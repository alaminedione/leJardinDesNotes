---
title: Proxy / Proxy Inverse
tags:
  - System Design
  - Proxy
  - Reverse Proxy
draft : false
---

# Proxy / Proxy Inverse

**Présentation**
Les proxys et les proxys inverses sont des serveurs intermédiaires qui gèrent le trafic réseau entre les clients et d'autres serveurs. Bien qu'ils agissent tous deux comme des intermédiaires, leur rôle et leur position dans l'architecture réseau diffèrent.

**Principes Clés**
- **Proxy (Forward Proxy):** Agit au nom d'un groupe de clients pour accéder à des ressources externes. Il protège l'identité des clients et peut être utilisé pour le filtrage de contenu ou la mise en cache côté client.
- **Proxy Inverse (Reverse Proxy):** Agit au nom d'un groupe de serveurs pour gérer les requêtes entrantes des clients. Il protège les serveurs backend, gère la répartition de charge, la terminaison SSL et la mise en cache côté serveur.

**Composants Principaux**
- **Proxy:** Se situe entre les clients et Internet.
- **Proxy Inverse:** Se situe entre Internet et les serveurs backend.

**Guides d'utilisation**
Un proxy est souvent utilisé dans les réseaux d'entreprise pour contrôler l'accès à Internet, surveiller l'utilisation ou mettre en cache des ressources fréquemment consultées. Un proxy inverse est couramment utilisé pour améliorer la sécurité, les performances et la fiabilité des serveurs web en distribuant le trafic, en gérant les certificats SSL et en servant de point d'entrée unique.

**Exemples de Code (Hono)**
Hono est généralement utilisé pour construire les services backend qui se trouvent *derrière* un proxy inverse. Le proxy inverse (comme Nginx, Apache, ou un service cloud comme AWS ALB) gérerait les requêtes entrantes et les transmettrait à l'application Hono appropriée.

Voici un exemple conceptuel montrant comment une application Hono pourrait recevoir une requête qui a traversé un proxy inverse. L'application Hono n'a pas besoin de savoir qu'un proxy inverse est présent, mais elle peut accéder aux informations ajoutées par le proxy inverse (comme l'adresse IP réelle du client via `X-Forwarded-For`).

```typescript
import { Hono } from 'hono';

const app = new Hono();

app.get('/info', (c) => {
  // Le proxy inverse ajoute souvent l'en-tête X-Forwarded-For
  const clientIp = c.req.header('X-Forwarded-For') || 'Inconnu';
  const host = c.req.header('Host');
  const userAgent = c.req.header('User-Agent');

  return c.text(`
    Informations de la requête reçue :
    Adresse IP du client (via proxy) : ${clientIp}
    Hôte demandé : ${host}
    Agent utilisateur : ${userAgent}
  `);
});

export default app;
```

**Diagramme Mermaid**
```mermaid
graph LR
    Client -- Requête --> Proxy[Proxy (Forward)]
    Proxy -- Requête --> Internet
    Internet -- Requête --> ReverseProxy[Proxy Inverse]
    ReverseProxy -- Requête --> ServeurBackend[Serveur Backend (Hono App)]
    ServeurBackend -- Réponse --> ReverseProxy
    ReverseProxy -- Réponse --> Internet
    Internet -- Réponse --> Proxy
    Proxy -- Réponse --> Client
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

**Cas d'Utilisation du Proxy (Forward Proxy)**
- **Contrôle d'accès et filtrage:** Les entreprises utilisent des proxys pour restreindre l'accès à certains sites web ou contenus pour leurs employés.
- **Mise en cache:** Les proxys peuvent mettre en cache les ressources web fréquemment demandées, réduisant ainsi la latence et la bande passante.
- **Anonymat et confidentialité:** Les utilisateurs peuvent masquer leur adresse IP réelle en acheminant leur trafic via un proxy.
- **Surveillance et journalisation:** Les proxys peuvent enregistrer toutes les requêtes et réponses, ce qui est utile pour l'audit et la sécurité.

**Cas d'Utilisation du Proxy Inverse (Reverse Proxy)**
- **Répartition de charge (Load Balancing):** Distribue le trafic entrant entre plusieurs serveurs backend pour améliorer la performance et la disponibilité.
- **Sécurité:** Protège les serveurs backend en agissant comme une première ligne de défense contre les attaques (DDoS, injections SQL).
- **Terminaison SSL/TLS:** Décharge les serveurs backend du chiffrement et du déchiffrement SSL, améliorant ainsi leurs performances.
- **Mise en cache:** Met en cache les réponses des serveurs backend pour réduire la charge et accélérer la livraison du contenu.
- **Compression et optimisation:** Peut compresser les réponses ou optimiser les images avant de les envoyer aux clients.
- **Routage d'API Gateway:** Dans une architecture de microservices, un proxy inverse peut servir de passerelle API pour router les requêtes vers les services appropriés.

**Composants Principaux**
- **Proxy:** Se situe entre les clients et Internet.
- **Proxy Inverse:** Se situe entre Internet et les serveurs backend.

**Technologies Courantes**
- **Pour les Proxys (Forward Proxy):**
    - **Squid:** Un proxy de mise en cache et de filtrage web très populaire.
    - **Privoxy:** Un proxy web sans cache avec des capacités de filtrage avancées pour la protection de la vie privée.
- **Pour les Proxys Inverses (Reverse Proxy):**
    - **Nginx:** Un serveur web et proxy inverse très performant, souvent utilisé pour la répartition de charge et la terminaison SSL.
    - **Apache HTTP Server (avec mod_proxy):** Peut également fonctionner comme un proxy inverse.
    - **HAProxy:** Un équilibreur de charge et proxy TCP/HTTP haute performance.
    - **Cloudflare, Akamai:** Services CDN qui agissent comme des proxys inverses distribués pour améliorer les performances et la sécurité.

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
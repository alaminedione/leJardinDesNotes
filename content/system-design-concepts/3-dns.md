---
title: DNS (Domain Name System)
tags:
  - System Design
  - DNS
draft : false
---

# DNS (Domain Name System)

**Présentation**
Le DNS, ou Domain Name System, est un système hiérarchique et décentralisé qui traduit les noms de domaine lisibles par l'homme (comme `google.com`) en adresses IP numériques (comme `172.217.160.142`) que les ordinateurs utilisent pour s'identifier sur Internet. C'est l'annuaire téléphonique d'Internet.

**Principes Clés**
- Le DNS élimine la nécessité pour les utilisateurs de mémoriser des adresses IP complexes.
- Il s'agit d'un système distribué, ce qui signifie qu'aucune entité unique ne gère toutes les traductions.
- Les informations DNS sont mises en cache à différents niveaux pour améliorer la vitesse et réduire la charge sur les serveurs DNS.

**Composants Principaux**
- **Noms de Domaine:** Les adresses web conviviales que les utilisateurs tapent dans les navigateurs.
- **Serveurs DNS:** Des serveurs spécialisés qui stockent les mappages entre les noms de domaine et les adresses IP. Il existe différents types de serveurs DNS (resolvers, root servers, TLD servers, authoritative nameservers).
- **Enregistrements DNS:** Les informations stockées sur les serveurs DNS qui lient un nom de domaine à une adresse IP ou à d'autres données (comme les enregistrements MX pour le courrier électronique).

**Guides d'utilisation**
Lorsqu'un utilisateur tape un nom de domaine dans son navigateur, une requête est envoyée à un serveur DNS pour obtenir l'adresse IP correspondante. Le navigateur utilise ensuite cette adresse IP pour se connecter au serveur web hébergeant le site. Ce processus est généralement très rapide et transparent pour l'utilisateur final.

**Exemples de Code (Hono)**
Hono, étant un framework côté serveur, n'interagit pas directement avec le processus de résolution DNS. La résolution des noms de domaine en adresses IP est gérée par le système d'exploitation sous-jacent ou l'environnement d'exécution. Cependant, votre application Hono peut faire des requêtes vers d'autres services en utilisant leurs noms de domaine.

Voici un exemple conceptuel montrant comment vous pourriez faire une requête HTTP depuis votre application Hono vers un autre service en utilisant son nom de domaine (la résolution DNS est gérée par le système).

```typescript
import { Hono } from 'hono';

const app = new Hono();

app.get('/fetch-example', async (c) => {
  try {
    // Le système résoudra 'example.com' en adresse IP
    const response = await fetch('https://example.com');
    const data = await response.text();
    return c.text(`Contenu de example.com (extrait) : ${data.substring(0, 100)}...`);
  } catch (error) {
    console.error('Erreur lors de la récupération:', error);
    return c.text('Erreur lors de la récupération du contenu.', 500);
  }
});

export default app;
```

**Diagramme Mermaid**
```mermaid
graph LR
    Utilisateur -- Tape nom de domaine --> Navigateur
    Navigateur -- Requête DNS --> ServeurDNS
    ServeurDNS -- Adresse IP --> Navigateur
    Navigateur -- Requête HTTP --> ServeurWeb[Serveur Web (Adresse IP)]
    ServeurWeb -- Réponse HTTP --> Navigateur
---
title: Adresse IP
tags:
  - System Design
  - Adresse IP
draft : false
---

# Adresse IP

**Présentation**
Une adresse IP (Internet Protocol) est une étiquette numérique unique attribuée à chaque appareil connecté à un réseau informatique qui utilise le Protocole Internet pour la communication. Elle sert d'identifiant pour localiser et communiquer avec des appareils spécifiques sur un réseau, comme Internet.

**Principes Clés**
- Chaque appareil sur un réseau IP doit avoir une adresse IP unique au sein de ce réseau.
- Les adresses IP permettent aux données d'être acheminées vers la bonne destination.
- Il existe deux versions principales : IPv4 (par exemple, 192.168.1.1) et IPv6 (par exemple, 2001:0db8:85a3:0000:0000:8a2e:0370:7334).

**Composants Principaux**
- **Adresse Réseau:** La partie de l'adresse IP qui identifie le réseau.
- **Adresse Hôte:** La partie de l'adresse IP qui identifie un appareil spécifique au sein du réseau.

**Guides d'utilisation**
Les adresses IP sont essentielles pour le fonctionnement d'Internet. Lorsque vous accédez à un site web, votre ordinateur utilise l'adresse IP du serveur web pour établir une connexion et échanger des données. Les routeurs utilisent les adresses IP pour diriger le trafic de données à travers les réseaux.

**Exemples de Code (Hono)**
Bien que Hono soit un framework web et ne gère pas directement l'attribution ou la gestion des adresses IP au niveau du système d'exploitation, vous pouvez accéder à l'adresse IP du client qui fait une requête via l'objet de contexte.

```typescript
import { Hono } from 'hono';

const app = new Hono();

app.get('/client-ip', (c) => {
  const clientIp = c.req.header('X-Forwarded-For') || c.req.header('X-Real-IP') || c.req.remoteAddress;
  return c.text(`Votre adresse IP est : ${clientIp}`);
});

export default app;
```
*Note : L'obtention de l'adresse IP réelle du client peut dépendre de l'infrastructure (par exemple, l'utilisation d'un proxy inverse ou d'un équilibreur de charge) et peut nécessiter de vérifier différents en-têtes.*

**Diagramme Mermaid**
```mermaid
graph LR
    AppareilA -- Utilise l'adresse IP --> AppareilB
    AppareilB -- Utilise l'adresse IP --> AppareilA
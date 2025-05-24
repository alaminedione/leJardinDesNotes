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

**Types d'Adresses IP**

- **Adresses IP Publiques:** Utilisées sur Internet, elles sont uniques et routables globalement. Elles permettent aux appareils d'être accessibles depuis n'importe où sur Internet.
- **Adresses IP Privées:** Utilisées au sein de réseaux locaux (LAN), elles ne sont pas routables sur Internet. Des plages spécifiques sont réservées à cet usage (ex: 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12).
- **Adresses IP Statiques:** Attribuées manuellement à un appareil et restent inchangées. Souvent utilisées pour les serveurs ou les équipements réseau.
- **Adresses IP Dynamiques:** Attribuées automatiquement par un serveur DHCP (Dynamic Host Configuration Protocol) pour une durée limitée. C'est le cas le plus courant pour les appareils clients (ordinateurs, smartphones).

**Composants Principaux**
- **Adresse Réseau:** La partie de l'adresse IP qui identifie le réseau.
- **Adresse Hôte:** La partie de l'adresse IP qui identifie un appareil spécifique au sein du réseau.

**Guides d'utilisation**
Les adresses IP sont essentielles pour le fonctionnement d'Internet. Lorsque vous accédez à un site web, votre ordinateur utilise l'adresse IP du serveur web pour établir une connexion et échanger des données. Les routeurs utilisent les adresses IP pour diriger le trafic de données à travers les réseaux.

**DHCP (Dynamic Host Configuration Protocol)**
Le DHCP est un protocole réseau qui permet d'attribuer automatiquement des adresses IP dynamiques aux appareils connectés à un réseau. Cela simplifie l'administration réseau en évitant la configuration manuelle de chaque appareil.

**NAT (Network Address Translation)**
Le NAT est une méthode qui permet à plusieurs appareils d'un réseau privé de partager une seule adresse IP publique pour accéder à Internet. Le routeur effectue la traduction d'adresse, ce qui aide à économiser les adresses IPv4 publiques et à masquer la topologie interne du réseau.

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
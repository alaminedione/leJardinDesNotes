---
title: WebSockets
tags:
  - System Design
  - WebSockets
draft : false
---

# WebSockets

**Présentation**
WebSockets est un protocole de communication qui permet un canal de communication bidirectionnel (full-duplex) persistant sur une seule connexion TCP. Contrairement au modèle requête-réponse de HTTP, WebSockets permet au serveur d'envoyer des données au client à tout moment, ce qui est idéal pour les applications en temps réel.

**Principes Clés**
- Communication bidirectionnelle (client et serveur peuvent envoyer des données indépendamment).
- Connexion persistante : une fois établie, la connexion reste ouverte jusqu'à ce qu'elle soit explicitement fermée.
- Faible latence : pas de surcharge de connexion pour chaque message.
- Efficace pour les applications en temps réel (chat, jeux en ligne, flux de données en direct).
- Utilise une poignée de main HTTP pour établir la connexion, puis passe au protocole WebSocket (`ws://` ou `wss://` pour sécurisé).

**Composants Principaux**
- **Client WebSocket:** Le côté client (généralement un navigateur web ou une application mobile) qui initie la connexion.
- **Serveur WebSocket:** Le côté serveur qui accepte la connexion et gère la communication bidirectionnelle.
- **Poignée de Main (Handshake):** Le processus initial basé sur HTTP pour établir la connexion WebSocket.
- **Messages:** Les données échangées sur la connexion WebSocket.

**Guides d'utilisation**
WebSockets est le choix privilégié pour les applications nécessitant des mises à jour en temps réel du serveur vers le client sans que le client n'ait à envoyer de requêtes répétées (polling). Des exemples typiques incluent les applications de chat, les tableaux de bord en direct, les jeux multijoueurs en ligne et les notifications push.

**Exemples de Code (Hono avec WebSockets - Conceptuel)**
Hono lui-même ne prend pas en charge nativement le protocole WebSocket. Pour ajouter la prise en charge de WebSocket à une application Hono, vous devriez utiliser une bibliothèque ou un adaptateur compatible avec Hono et votre environnement d'exécution (par exemple, `ws` pour Node.js, ou des APIs spécifiques si vous utilisez Cloudflare Workers ou Deno).

Voici un exemple conceptuel montrant comment une route Hono pourrait être "mise à niveau" vers une connexion WebSocket (la logique de gestion WebSocket dépendrait de la bibliothèque/plateforme utilisée) :

```typescript
import { Hono } from 'hono';
// Importation conceptuelle d'une bibliothèque WebSocket
// import { upgradeWebSocket } from './websocket-library';

const app = new Hono();

app.get('/realtime', (c) => {
  // Dans une implémentation réelle, vous utiliseriez une fonction
  // pour "mettre à niveau" la connexion HTTP en connexion WebSocket.
  // Cette fonction prendrait généralement en charge les événements
  // 'open', 'message', 'close', 'error'.

  // Exemple conceptuel de réponse pour indiquer que WebSocket est attendu
  if (c.req.header('Upgrade') === 'websocket') {
      console.log('Requête de mise à niveau WebSocket reçue');
      // Ici, vous appelleriez la logique de gestion WebSocket
      // return upgradeWebSocket(c.req, c.env); // L'implémentation dépend de la plateforme/librairie
      return c.text('Mise à niveau WebSocket en cours...', 101); // Code 101 Switching Protocols
  } else {
      return c.text('Cette endpoint nécessite une connexion WebSocket.');
  }
});

export default app;
```
*Note : L'implémentation réelle de la gestion des connexions WebSocket et de l'échange de messages dépend fortement de l'environnement d'exécution (Node.js, Deno, Cloudflare Workers, etc.) et des bibliothèques utilisées.*

**Diagramme Mermaid**
```mermaid
graph TD
    Client -- Requête HTTP (Upgrade: websocket) --> Serveur[Serveur (Application Hono)]
    Serveur -- Réponse HTTP (101 Switching Protocols) --> Client
    Client <--> |Connexion Persistante| Serveur
    Client -- Messages --> Serveur
    Serveur -- Messages --> Client
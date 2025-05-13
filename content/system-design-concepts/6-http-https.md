---
title: HTTP / HTTPS
tags:
  - System Design
  - HTTP
  - HTTPS
draft : false
---

# HTTP / HTTPS

**Présentation**
HTTP (Hypertext Transfer Protocol) et HTTPS (Hypertext Transfer Protocol Secure) sont les protocoles fondamentaux utilisés pour transférer des données sur le World Wide Web. Ils définissent comment les clients (comme les navigateurs web) et les serveurs communiquent pour échanger des informations.

**Principes Clés**
- **HTTP:** Protocole sans état basé sur des requêtes-réponses. Le client envoie une requête au serveur, et le serveur renvoie une réponse. Les données sont transférées en texte clair.
- **HTTPS:** La version sécurisée de HTTP. Il utilise SSL/TLS pour chiffrer la communication entre le client et le serveur, garantissant la confidentialité et l'intégrité des données.

**Composants Principaux**
- **Client:** Généralement un navigateur web.
- **Serveur:** Le serveur web hébergeant les ressources demandées.
- **Requête HTTP/HTTPS:** Envoyée par le client, contient la méthode (GET, POST, etc.), l'URL, les en-têtes et éventuellement un corps.
- **Réponse HTTP/HTTPS:** Envoyée par le serveur, contient un code de statut, des en-têtes et le corps de la réponse (par exemple, une page web).
- **SSL/TLS:** Protocoles de chiffrement utilisés par HTTPS pour sécuriser la connexion.

**Guides d'utilisation**
HTTP est utilisé pour accéder à la plupart des ressources web. HTTPS est essentiel pour les sites web qui traitent des informations sensibles (comme les identifiants de connexion, les informations de paiement) afin de protéger les données contre l'interception. L'utilisation de HTTPS est désormais une pratique standard pour tous les sites web afin d'assurer la sécurité et d'améliorer le référencement.

**Exemples de Code (Hono)**
Hono est un framework web qui fonctionne nativement avec HTTP et HTTPS. Lorsque vous déployez une application Hono, vous la configurez pour écouter les requêtes sur un port spécifique, généralement via HTTP ou HTTPS (souvent géré par un proxy inverse en production).

Voici un exemple simple d'une application Hono gérant différentes méthodes HTTP :

```typescript
import { Hono } from 'hono';

const app = new Hono();

// Gérer les requêtes GET
app.get('/data', (c) => {
  return c.json({ message: 'Ceci est une requête GET' });
});

// Gérer les requêtes POST
app.post('/submit', async (c) => {
  const body = await c.req.json();
  return c.json({ received: body, status: 'success' });
});

// Gérer les requêtes PUT
app.put('/items/:id', async (c) => {
  const id = c.req.param('id');
  const body = await c.req.json();
  return c.json({ id: id, updated: body, status: 'updated' });
});

export default app;
```
*Note : La gestion de HTTPS en production implique généralement la configuration d'un serveur web (comme Nginx) ou d'un service cloud (comme un Load Balancer) devant votre application Hono pour gérer le certificat SSL/TLS.*

**Diagramme Mermaid**
```mermaid
graph LR
    Client -- Requête HTTP --> ServeurWeb[Serveur Web]
    ServeurWeb -- Réponse HTTP --> Client

    Client -- Requête HTTPS (Chiffrée) --> ServeurWebSec[Serveur Web (HTTPS)]
    ServeurWebSec -- Réponse HTTPS (Chiffrée) --> Client
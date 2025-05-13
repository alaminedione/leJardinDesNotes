---
title: CDN (Content Delivery Network)
tags:
  - System Design
  - CDN
  - Content Delivery Network
draft : false
---

# CDN (Content Delivery Network)

**Présentation**
Un CDN, ou Content Delivery Network, est un réseau distribué géographiquement de serveurs qui travaillent ensemble pour fournir du contenu web (comme des images, des vidéos, des feuilles de style CSS et des fichiers JavaScript) aux utilisateurs de manière rapide et efficace. En mettant en cache le contenu sur des serveurs situés plus près de l'utilisateur final, un CDN réduit la latence et la charge sur le serveur d'origine.

**Principes Clés**
- Distribution du contenu statique sur un réseau mondial de serveurs (points de présence - PoP).
- Mise en cache du contenu aux PoP pour un accès rapide.
- Réduction de la latence en servant le contenu depuis le serveur le plus proche de l'utilisateur.
- Diminution de la charge sur le serveur d'origine.
- Amélioration de la résilience et de la disponibilité du contenu.

**Composants Principaux**
- **Serveurs d'Origine:** Le serveur où le contenu original est stocké (par exemple, votre serveur web ou votre stockage Blob).
- **Points de Présence (PoP):** Les centres de données distribués géographiquement où le contenu est mis en cache.
- **Serveurs de Cache:** Les serveurs au sein des PoP qui stockent et servent le contenu mis en cache.
- **Système de Routage:** Dirige les requêtes des utilisateurs vers le PoP le plus approprié.

**Guides d'utilisation**
L'utilisation d'un CDN est fortement recommandée pour les sites web et les applications qui servent du contenu statique à une audience mondiale. Pour utiliser un CDN avec une application Hono, vous configurez le CDN pour qu'il récupère le contenu statique de votre serveur d'origine (où votre application Hono pourrait servir ces fichiers, bien qu'il soit plus courant de les servir depuis un stockage Blob ou un serveur web optimisé pour le contenu statique). Le CDN mettra ensuite en cache ce contenu et le servira aux utilisateurs.

**Exemples de Code (Hono et CDN - Conceptuel)**
Bien que le CDN serve le contenu statique, votre application Hono pourrait générer les pages HTML qui référencent ce contenu statique via les URLs du CDN.

Voici un exemple conceptuel montrant une route Hono qui génère une page HTML référençant une image servie par un CDN :

```typescript
import { Hono } from 'hono';
import { html } from 'hono/html';

const app = new Hono();

// Supposons que votre image est stockée sur un CDN à cette URL
const CDN_IMAGE_URL = 'https://your-cdn-domain.com/images/logo.png';

app.get('/page-with-image', (c) => {
  return c.html(
    html`
      <!DOCTYPE html>
      <html>
      <head>
        <title>Page avec Image CDN</title>
      </head>
      <body>
        <h1>Bienvenue !</h1>
        <img src="${CDN_IMAGE_URL}" alt="Logo servi par CDN">
        <p>Cette image est chargée via un réseau de diffusion de contenu (CDN).</p>
      </body>
      </html>
    `
  );
});

export default app;
```
*Note : L'URL du CDN (`CDN_IMAGE_URL`) pointerait vers le contenu mis en cache par le CDN, qui à son tour a été récupéré de votre serveur d'origine.*

**Diagramme Mermaid**
```mermaid
graph LR
    Utilisateur -- Requête Page HTML --> ApplicationHono[Application Hono (Serveur d'Origine)]
    ApplicationHono -- Renvoie HTML (référençant CDN) --> Utilisateur
    Utilisateur -- Requête Image (URL CDN) --> CDN[Réseau de Diffusion de Contenu (CDN)]
    CDN -- Si Cache Miss --> ServeurOrigineStatic[Serveur d'Origine (Contenu Statique)]
    ServeurOrigineStatic -- Contenu --> CDN
    CDN -- Sert Image depuis PoP le plus proche --> Utilisateur
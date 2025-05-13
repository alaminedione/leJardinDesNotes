---
title: Latence
tags:
  - System Design
  - Latence
draft : false
---

# Latence

**Présentation**
La latence est le délai entre le moment où une requête est envoyée par un client et le moment où la première réponse est reçue du serveur. En termes simples, c'est le temps que prennent les données pour voyager d'un point à un autre sur un réseau. Une latence élevée peut rendre une application lente et peu réactive.

**Principes Clés**
- La distance physique entre le client et le serveur est un facteur majeur de latence.
- La congestion du réseau, la qualité de l'infrastructure et le nombre d'intermédiaires (routeurs, proxys) peuvent également affecter la latence.
- Réduire la latence améliore l'expérience utilisateur et les performances de l'application.

**Composants Principaux**
- **Client:** L'appareil qui envoie la requête.
- **Serveur:** L'appareil qui traite la requête et envoie la réponse.
- **Réseau:** L'infrastructure par laquelle les données transitent.

**Guides d'utilisation**
Pour minimiser la latence dans une architecture système, on peut déployer des serveurs plus près des utilisateurs (par exemple, en utilisant des réseaux de diffusion de contenu - CDN), optimiser les chemins réseau, réduire le nombre de requêtes nécessaires et optimiser le traitement côté serveur pour réduire le temps de réponse.

**Exemples de Code (Hono)**
La latence est principalement une caractéristique du réseau et de l'infrastructure, et non quelque chose que l'on gère directement dans le code de l'application Hono. Cependant, un code serveur efficace et rapide peut réduire la contribution du serveur au temps de latence total (temps de traitement).

Voici un exemple simple d'une route Hono qui répond rapidement pour minimiser le temps de traitement côté serveur :

```typescript
import { Hono } from 'hono';

const app = new Hono();

app.get('/fast-response', (c) => {
  // Une réponse simple et rapide
  return c.text('Réponse rapide!');
});

// Une route potentiellement plus lente (simulée)
app.get('/slow-response', async (c) => {
  // Simuler un délai de traitement (par exemple, une requête à une base de données lente)
  await new Promise(resolve => setTimeout(resolve, 200)); // Délai de 200ms
  return c.text('Réponse lente après traitement...');
});

export default app;
```
*Note : Le délai simulé dans `/slow-response` contribue au temps de réponse total, et donc à la latence perçue par le client.*

**Diagramme Mermaid**
```mermaid
graph LR
    Client -- Requête (Délai réseau) --> Serveur
    Serveur -- Traitement (Délai serveur) --> Serveur
    Serveur -- Réponse (Délai réseau) --> Client
    Note right of Client: Latence = Délai Requête + Délai Serveur + Délai Réponse
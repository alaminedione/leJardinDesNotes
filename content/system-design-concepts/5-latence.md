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

**Facteurs Influant sur la Latence**
Plusieurs facteurs peuvent contribuer à la latence :
- **Distance Géographique:** Plus le client et le serveur sont éloignés, plus le temps de trajet des données est long.
- **Congestion du Réseau:** Un trafic réseau élevé peut entraîner des retards dans la transmission des paquets.
- **Nombre de Hops:** Chaque routeur ou intermédiaire que les données traversent ajoute un petit délai.
- **Qualité de l'Infrastructure:** La bande passante, le type de connexion (fibre optique vs ADSL) et la qualité des équipements réseau.
- **Traitement Côté Serveur:** Le temps nécessaire au serveur pour traiter la requête et générer une réponse.
- **Mise en Cache:** L'absence ou une mauvaise gestion de la mise en cache peut augmenter la latence en forçant des requêtes complètes.
- **Protocoles Réseau:** Certains protocoles sont plus "verbeux" ou nécessitent plus d'allers-retours, augmentant la latence.

**Composants Principaux**
- **Client:** L'appareil qui envoie la requête.
- **Serveur:** L'appareil qui traite la requête et envoie la réponse.
- **Réseau:** L'infrastructure par laquelle les données transitent.

**Guides d'utilisation**
Pour minimiser la latence dans une architecture système, on peut déployer des serveurs plus près des utilisateurs (par exemple, en utilisant des réseaux de diffusion de contenu - CDN), optimiser les chemins réseau, réduire le nombre de requêtes nécessaires et optimiser le traitement côté serveur pour réduire le temps de réponse.

**Stratégies pour Réduire la Latence**
- **Utilisation de CDN (Content Delivery Networks):** Déployer des copies du contenu statique (images, CSS, JS) sur des serveurs situés plus près des utilisateurs finaux.
- **Optimisation du Réseau:** Utiliser des routes réseau plus directes, des protocoles optimisés (ex: HTTP/2, QUIC) et des équipements réseau performants.
- **Mise en Cache:** Mettre en cache les données fréquemment accédées au niveau du client, du proxy ou du serveur pour éviter des requêtes répétées.
- **Optimisation du Code Serveur:** Réduire le temps de traitement des requêtes côté serveur en optimisant les algorithmes, les requêtes de base de données et l'utilisation des ressources.
- **Réduction du Nombre de Requêtes:** Combiner les requêtes, utiliser le multiplexage (HTTP/2) ou le préchargement pour minimiser les allers-retours.
- **Compression des Données:** Réduire la taille des données transférées sur le réseau (Gzip, Brotli).
- **WebSockets:** Pour les applications nécessitant une communication bidirectionnelle en temps réel, les WebSockets réduisent la latence par rapport aux requêtes HTTP répétées.

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
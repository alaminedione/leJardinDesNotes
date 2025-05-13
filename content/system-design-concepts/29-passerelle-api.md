---
title: Passerelle API
tags:
  - System Design
  - Passerelle API
  - API Gateway
draft : false
---

# Passerelle API (API Gateway)

**Présentation**
Une passerelle API est un point d'entrée unique pour les clients accédant à un ensemble de services backend, souvent dans une architecture de microservices. Elle agit comme un proxy inverse pour les APIs, gérant des tâches transversales telles que l'authentification, la limitation de débit, la journalisation, la surveillance et le routage des requêtes vers les services appropriés.

**Principes Clés**
- Point d'entrée unique pour les clients.
- Gère les préoccupations transversales (sécurité, limitation de débit, etc.).
- Route les requêtes vers les services backend appropriés.
- Peut agréger les réponses de plusieurs services.
- Découple les clients des services backend individuels.

**Composants Principaux**
- **Clients:** Applications (web, mobile) qui appellent les APIs.
- **Passerelle API:** Le serveur qui reçoit toutes les requêtes client.
- **Services Backend:** Les services (microservices ou monolithiques) qui exécutent la logique métier.
- **Logique de Routage:** Détermine quel service backend doit traiter une requête entrante.
- **Plugins/Modules:** Fonctionnalités ajoutées à la passerelle (authentification, limitation de débit, etc.).

**Guides d'utilisation**
Une passerelle API est particulièrement utile dans les architectures de microservices pour simplifier l'accès aux nombreux services backend. Au lieu que les clients aient à connaître les adresses et les détails de chaque service, ils interagissent uniquement avec la passerelle. La passerelle gère ensuite la complexité du routage et des tâches transversales. Des exemples de passerelles API incluent NGINX (avec des modules appropriés), Kong, Apigee et les services de passerelle API des fournisseurs cloud (AWS API Gateway, Azure API Management).

**Exemples de Code (Hono derrière une Passerelle API - Conceptuel)**
Une application Hono fonctionnerait comme l'un des services backend derrière une passerelle API. L'application Hono n'a pas besoin de savoir qu'une passerelle API est présente, bien qu'elle puisse recevoir des informations supplémentaires via les en-têtes ajoutés par la passerelle (par exemple, l'ID de l'utilisateur authentifié).

Voici un exemple simple d'une application Hono qui pourrait être l'un des services backend :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';

const app = new Hono();

// Cette route pourrait être appelée par la passerelle API
app.get('/profile', (c) => {
  // La passerelle API pourrait ajouter un en-tête avec l'ID utilisateur authentifié
  const userId = c.req.header('X-Authenticated-User-Id');

  if (!userId) {
    // Si l'authentification n'a pas été gérée par la passerelle
    return c.json({ message: 'Non authentifié' }, 401);
  }

  // Dans une application réelle, vous récupéreriez le profil utilisateur
  // en utilisant l'userId depuis votre base de données.

  // Simulation de données de profil
  const userProfile = { userId: userId, name: `Utilisateur ${userId}`, role: 'membre' };

  return c.json(userProfile);
});

export default app;
```
*Note : La configuration de la passerelle API pour authentifier les utilisateurs et ajouter l'en-tête `X-Authenticated-User-Id` est gérée au niveau de la passerelle, pas dans le code Hono.*

**Diagramme Mermaid**
```mermaid
graph TD
    Client -- Requête --> PasserelleAPI[Passerelle API]
    PasserelleAPI -- Authentification --> SystèmeAuth[Système d'Authentification]
    PasserelleAPI -- Limitation de Débit --> SystèmeRateLimit[Système de Limitation de Débit]
    PasserelleAPI -- Routage --> ServiceA[Service A (Hono)]
    PasserelleAPI -- Routage --> ServiceB[Service B (Hono)]

    ServiceA -- Réponse --> PasserelleAPI
    ServiceB -- Réponse --> PasserelleAPI
    PasserelleAPI -- Réponse --> Client
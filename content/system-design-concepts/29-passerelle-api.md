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

**Fonctionnalités Clés d'une Passerelle API**
Une passerelle API offre un large éventail de fonctionnalités :
- **Routage des Requêtes:** Dirige les requêtes entrantes vers le service backend approprié en fonction de l'URL, des en-têtes, etc.
- **Authentification et Autorisation:** Gère la vérification des identités des clients et leurs permissions avant de transmettre la requête.
- **Limitation de Débit (Rate Limiting):** Contrôle le nombre de requêtes qu'un client peut envoyer dans un laps de temps donné.
- **Mise en Cache:** Met en cache les réponses des services backend pour améliorer les performances et réduire la charge.
- **Transformation des Requêtes/Réponses:** Modifie les requêtes entrantes ou les réponses sortantes (par exemple, agrégation, filtrage, formatage).
- **Journalisation et Surveillance:** Collecte des journaux et des métriques sur le trafic API pour l'analyse et le débogage.
- **Terminaison SSL/TLS:** Gère le chiffrement/déchiffrement SSL, déchargeant les services backend.
- **Gestion des Versions d'API:** Permet de gérer différentes versions d'une API.
- **Circuit Breaker:** Isole les services défaillants pour éviter la propagation des pannes.

**Composants Principaux**
- **Clients:** Applications (web, mobile) qui appellent les APIs.
- **Passerelle API:** Le serveur qui reçoit toutes les requêtes client.
- **Services Backend:** Les services (microservices ou monolithiques) qui exécutent la logique métier.
- **Logique de Routage:** Détermine quel service backend doit traiter une requête entrante.
- **Plugins/Modules:** Fonctionnalités ajoutées à la passerelle (authentification, limitation de débit, etc.).

**Guides d'utilisation**
Une passerelle API est particulièrement utile dans les architectures de microservices pour simplifier l'accès aux nombreux services backend. Au lieu que les clients aient à connaître les adresses et les détails de chaque service, ils interagissent uniquement avec la passerelle. La passerelle gère ensuite la complexité du routage et des tâches transversales. Des exemples de passerelles API incluent NGINX (avec des modules appropriés), Kong, Apigee et les services de passerelle API des fournisseurs cloud (AWS API Gateway, Azure API Management).

**Avantages et Inconvénients d'une Passerelle API**

**Avantages:**
- **Simplification pour les Clients:** Les clients n'ont qu'un seul point d'entrée à connaître, simplifiant l'intégration.
- **Gestion des Tâches Transversales:** Centralise l'authentification, la limitation de débit, la journalisation, etc., évitant la duplication de code dans chaque service.
- **Découplage:** Isole les clients des changements dans l'architecture backend (ajout/suppression de services, refactoring).
- **Agrégation de Services:** Peut combiner les réponses de plusieurs services en une seule réponse pour le client.
- **Sécurité Améliorée:** Agit comme une première ligne de défense contre les menaces.
- **Gestion des Versions:** Facilite la gestion des différentes versions d'API.

**Inconvénients:**
- **Point de Défaillance Unique (SPOF):** Si la passerelle API tombe en panne, l'ensemble du système peut devenir inaccessible. Nécessite une haute disponibilité.
- **Goulot d'Étranglement Potentiel:** Si la passerelle n'est pas correctement mise à l'échelle, elle peut devenir un goulot d'étranglement.
- **Complexité Accrue:** Ajoute une couche d'infrastructure supplémentaire à gérer et à surveiller.
- **Latence Supplémentaire:** Chaque requête passe par la passerelle, ce qui peut introduire une légère latence.
- **Complexité de la Configuration:** La configuration des règles de routage, de sécurité, etc., peut être complexe.

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
sequenceDiagram
    participant Client
    participant APIGateway
    participant AuthService[Système d'Authentification]
    participant RateLimitService[Système de Limitation de Débit]
    participant ServiceA[Microservice A]
    participant ServiceB[Microservice B]

    Client->>APIGateway: Requête API (ex: GET /users/profile)
    activate APIGateway

    APIGateway->>AuthService: 1. Vérifier Authentification/Autorisation
    activate AuthService
    AuthService-->>APIGateway: Résultat Authentification
    deactivate AuthService

    APIGateway->>RateLimitService: 2. Vérifier Limitation de Débit
    activate RateLimitService
    RateLimitService-->>APIGateway: Résultat Limitation de Débit
    deactivate RateLimitService

    alt Routage vers Service A
        APIGateway->>ServiceA: 3. Route la requête
        activate ServiceA
        ServiceA-->>APIGateway: Réponse du Service A
        deactivate ServiceA
    else Routage vers Service B
        APIGateway->>ServiceB: 3. Route la requête
        activate ServiceB
        ServiceB-->>APIGateway: Réponse du Service B
        deactivate ServiceB
    end

    APIGateway-->>Client: Réponse finale
    deactivate APIGateway
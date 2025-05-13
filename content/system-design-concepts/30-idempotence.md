---
title: Idempotence
tags:
  - System Design
  - Idempotence
  - Idempotency
draft : false
---

# Idempotence (Idempotency)

**Présentation**
L'idempotence est une propriété d'une opération ou d'une requête qui garantit que l'exécution répétée de cette opération ou requête produit le même résultat que si elle n'avait été exécutée qu'une seule fois. Dans les systèmes distribués, où les requêtes peuvent être retentées en raison de problèmes réseau ou de défaillances de service, l'idempotence est cruciale pour éviter les effets secondaires indésirables (comme débiter un client plusieurs fois pour la même transaction).

**Principes Clés**
- L'exécution multiple d'une opération idempotente a le même effet qu'une seule exécution.
- Important dans les systèmes distribués pour gérer les requêtes retentées.
- Ne signifie pas que la réponse de l'opération sera toujours la même (par exemple, une réponse peut indiquer que la ressource existait déjà lors des appels suivants), mais que l'état du système ne change pas après la première exécution réussie.

**Composants Principaux**
- **Opération/Requête:** L'action exécutée.
- **Identifiant d'Idempotence (Idempotency Key):** Un identifiant unique fourni par le client avec la requête pour permettre au serveur de détecter les doublons.
- **Mécanisme de Détection des Doublons:** Côté serveur, logique pour vérifier si une requête avec le même identifiant d'idempotence a déjà été traitée.
- **Stockage de l'État des Requêtes:** Un endroit où le serveur stocke les identifiants d'idempotence des requêtes traitées pendant une certaine période.

**Guides d'utilisation**
Les opérations qui modifient l'état du système (comme les requêtes POST, PUT, PATCH, DELETE) devraient idéalement être idempotentes, en particulier dans les systèmes où les retries automatiques sont activés. Pour rendre une opération idempotente, le client inclut un identifiant unique avec la requête. Le serveur stocke cet identifiant et, s'il reçoit une requête avec un identifiant déjà vu, il renvoie le résultat de la première exécution réussie sans exécuter à nouveau l'opération.

**Exemples de Code (Hono avec Idempotence - Conceptuel)**
Pour implémenter l'idempotence dans une application Hono, vous devriez extraire un identifiant d'idempotence de la requête (souvent un en-tête comme `Idempotency-Key`), vérifier si cet identifiant a déjà été traité, et stocker l'identifiant et le résultat de l'opération après le premier traitement réussi.

Voici un exemple conceptuel montrant comment une route Hono pourrait gérer l'idempotence pour une requête de création de ressource :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';
// Importation conceptuelle d'un client de cache ou de base de données pour stocker les clés d'idempotence
// import idempotencyStore from './idempotencyStore'; // Par exemple, Redis ou une table DB

const app = new Hono();

// Route pour créer une nouvelle ressource de manière idempotente
app.post('/resources', async (c) => {
  const idempotencyKey = c.req.header('Idempotency-Key');
  const requestBody = await c.req.json();

  if (!idempotencyKey) {
    return c.json({ message: 'En-tête Idempotency-Key manquant' }, 400);
  }

  try {
    // 1. Vérifier si la clé d'idempotence a déjà été traitée
    // const cachedResult = await idempotencyStore.getResult(idempotencyKey);

    const cachedResult = null; // Simulation: clé non trouvée

    if (cachedResult) {
      console.log(`Requête idempotente détectée pour la clé: ${idempotencyKey}. Renvoi du résultat mis en cache.`);
      return c.json(cachedResult.response, cachedResult.status);
    }

    // 2. Si non traitée, exécuter l'opération
    console.log(`Traitement de la nouvelle requête pour la clé: ${idempotencyKey}`);
    // const newResource = await createResource(requestBody); // Logique de création de ressource
    const newResource = { id: Math.random().toString(36).substring(7), ...requestBody }; // Simulation de création

    // 3. Stocker le résultat de l'opération avec la clé d'idempotence
    const responseStatus = 201; // Statut de la réponse de création
    // await idempotencyStore.storeResult(idempotencyKey, newResource, responseStatus);
    console.log(`Résultat stocké pour la clé: ${idempotencyKey}`);

    return c.json(newResource, responseStatus);

  } catch (error) {
    console.error('Erreur lors du traitement de la requête idempotente:', error);
    return c.json({ message: 'Erreur serveur' }, 500);
  }
});

// Fonction conceptuelle pour créer la ressource (remplacez par votre logique métier)
// async function createResource(data) {
//   // Logique pour créer la ressource dans la base de données, etc.
//   return { id: 'new-id', ...data };
// }


export default app;
```
*Note : L'implémentation de `idempotencyStore` nécessiterait un stockage persistant (base de données, cache distribué) et une stratégie d'expiration pour les clés d'idempotence.*

**Diagramme Mermaid**
```mermaid
graph TD
    Client -- Requête (avec Idempotency-Key) --> ApplicationHono[Application Hono]
    ApplicationHono -- 1. Vérifier Clé --> StockageIdempotence[Stockage Idempotence]
    StockageIdempotence -- Clé Trouvée --> ApplicationHono
    ApplicationHono -- Renvoie Résultat Mis en Cache --> Client

    StockageIdempotence -- Clé Non Trouvée --> ApplicationHono
    ApplicationHono -- 2. Exécuter Opération --> LogiqueMetier[Logique Métier]
    LogiqueMetier -- Résultat --> ApplicationHono
    ApplicationHono -- 3. Stocker Résultat --> StockageIdempotence
    ApplicationHono -- Renvoie Résultat --> Client
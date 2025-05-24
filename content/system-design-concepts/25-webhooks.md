---
title: Webhooks
tags: system-design webhooks
draft : false
---

# Webhooks

**Présentation**
Un webhook est un mécanisme qui permet à une application de fournir des informations en temps réel à une autre application. Au lieu que l'application cliente interroge (poll) constamment le serveur pour des mises à jour, le serveur envoie une notification (généralement une requête HTTP POST) à une URL spécifiée par le client dès qu'un événement se produit.

**Principes Clés**
- Communication basée sur les événements : les données sont envoyées lorsqu'un événement se produit.
- Modèle push : le serveur "pousse" les données vers le client.
- Nécessite une URL de rappel (callback URL) exposée par l'application cliente.
- Réduit la charge sur le serveur et le réseau par rapport au polling.

**Avantages et Inconvénients des Webhooks**

**Avantages:**
- **Mises à Jour en Temps Réel:** Permet une communication quasi instantanée entre les applications.
- **Efficacité:** Élimine le besoin de polling constant, réduisant la charge sur les deux systèmes et la consommation de bande passante.
- **Simplicité d'Implémentation:** Relativement simple à mettre en place pour les fournisseurs et les consommateurs (juste un endpoint HTTP).
- **Découplage:** Les systèmes peuvent interagir sans être fortement couplés, le fournisseur n'a pas besoin de connaître la logique interne du consommateur.

**Inconvénients:**
- **Dépendance à la Disponibilité du Consommateur:** Si l'URL de rappel du consommateur est indisponible, le webhook peut échouer (nécessite des mécanismes de relecture).
- **Sécurité:** Les webhooks peuvent être vulnérables aux attaques si la signature n'est pas vérifiée.
- **Complexité de la Gestion des Échecs:** Le fournisseur doit implémenter une logique de relecture et de gestion des erreurs.
- **Pas de Réponse Immédiate:** Le fournisseur ne reçoit pas de réponse immédiate sur le succès du traitement de l'événement par le consommateur.
- **Gestion des Doublons:** Les webhooks peuvent être livrés plusieurs fois, le consommateur doit gérer l'idempotence.

**Composants Principaux**
- **Fournisseur (Provider):** L'application qui déclenche l'événement et envoie le webhook (par exemple, Stripe, GitHub).
- **Consommateur (Consumer):** L'application qui reçoit le webhook à son URL de rappel (votre application).
- **URL de Rappel (Callback URL):** L'endpoint HTTP exposé par le consommateur pour recevoir les webhooks.
- **Événement:** L'action qui déclenche l'envoi du webhook (par exemple, un paiement réussi, un commit de code).
- **Charge Utile (Payload):** Les données envoyées dans la requête webhook, décrivant l'événement.

**Guides d'utilisation**
Les webhooks sont couramment utilisés pour intégrer des services tiers et réagir à des événements externes en temps quasi réel. Par exemple, recevoir des notifications de paiement de Stripe, des mises à jour de dépôt de GitHub, ou des messages entrants de Twilio. Pour utiliser des webhooks avec une application Hono, vous créez une route qui sert d'URL de rappel pour le fournisseur de webhook et implémentez la logique pour traiter la charge utile entrante.

**Considérations de Sécurité et de Fiabilité pour les Webhooks**
- **Vérification de la Signature:** Toujours vérifier la signature du webhook (si fournie par le fournisseur) pour s'assurer que la requête provient d'une source légitime et n'a pas été falsifiée.
- **HTTPS Obligatoire:** L'URL de rappel doit impérativement utiliser HTTPS pour chiffrer les données en transit.
- **Idempotence:** Concevoir l'endpoint de réception du webhook pour être idempotent, car les webhooks peuvent être livrés plusieurs fois.
- **Gestion des Échecs et Relectures:** Le fournisseur de webhook doit implémenter une logique de relecture avec un backoff exponentiel en cas d'échec de livraison. Le consommateur doit répondre rapidement (200 OK) pour éviter les relectures inutiles.
- **Files de Messages (Message Queues):** Pour les applications à fort trafic ou nécessitant un traitement asynchrone, il est recommandé de placer le traitement du webhook dans une file de messages pour éviter de bloquer l'endpoint de réception.
- **Journalisation et Surveillance:** Journaliser les webhooks reçus et surveiller l'endpoint pour détecter les anomalies ou les échecs.
- **Secret de Webhook:** Utiliser un secret partagé pour générer et vérifier les signatures.

**Exemples de Code (Hono recevant un Webhook - Conceptuel)**
Une application Hono peut facilement servir d'endpoint pour recevoir des webhooks. Vous définissez une route (souvent POST) qui correspond à l'URL de rappel configurée chez le fournisseur de webhook.

Voici un exemple conceptuel montrant comment une application Hono pourrait recevoir un webhook de paiement :

```typescript
import { Hono } from 'hono';
import { json } from 'hono/json';

const app = new Hono();

// Endpoint pour recevoir les webhooks de paiement
app.post('/webhooks/payment', async (c) => {
  const payload = await c.req.json(); // La charge utile du webhook

  console.log('Webhook de paiement reçu:', payload);

  // Dans une application réelle, vous vérifieriez la signature du webhook
  // pour vous assurer qu'il provient d'une source fiable et traiteriez l'événement.

  // Exemple de traitement basé sur le type d'événement (conceptuel)
  if (payload.event_type === 'payment_succeeded') {
    console.log(`Paiement réussi pour la commande ${payload.order_id}`);
    // Mettre à jour votre base de données, envoyer une confirmation, etc.
  } else {
    console.log(`Événement de paiement non géré: ${payload.event_type}`);
  }

  // Renvoyer une réponse 200 OK pour indiquer que le webhook a été reçu
  return c.text('Webhook reçu', 200);
});

export default app;
```
*Note : La sécurité est cruciale pour les webhooks. Vous devez toujours vérifier la signature du webhook pour authentifier la source et potentiellement implémenter une logique de relecture pour gérer les livraisons en double.*

**Diagramme Mermaid**
```mermaid
sequenceDiagram
    participant Fournisseur[Application Fournisseur]
    participant Consommateur[Application Consommateur (Webhook Listener)]

    Fournisseur->>Fournisseur: 1. Événement se produit (ex: Paiement réussi)
    Fournisseur->>Consommateur: 2. Envoie Webhook (HTTP POST à l'URL de rappel)
    activate Consommateur
    Consommateur->>Consommateur: 3. Valide et traite la charge utile
    Consommateur-->>Fournisseur: 4. Réponse HTTP 200 OK
    deactivate Consommateur

    Note over Fournisseur,Consommateur: Le fournisseur attend une réponse 2xx pour confirmer la réception.
    Note over Fournisseur,Consommateur: En cas d'échec, le fournisseur peut re-tenter l'envoi.
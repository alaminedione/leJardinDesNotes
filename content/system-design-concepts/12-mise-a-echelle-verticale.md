---
title: Mise à l'échelle Verticale
tags:
  - System Design
  - Mise à l'échelle Verticale
draft : false
---

# Mise à l'échelle Verticale (Vertical Scaling)

**Présentation**
La mise à l'échelle verticale, également appelée "scaling up", consiste à augmenter la capacité d'un serveur individuel en lui ajoutant des ressources (CPU, RAM, stockage) pour gérer une charge de travail accrue.

**Principes Clés**
- Augmentation des ressources d'une seule machine.
- Approche simple et rapide pour gérer une augmentation modérée du trafic.
- Limité par la capacité maximale du matériel disponible.
- Peut entraîner un point de défaillance unique (Single Point of Failure - SPOF).

**Limites et Inconvénients**
- **Coût Élevé:** Les serveurs haut de gamme avec beaucoup de ressources sont très coûteux.
- **Limites Matérielles:** Il y a une limite physique à la quantité de CPU, RAM, etc., qu'un seul serveur peut contenir.
- **Point de Défaillance Unique (SPOF):** Si le serveur unique tombe en panne, toute l'application est hors service. Il n'y a pas de redondance.
- **Temps d'Arrêt (Downtime):** L'augmentation des ressources nécessite souvent un arrêt du serveur, ce qui entraîne une interruption de service.
- **Moins de Flexibilité:** Moins adapté aux charges de travail imprévisibles ou très fluctuantes.

**Composants Principaux**
- **Serveur Unique:** La machine dont les ressources sont augmentées.
- **Ressources:** CPU, RAM, Stockage, Bande passante réseau.

**Guides d'utilisation**
La mise à l'échelle verticale est souvent la première approche envisagée pour gérer une charge croissante en raison de sa simplicité. Elle est adaptée aux applications avec une croissance prévisible et modérée, ou comme solution temporaire avant de mettre en œuvre une stratégie de mise à l'échelle horizontale. Cependant, elle atteint rapidement ses limites en termes de coût, de capacité matérielle et de résilience aux pannes.

**Comparaison avec la Mise à l'échelle Horizontale**
| Caractéristique       | Mise à l'échelle Verticale (Scale Up)                               | Mise à l'échelle Horizontale (Scale Out)                               |
| :-------------------- | :------------------------------------------------------------------ | :---------------------------------------------------------------------- |
| **Méthode**           | Ajouter des ressources (CPU, RAM) à un serveur existant.            | Ajouter plus de serveurs (instances) à votre système.                   |
| **Coût**              | Plus coûteux à grande échelle (serveurs haut de gamme).             | Potentiellement moins cher (plusieurs serveurs moins puissants).       |
| **Complexité**        | Plus simple à implémenter initialement.                             | Plus complexe à gérer (répartition de charge, cohérence des données).  |
| **Disponibilité**     | Point de défaillance unique. Nécessite un temps d'arrêt pour les mises à niveau. | Haute disponibilité (redondance). Peut gérer les pannes d'instances.   |
| **Scalabilité**       | Limité par les capacités maximales d'un seul serveur.              | Scalabilité quasi illimitée en ajoutant des nœuds.                     |
| **Cas d'utilisation** | Applications avec charge modérée, bases de données monolithiques.    | Applications web à fort trafic, microservices, Big Data.                |

**Exemples de Code (Hono)**
La mise à l'échelle verticale est une opération d'infrastructure et ne nécessite généralement pas de modifications du code de l'application Hono elle-même. L'application Hono bénéficiera automatiquement des ressources accrues du serveur sous-jacent.

Voici un exemple simple d'une application Hono qui ne nécessite pas de modifications pour bénéficier de la mise à l'échelle verticale :

```typescript
import { Hono } from 'hono';

const app = new Hono();

app.get('/status', (c) => {
  // Cette route renvoie simplement un statut.
  // Ses performances s'amélioreront si le serveur sous-jacent a plus de CPU/RAM.
  return c.text('Service opérationnel');
});

// Une route qui pourrait bénéficier de plus de RAM si elle gère de grandes quantités de données en mémoire
app.post('/process-data', async (c) => {
  const data = await c.req.json();
  // Traitement de données (conceptuel)
  // Si 'data' est très grand, plus de RAM sur le serveur aiderait.
  console.log('Traitement des données...');
  return c.json({ status: 'données traitées', received: data });
});

export default app;
```
*Note : L'impact de la mise à l'échelle verticale sur les performances dépend de la nature de la charge de travail de l'application.*

**Diagramme Mermaid**
```mermaid
graph TD
    A[Serveur Initial] --> B{Ajout de Ressources}
    B --> C[Serveur Plus Puissant]

    subgraph Avant Mise à l'échelle
        Client1(Client) -- Requête --> A
        Client2(Client) -- Requête --> A
    end

    subgraph Après Mise à l'échelle Verticale
        Client3(Client) -- Requête --> C
        Client4(Client) -- Requête --> C
        Client5(Client) -- Requête --> C
        Note right of C: Gère plus de charge
    end
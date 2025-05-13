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

**Composants Principaux**
- **Serveur Unique:** La machine dont les ressources sont augmentées.
- **Ressources:** CPU, RAM, Stockage, Bande passante réseau.

**Guides d'utilisation**
La mise à l'échelle verticale est souvent la première approche envisagée pour gérer une charge croissante en raison de sa simplicité. Elle est adaptée aux applications avec une croissance prévisible et modérée, ou comme solution temporaire avant de mettre en œuvre une stratégie de mise à l'échelle horizontale. Cependant, elle atteint rapidement ses limites en termes de coût, de capacité matérielle et de résilience aux pannes.

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
    Serveur[Serveur Unique]
    Utilisateurs[Utilisateurs]

    Utilisateurs -- Requêtes --> Serveur
    Serveur -- Traite les requêtes --> Serveur

    subgraph "Mise à l'échelle Verticale"
        Serveur -- Ajouter CPU/RAM/Stockage --> Serveur_Plus_Puissant[Serveur Plus Puissant]
    end

    Utilisateurs -- Plus de Requêtes --> Serveur_Plus_Puissant
    Serveur_Plus_Puissant -- Gère plus de requêtes --> Serveur_Plus_Puissant
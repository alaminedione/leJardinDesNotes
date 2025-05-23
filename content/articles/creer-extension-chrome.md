# Créer sa première extension Chrome : Guide complet pour débutants

## Introduction
- Qu'est-ce qu'une extension Chrome et pourquoi en créer une
- Les différents types d'extensions possibles (utilitaires, modificateurs de contenu, extensions de productivité...)
- Prérequis techniques (connaissances basiques en HTML, CSS, JavaScript)
- Ce que nous allons créer dans ce tutoriel : une extension simple qui modifie l'apparence des pages web

## 1. Comprendre la structure d'une extension Chrome

### Les fichiers essentiels
- **manifest.json** : la pierre angulaire de toute extension
- **popup.html/js/css** : l'interface utilisateur qui apparaît quand on clique sur l'icône
- **background.js** : scripts qui s'exécutent en arrière-plan
- **content scripts** : scripts qui interagissent avec les pages web
- **options.html** : page de configuration de l'extension

### Le manifest.json en détail
- Format et structure de base
- Champs obligatoires et optionnels
- Versions du manifest (v2 vs v3) et leurs différences
- Exemple complet commenté d'un manifest.json

## 2. Préparation de l'environnement de développement

### Configuration de base
- Structure des dossiers recommandée
- Outils utiles pour le développement
- Configuration de l'éditeur de code (VSCode, extensions recommandées)

### Mode développeur dans Chrome
- Activation du mode développeur
- Chargement d'une extension non empaquetée
- Outils de débogage des extensions

## 3. Créer une extension simple : "Page Styler"

### Objectif du projet
- Présentation de l'extension "Page Styler" qui permet de modifier les couleurs d'une page web
- Fonctionnalités : changer la couleur de fond, la couleur du texte, et la police d'écriture

### Étape 1 : Création du manifest.json
```json
{
  "manifest_version": 3,
  "name": "Page Styler",
  "version": "1.0",
  "description": "Modifiez l'apparence des pages web",
  "permissions": ["activeTab", "storage"],
  "action": {
    "default_popup": "popup.html",
    "default_icon": {
      "16": "images/icon16.png",
      "48": "images/icon48.png",
      "128": "images/icon128.png"
    }
  },
  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["content.js"]
    }
  ],
  "options_page": "options.html"
}
```

### Étape 2 : Création de l'interface popup
- Structure HTML du popup
- Style CSS pour l'interface
- Fonctionnalités JavaScript pour la popup
- Communication entre popup et content script

### Étape 3 : Développement du content script
- Injection de CSS dans la page
- Manipulation du DOM
- Écouteurs d'événements
- Utilisation de l'API Storage pour sauvegarder les préférences

### Étape 4 : Page d'options
- Interface pour les réglages avancés
- Sauvegarde des préférences utilisateur
- Prévisualisation des changements

## 4. Test et débogage de l'extension

### Méthodes de test
- Rechargement de l'extension
- Utilisation de la console pour le débogage
- Inspection des éléments du popup

### Erreurs courantes et solutions
- Problèmes de permissions
- Erreurs dans le manifest
- Problèmes de communication entre scripts
- Débogage du content script

## 5. Fonctionnalités avancées pour améliorer votre extension

### API Chrome supplémentaires
- `chrome.tabs` pour manipuler les onglets
- `chrome.contextMenus` pour ajouter des options au menu contextuel
- `chrome.alarms` pour planifier des tâches
- `chrome.notifications` pour afficher des notifications

### Stockage persistant
- Différence entre `chrome.storage.sync` et `chrome.storage.local`
- Meilleures pratiques pour stocker les données
- Gestion des données utilisateur

### Sécurité et bonnes pratiques
- Content Security Policy (CSP)
- Cross-Origin Resource Sharing (CORS)
- Isolation des privilèges
- Protection contre les injections XSS

## 6. Préparation au déploiement sur le Chrome Web Store

### Création des assets
- Icônes aux différentes tailles requises
- Captures d'écran pour la fiche du store
- Création d'une bannière promotionnelle
- Préparation de la description et mots-clés

### Empaquetage de l'extension
- Création du fichier .zip
- Vérification finale avant soumission
- Linting et derniers tests

### Processus de soumission
- Création d'un compte développeur Chrome Web Store
- Frais d'enregistrement
- Formulaire de soumission
- Processus de validation et délais estimés

### Monétisation (optionnel)
- Options de monétisation d'une extension
- Modèles économiques possibles
- Intégration de systèmes de paiement

## 7. Cas d'usage avancés et idées d'extensions

### Extensions populaires à analyser
- Exemples d'extensions bien conçues et leur architecture
- Code ouvert à étudier

### Idées de projets pour débutants
- Extension de productivité simple
- Extension de personnalisation
- Extension utilitaire pour développeurs

### Ressources pour continuer à apprendre
- Documentation officielle
- Communautés et forums
- Tutoriels avancés

## Conclusion
- Récapitulatif des concepts clés
- Encouragement à expérimenter
- Prochaines étapes dans le développement d'extensions

## Annexes
- Glossaire des termes techniques
- Référence rapide des API Chrome
- Checklist de déploiement
- Ressources complémentaires

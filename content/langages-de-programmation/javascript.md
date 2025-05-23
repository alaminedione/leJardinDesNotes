---
title: JavaScript
draft: false
tags:
  - javascript
  - programming
description: Langage de script principalement utilisé pour le développement web côté client, mais aussi côté serveur avec Node.js.
---

# JavaScript

## Sommaire

1. Introduction à JavaScript
    * Qu'est-ce que JavaScript ?
    * Historique et évolution (ECMAScript)
    * Environnements d'exécution (Navigateur, Node.js)
2. Bases du Langage
    * Syntaxe de base
    * Variables et types de données (primitifs et objets)
    * Opérateurs
    * Structures de contrôle (conditions, boucles)
    * Fonctions
3. Concepts Avancés
    * Portée (Scope) et Closures
    * Objets et Programmation Orientée Objet (POO)
    * Prototypes et Héritage
    * Asynchronisme (Callbacks, Promises, Async/Await)
    * Modules (CommonJS, ES Modules)
4. Programmation Fonctionnelle
    * Fonctions Pures et Impures
    * Immuabilité
    * Fonctions d'Ordre Supérieur (map, filter, reduce)
5. Manipulation du DOM
    * Accès et modification des éléments HTML
    * Gestion des événements
    * Manipulation des styles CSS
6. Développement Côté Serveur avec Node.js
    * Introduction à Node.js
    * Modules intégrés
    * Gestion des paquets (npm, yarn)
    * Frameworks populaires (Express, NestJS)
7. Frameworks et Bibliothèques Front-end
    * React
    * Angular
    * Vue.js
    * Autres bibliothèques utiles
8. TypeScript
    * Qu'est-ce que TypeScript ?
    * Avantages de TypeScript
    * Intégration avec les frameworks
9. Tests en JavaScript
    * Types de tests (Unitaires, d'intégration, End-to-End)
    * Outils de test (Jest, Mocha, Cypress)
10. Bonnes Pratiques et Patterns
    * Conventions de nommage
    * Gestion des erreurs
    * Patterns de conception courants
11. Design Patterns
    * Singleton Pattern
    * Factory Pattern
    * Observer Pattern
    * Module Pattern
12. Ressources et Communauté
    * Documentation officielle
    * Communautés en ligne
    * Outils de développement

## 1. Introduction à JavaScript

### Qu'est-ce Que JavaScript ?

JavaScript est un langage de script principalement utilisé pour le développement web côté client, mais aussi côté serveur avec Node.js. Il permet d'ajouter de l'interactivité aux pages web, de manipuler le DOM, de gérer les événements et de communiquer avec le serveur.

### Historique Et Évolution (ECMAScript)

* Créé par Brendan Eich chez Netscape en 1995.
* Nommé initialement LiveScript, puis renommé JavaScript pour surfer sur la popularité de Java.
* Standardisé par l'ECMA International sous le nom d'ECMAScript (ES).
* Les versions d'ECMAScript (ES6, ES7, ES8, etc.) apportent régulièrement de nouvelles fonctionnalités au langage.

### Environnements D'exécution (Navigateur, Node.js)

* **Navigateur web** : Environnement d'exécution principal de JavaScript. Permet d'interagir avec le DOM et de gérer les événements utilisateur.
* **Node.js** : Environnement d'exécution JavaScript côté serveur. Permet de développer des applications web complètes (API, serveurs web, etc.).

## 2. Bases Du Langage

### Syntaxe De Base

* Syntaxe inspirée de C, C++ et Java.
* Utilisation de variables, de types de données, d'opérateurs et de structures de contrôle.
* Sensible à la casse (majuscules et minuscules).

```javascript
// Ceci est un commentaire
let nom = "John"; // Déclaration d'une variable
console.log("Hello, " + nom + "!"); // Affichage dans la console
```

### Variables Et Types De Données (primitifs Et objets)

* Types primitifs :
    * `number` : Nombres (entiers et flottants).
    * `string` : Chaînes de caractères.
    * `boolean` : Booléens (true ou false).
    * `null` : Absence de valeur intentionnelle.
    * `undefined` : Variable non initialisée.
    * `symbol` (ES6) : Identificateur unique.
    * `bigint` (ES2020) : Entiers de taille arbitraire.
* Objets :
    * `object` : Collection de propriétés (paires clé-valeur).
    * `array` : Tableau (collection ordonnée d'éléments).
    * `function` : Fonction (bloc de code réutilisable).

```javascript
let age = 30; // number
let nom = "John"; // string
let estValide = true; // boolean
let valeurNull = null; // null
let valeurIndefinie; // undefined

let personne = { // object
    nom: "John",
    age: 30
};

let nombres = [1, 2, 3, 4, 5]; // array

function add(a, b) { // function
    return a + b;
}
```

### Opérateurs

* Arithmétiques : `+`, `-`, `*`, `/`, `%`, `**` (exponentiation)
* Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
* Logiques : `&&`, `||`, `!`
* Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
* Incrémentation/Décrémentation : `++`, `--`
* Comparaison stricte : `===` (valeur et type), `!==`

```javascript
let x = 10;
let y = 5;
let sum = x + y;
let isEqual = (x == y);
let condition = (x > 0 && y < 10);
x++;
```

### Structures De Contrôle (conditions, boucles)

* `if`, `else if`, `else` : Conditionnelles
* `for`, `while`, `do-while` : Boucles
* `switch` : Sélection multiple

```javascript
let score = 85;
if (score > 90) {
    // ...
} else if (score > 80) {
    // ...
} else {
    // ...
}

for (let i = 0; i < 5; i++) {
    // ...
}

while (score > 0) {
    // ...
    score--;
}

switch (score) {
    case 100:
        // ...
        break;
    default:
        // ...
}
```

### Fonctions

* Blocs de code réutilisables.
* Déclaration : `function nomFonction(paramètres) { // corps }`
* Expressions de fonction : `let nomFonction = function(paramètres) { // corps }`
* Fonctions fléchées (ES6) : `(paramètres) => { // corps }`

```javascript
function add(a, b) {
    return a + b;
}

let multiply = function(a, b) {
    return a * b;
}

let square = (x) => {
    return x * x;
}

console.log(add(5, 3));
console.log(multiply(5, 3));
console.log(square(5));
```

## 3. Concepts Avancés

### Portée (Scope) Et Closures

* **Portée (Scope)** : Détermine la visibilité des variables.
    * Portée globale : Variables déclarées en dehors de toute fonction.
    * Portée locale : Variables déclarées à l'intérieur d'une fonction.
    * Portée de bloc (ES6) : Variables déclarées avec `let` et `const` sont limitées au bloc dans lequel elles sont définies.
* **Closures** : Une fonction qui "se souvient" des variables de son environnement lexical, même après que la fonction extérieure a été exécutée.

```javascript
let globalVariable = "Global";

function maFonction() {
    let localVariable = "Local";
    console.log(globalVariable); // Accessible
    console.log(localVariable); // Accessible

    function maFonctionInterne() {
        console.log(globalVariable); // Accessible
        console.log(localVariable); // Accessible (closure)
    }

    maFonctionInterne();
}

maFonction();
console.log(globalVariable); // Accessible
// console.log(localVariable); // Erreur : non définie
```

### Objets Et Programmation Orientée Objet (POO)

* JavaScript est un langage basé sur les prototypes, mais il supporte les concepts de la POO.
* Création d'objets avec des littéraux d'objet ou avec des constructeurs.
* Classes (ES6) : Syntaxe plus proche des langages POO classiques.

```javascript
// Littéral d'objet
let personne = {
    nom: "John",
    age: 30,
    direBonjour: function() {
        console.log("Bonjour, je suis " + this.nom);
    }
};

personne.direBonjour();

// Constructeur
function Personne(nom, age) {
    this.nom = nom;
    this.age = age;
    this.direBonjour = function() {
        console.log("Bonjour, je suis " + this.nom);
    }
}

let personne2 = new Personne("Jane", 25);
personne2.direBonjour();

// Classe (ES6)
class Animal {
    constructor(nom) {
        this.nom = nom;
    }

    faireDuBruit() {
        console.log("Bruit générique");
    }
}

let animal = new Animal("Animal");
animal.faireDuBruit();
```

### Prototypes Et Héritage

* En JavaScript, les objets héritent des propriétés et des méthodes de leur prototype.
* Le prototype est un autre objet.
* Possibilité de modifier le prototype d'un objet pour ajouter ou modifier des fonctionnalités.

```javascript
function Animal(nom) {
    this.nom = nom;
}

Animal.prototype.faireDuBruit = function() {
    console.log("Bruit générique");
}

function Chien(nom) {
    Animal.call(this, nom); // Héritage
}

Chien.prototype = Object.create(Animal.prototype); // Héritage

Chien.prototype.faireDuBruit = function() {
    console.log("Woof!");
}

let chien = new Chien("Fido");
chien.faireDuBruit();
```

### Asynchronisme (Callbacks, Promises, Async/Await)

* JavaScript est un langage asynchrone et non bloquant.
* **Callbacks** : Fonctions passées en argument à d'autres fonctions et exécutées une fois l'opération terminée.
* **Promises** : Objets représentant une valeur qui peut être disponible maintenant, dans le futur ou jamais.
* **Async/Await** (ES8) : Syntaxe plus simple pour gérer les opérations asynchrones.

```javascript
// Callbacks
function telechargerDonnees(url, callback) {
    // ...
    callback(donnees);
}

telechargerDonnees("https://www.example.com/data", function(data) {
    console.log("Données téléchargées:", data);
});

// Promises
function telechargerDonnees2(url) {
    return new Promise(function(resolve, reject) {
        // ...
        resolve(donnees);
        // reject(erreur);
    });
}

telechargerDonnees2("https://www.example.com/data")
    .then(function(data) {
        console.log("Données téléchargées:", data);
    })
    .catch(function(erreur) {
        console.error("Erreur:", erreur);
    });

// Async/Await
async function afficherDonnees() {
    try {
        let data = await telechargerDonnees2("https://www.example.com/data");
        console.log("Données téléchargées:", data);
    } catch (erreur) {
        console.error("Erreur:", erreur);
    }
}

afficherDonnees();
```

### Modules (CommonJS, ES Modules)

* Les modules permettent d'organiser le code en fichiers séparés et de réutiliser le code.
* **CommonJS** : Système de modules utilisé par Node.js (utilisation de `require` et `module.exports`).
* **ES Modules** (ES6) : Système de modules standardisé (utilisation de `import` et `export`).

```javascript
// CommonJS (Node.js)
// module.js
module.exports = {
    maVariable: "Hello",
    maFonction: function() {
        console.log("Hello!");
    }
};

// main.js
const module = require('./module');
console.log(module.maVariable);
module.maFonction();

// ES Modules
// module.js
export const maVariable = "Hello";
export function maFonction() {
    console.log("Hello!");
}

// main.js
import { maVariable, maFonction } from './module.js';
console.log(maVariable);
maFonction();
```

## 4. Programmation Fonctionnelle

### Fonctions Pures Et Impures

* **Fonction Pure** : Une fonction qui, étant donné les mêmes entrées, retourne toujours les mêmes sorties et n'a pas d'effets secondaires (ne modifie pas l'état en dehors de son scope).
    * Facile à tester et à raisonner.
    * Exemple : `function add(a, b) { return a + b; }`
* **Fonction Impure** : Une fonction qui peut avoir des effets secondaires (modifie l'état global, effectue des I/O, etc.) ou dont la sortie dépend de facteurs externes.
    * Plus difficile à tester et à déboguer.
    * Exemple : `console.log()`, `Math.random()`, modification d'une variable globale.

```javascript
// Fonction pure
function multiplier(a, b) {
    return a * b;
}

// Fonction impure (modifie une variable globale)
let total = 0;
function ajouterAuTotal(valeur) {
    total += valeur;
    return total;
}

console.log(multiplier(2, 3)); // 6
console.log(ajouterAuTotal(5)); // 5
console.log(ajouterAuTotal(10)); // 15
```

### Immuabilité

* Le concept d'immuabilité signifie qu'une fois qu'une donnée est créée, elle ne peut pas être modifiée. Au lieu de modifier une donnée existante, on crée une nouvelle donnée avec les modifications.
* Avantages : Prévient les effets secondaires inattendus, facilite le débogage, améliore la prévisibilité du code.
* Méthodes pour l'immuabilité : `Object.assign()`, spread operator (`…`), `Array.prototype.slice()`, `Array.prototype.map()`, `Array.prototype.filter()`.

```javascript
// Objet mutable
let personneMutable = { nom: "Alice", age: 30 };
personneMutable.age = 31; // Modification directe

// Objet immutable (avec spread operator)
let personneImmutable = { nom: "Bob", age: 25 };
let nouvellePersonne = { ...personneImmutable, age: 26 }; // Crée un nouvel objet

console.log(personneImmutable); // { nom: "Bob", age: 25 }
console.log(nouvellePersonne); // { nom: "Bob", age: 26 }

// Tableau mutable
let nombresMutables = [1, 2, 3];
nombresMutables.push(4); // Modification directe

// Tableau immutable (avec spread operator)
let nombresImmutables = [1, 2, 3];
let nouveauxNombres = [...nombresImmutables, 4]; // Crée un nouveau tableau

console.log(nombresMutables); // [1, 2, 3, 4]
console.log(nombresImmutables); // [1, 2, 3]
console.log(nouveauxNombres); // [1, 2, 3, 4]
```

### Fonctions D'ordre Supérieur (map, Filter, reduce)

* Une fonction d'ordre supérieur est une fonction qui prend une ou plusieurs fonctions en argument, ou qui retourne une fonction.
* **`map()`** : Crée un nouveau tableau en appelant une fonction fournie sur chaque élément du tableau appelant.
* **`filter()`** : Crée un nouveau tableau avec tous les éléments qui passent le test implémenté par la fonction fournie.
* **`reduce()`** : Exécute une fonction de "réducteur" (fournie par l'utilisateur) sur chaque élément du tableau, de gauche à droite, afin de réduire le tableau à une seule valeur.

```javascript
const chiffres = [1, 2, 3, 4, 5];

// map : Doubler chaque chiffre
const chiffresDoubles = chiffres.map(chiffre => chiffre * 2);
console.log(chiffresDoubles); // [2, 4, 6, 8, 10]

// filter : Garder seulement les chiffres pairs
const chiffresPairs = chiffres.filter(chiffre => chiffre % 2 === 0);
console.log(chiffresPairs); // [2, 4]

// reduce : Somme de tous les chiffres
const sommeChiffres = chiffres.reduce((accumulateur, chiffre) => accumulateur + chiffre, 0);
console.log(sommeChiffres); // 15
```

## 5. Manipulation Du DOM

### Accès Et Modification Des Éléments HTML

* Le DOM (Document Object Model) est une représentation arborescente du document HTML.
* JavaScript permet d'accéder et de modifier les éléments HTML via le DOM.
* Méthodes courantes :
    * `document.getElementById()` : Sélectionne un élément par son ID.
    * `document.querySelector()` : Sélectionne le premier élément correspondant à un sélecteur CSS.
    * `document.querySelectorAll()` : Sélectionne tous les éléments correspondant à un sélecteur CSS.
    * `element.innerHTML` : Modifie le contenu HTML d'un élément.
    * `element.textContent` : Modifie le contenu textuel d'un élément.
    * `element.setAttribute()` : Modifie un attribut d'un élément.

```javascript
// Accès à un élément par son ID
let titre = document.getElementById("monTitre");

// Accès à un élément par son sélecteur CSS
let paragraphe = document.querySelector("p");

// Modification du contenu HTML
titre.innerHTML = "Nouveau titre";

// Modification du contenu textuel
paragraphe.textContent = "Nouveau paragraphe";

// Modification d'un attribut
let image = document.querySelector("img");
image.setAttribute("src", "nouvelle_image.jpg");
```

### Gestion Des Événements

* JavaScript permet de réagir aux événements utilisateur (clic, survol, soumission de formulaire, etc.).
* Méthodes courantes :
    * `element.addEventListener()` : Attache un gestionnaire d'événements à un élément.

```javascript
let bouton = document.getElementById("monBouton");

bouton.addEventListener("click", function() {
    alert("Bouton cliqué!");
});
```

### Manipulation Des Styles CSS

* JavaScript permet de modifier les styles CSS des éléments HTML.
* Méthodes courantes :
    * `element.style.proprieteCSS` : Modifie une propriété CSS directement.
    * `element.classList.add()` : Ajoute une classe CSS à un élément.
    * `element.classList.remove()` : Supprime une classe CSS d'un élément.

```javascript
let titre = document.getElementById("monTitre");

// Modification directe du style
titre.style.color = "red";

// Ajout d'une classe CSS
titre.classList.add("highlight");

// Suppression d'une classe CSS
titre.classList.remove("highlight");
```

## 5. Développement Côté Serveur Avec Node.js

### Introduction à Node.js

* Node.js est un environnement d'exécution JavaScript côté serveur.
* Permet d'utiliser JavaScript pour développer des applications web complètes (API, serveurs web, etc.).
* Basé sur le moteur JavaScript V8 de Chrome.
* Non bloquant et orienté événements.

### Modules Intégrés

* Node.js fournit de nombreux modules intégrés pour effectuer des opérations courantes (ex: `fs` pour manipuler les fichiers, `http` pour créer des serveurs web).

```javascript
const fs = require('fs'); // Module pour manipuler les fichiers

fs.readFile('monfichier.txt', 'utf8', function(err, data) {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data);
});
```

### Gestion Des Paquets (npm, yarn)

* **npm (Node Package Manager)** : Gestionnaire de paquets par défaut pour Node.js.
* **yarn** : Autre gestionnaire de paquets populaire, offrant des performances améliorées.

```bash
# Installation d'un paquet avec npm
npm install nom_du_paquet

# Installation d'un paquet avec yarn
yarn add nom_du_paquet
```

### Frameworks Populaires (Express, NestJS)

* **Express** : Framework web minimaliste et flexible pour Node.js.
* **NestJS** : Framework pour construire des applications serveur efficaces et évolutives (inspiré par Angular).

## 6. Frameworks Et Bibliothèques Front-end

### React

* Bibliothèque JavaScript pour construire des interfaces utilisateur.
* Basée sur les composants.
* Utilisation de JSX (syntaxe combinant HTML et JavaScript).
* Gestion de l'état avec des composants stateful ou avec des outils comme Redux ou Context API.

### Angular

* Framework complet pour construire des applications web complexes.
* Basé sur TypeScript.
* Utilisation de composants, de services et de modules.
* Fournit une structure robuste et des outils pour le développement d'applications à grande échelle.

### Vue.js

* Framework progressif pour construire des interfaces utilisateur.
* Facile à apprendre et à intégrer dans des projets existants.
* Basé sur les composants.
* Offre une grande flexibilité et une courbe d'apprentissage douce.

### Autres Bibliothèques Utiles

* jQuery : Bibliothèque pour simplifier la manipulation du DOM (bien que moins utilisée aujourd'hui).
* Lodash : Bibliothèque d'utilitaires pour manipuler les tableaux, les objets et les chaînes de caractères.

## 7. TypeScript

### Qu'est-ce Que TypeScript ?

* TypeScript est un sur-ensemble typé de JavaScript qui compile en JavaScript simple.
* Développé et maintenu par Microsoft.
* Apporte le typage statique optionnel, ce qui permet de détecter les erreurs de type au moment de la compilation plutôt qu'à l'exécution.
* Améliore la maintenabilité du code, la lisibilité et la collaboration sur de grands projets.
* Offre des fonctionnalités avancées comme les interfaces, les types génériques, les décorateurs, etc.

```typescript
// Déclaration de variables avec types
let nom: string = "Alice";
let age: number = 30;
let estActif: boolean = true;

// Fonctions avec types de paramètres et de retour
function saluer(prenom: string): string {
    return `Bonjour, ${prenom}!`;
}

console.log(saluer("Bob"));

// Interfaces pour définir la forme des objets
interface Utilisateur {
    id: number;
    nom: string;
    email?: string; // Propriété optionnelle
}

const utilisateur1: Utilisateur = {
    id: 1,
    nom: "Charlie"
};

const utilisateur2: Utilisateur = {
    id: 2,
    nom: "David",
    email: "david@example.com"
};

// Classes avec types
class Point {
    x: number;
    y: number;

    constructor(x: number, y: number) {
        this.x = x;
        this.y = y;
    }

    getDistance(): number {
        return Math.sqrt(this.x ** 2 + this.y ** 2);
    }
}

const p = new Point(3, 4);
console.log(p.getDistance());
```

### Avantages De TypeScript

* **Détection précoce des erreurs** : Les erreurs de type sont détectées avant l'exécution, réduisant les bugs en production.
* **Meilleure maintenabilité** : Le code est plus facile à comprendre et à modifier grâce aux types explicites.
* **Amélioration de l'IDE** : Les éditeurs de code offrent une meilleure auto-complétion, refactoring et navigation.
* **Code plus robuste** : Les types aident à écrire du code plus fiable et moins sujet aux erreurs.
* **Évolutivité** : Idéal pour les grands projets et les équipes importantes.

### Intégration Avec Les Frameworks

* TypeScript est largement adopté par les frameworks front-end modernes comme Angular (qui l'utilise par défaut), React et Vue.js.
* Il est également très utilisé dans l'écosystème Node.js, notamment avec des frameworks comme NestJS.

## 8. Tests En JavaScript

### Types De Tests (Unitaires, D'intégration, End-to-End)

* **Tests unitaires** : Vérifient le comportement d'une fonction ou d'un composant individuel.
* **Tests d'intégration** : Vérifient l'interaction entre plusieurs unités de code.
* **Tests End-to-End (E2E)** : Vérifient le fonctionnement de l'application de bout en bout, en simulant le comportement d'un utilisateur réel.

### Outils De Test (Jest, Mocha, Cypress)

* **Jest** : Framework de test développé par Facebook, simple à configurer et offrant de nombreuses fonctionnalités (mocking, couverture de code, etc.).
* **Mocha** : Framework de test flexible et extensible, nécessitant l'installation de bibliothèques supplémentaires (ex: Chai pour les assertions, Sinon pour le mocking).
* **Cypress** : Framework de test E2E pour tester les applications web dans un navigateur réel.

## 9. Bonnes Pratiques Et Patterns

### Conventions De Nommage

* Utiliser le camelCase pour les noms de variables et de fonctions.
* Utiliser des noms clairs et descriptifs.
* Utiliser des noms courts pour les variables locales.
* Utiliser des noms longs pour les variables globales.
* Préfixer les constantes avec `const` et utiliser des noms en majuscules (ex: `const PI = 3.14`).

### Gestion Des Erreurs

* Utiliser les blocs `try…catch` pour gérer les exceptions.
* Afficher des messages d'erreur clairs et informatifs.
* Utiliser des outils de débogage pour identifier et corriger les erreurs.

### Patterns De Conception Courants

* Module Pattern
* Observer Pattern
* Factory Pattern

## 11. Design Patterns

Les Design Patterns sont des solutions réutilisables à des problèmes courants en conception logicielle. Ils ne sont pas des bibliothèques ou des frameworks, mais des modèles que l'on peut adapter à ses propres besoins.

### Singleton Pattern

* Garantit qu'une classe n'a qu'une seule instance et fournit un point d'accès global à cette instance.
* Utile pour la gestion de configurations, de bases de données, ou de ressources partagées.

```javascript
const Singleton = (function () {
    let instance;

    function createInstance() {
        const object = new Object("Je suis l'instance unique");
        return object;
    }

    return {
        getInstance: function () {
            if (!instance) {
                instance = createInstance();
            }
            return instance;
        }
    };
})();

const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();

console.log(instance1 === instance2); // true
```

### Factory Pattern

* Fournit une interface pour créer des objets dans une superclasse, mais permet aux sous-classes de modifier le type d'objets qui seront créés.
* Utile lorsque le processus de création d'objets est complexe ou dépend de conditions.

```javascript
class Voiture {
    constructor(options) {
        this.portes = options.portes || 4;
        this.couleur = options.couleur || "noir";
    }
}

class Camion {
    constructor(options) {
        this.roues = options.roues || 6;
        this.chargeMax = options.chargeMax || "10 tonnes";
    }
}

class VehiculeFactory {
    creerVehicule(type, options) {
        switch (type) {
            case "voiture":
                return new Voiture(options);
            case "camion":
                return new Camion(options);
            default:
                return null;
        }
    }
}

const factory = new VehiculeFactory();
const maVoiture = factory.creerVehicule("voiture", { couleur: "rouge" });
const monCamion = factory.creerVehicule("camion", { roues: 8 });

console.log(maVoiture); // Voiture { portes: 4, couleur: 'rouge' }
console.log(monCamion); // Camion { roues: 8, chargeMax: '10 tonnes' }
```

### Observer Pattern

* Définit une dépendance un-à-plusieurs entre des objets, de sorte que lorsqu'un objet change d'état, tous ses dépendants sont avertis et mis à jour automatiquement.
* Utile pour la gestion d'événements, les systèmes de notification, ou les architectures réactives.

```javascript
class Sujet {
    constructor() {
        this.observateurs = [];
    }

    ajouterObservateur(observateur) {
        this.observateurs.push(observateur);
    }

    notifier(donnees) {
        this.observateurs.forEach(observateur => observateur.miseAJour(donnees));
    }
}

class Observateur {
    constructor(nom) {
        this.nom = nom;
    }

    miseAJour(donnees) {
        console.log(`${this.nom} a reçu la mise à jour: ${donnees}`);
    }
}

const sujet = new Sujet();
const obs1 = new Observateur("Observateur 1");
const obs2 = new Observateur("Observateur 2");

sujet.ajouterObservateur(obs1);
sujet.ajouterObservateur(obs2);

sujet.notifier("Nouvelles données disponibles !");
// Observateur 1 a reçu la mise à jour: Nouvelles données disponibles !
// Observateur 2 a reçu la mise à jour: Nouvelles données disponibles !
```

### Module Pattern

* Permet d'encapsuler des variables et des fonctions privées, exposant uniquement une interface publique.
* Utile pour organiser le code, éviter les collisions de noms dans l'espace global et créer des modules réutilisables.

```javascript
const MonModule = (function () {
    let privateVariable = "Je suis privé";

    function privateMethod() {
        console.log(privateVariable);
    }

    return {
        publicMethod: function () {
            console.log("Je suis une méthode publique.");
            privateMethod();
        },
        publicVariable: "Je suis public"
    };
})();

MonModule.publicMethod(); // Je suis une méthode publique. \n Je suis privé
console.log(MonModule.publicVariable); // Je suis public
// console.log(MonModule.privateVariable); // undefined (non accessible)
```

## 12. Ressources Et Communauté

### Documentation Officielle

* [MDN Web Docs JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript)

### Communautés En Ligne

* [Stack Overflow](https://stackoverflow.com/)
* [Reddit (r/javascript)](https://www.reddit.com/r/javascript/)

### Outils De Développement

* Navigateurs web avec outils de développement intégrés (Chrome DevTools, Firefox Developer Tools).
* Éditeurs de code (VS Code, Sublime Text, Atom).

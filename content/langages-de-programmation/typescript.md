---
title: TypeScript
draft: false
tags:
  - typescript
  - programming
description: Sur-ensemble typé de JavaScript qui compile en JavaScript simple.
---

## Sommaire

1.  Introduction à TypeScript
    *   Qu'est-ce que TypeScript ?
    *   Pourquoi utiliser TypeScript ?
    *   Installation et configuration
    *   Compilation (tsc)
2.  Bases du Langage
    *   Types primitifs (string, number, boolean, null, undefined, symbol, bigint)
    *   Annotations de type
    *   Inférence de type
    *   Variables et constantes
    *   Opérateurs
    *   Structures de contrôle
    *   Fonctions
3.  Types Avancés
    *   Tableaux et Tuples
    *   Enums
    *   Any, Unknown, Void, Never
    *   Union Types et Intersection Types
    *   Alias de type
4.  Interfaces
    *   Déclaration et utilisation des interfaces
    *   Interfaces pour les objets, fonctions, classes
    *   Extension d'interfaces
5.  Classes
    *   Déclaration et utilisation des classes
    *   Modificateurs d'accès (public, private, protected)
    *   Héritage
    *   Classes abstraites
6.  Génériques (Generics)
    *   Fonctions génériques
    *   Interfaces génériques
    *   Classes génériques
    *   Contraintes de type
7.  Modules
    *   Import et Export
    *   Espaces de noms (Namespaces)
8.  Décorateurs
    *   Utilisation des décorateurs
    *   Création de décorateurs
9.  Configuration du Compilateur (tsconfig.json)
    *   Options courantes
    *   Inclusion et exclusion de fichiers
10. Intégration avec des Frameworks JavaScript
    *   React, Angular, Vue.js
    *   Node.js
11. Tests en TypeScript
    *   Utilisation d'outils de test JavaScript (Jest, Mocha) avec TypeScript
12. Bonnes Pratiques
    *   Conventions de nommage
    *   Gestion des erreurs
    *   Utilisation stricte des types
13. Ressources et Communauté
    *   Documentation officielle
    *   Communautés en ligne
## 1. Introduction à TypeScript

### Qu'est-ce que TypeScript ?

TypeScript est un sur-ensemble typé de JavaScript qui compile en JavaScript simple. Il ajoute des fonctionnalités de typage statique, de classes et d'interfaces à JavaScript, ce qui permet de développer des applications plus robustes et maintenables.

### Pourquoi utiliser TypeScript ?

*   **Typage statique** : Détection des erreurs de type à la compilation, ce qui réduit les erreurs à l'exécution.
*   **Meilleure maintenabilité** : Le typage statique facilite la compréhension et la refactorisation du code.
*   **Productivité accrue** : L'autocomplétion et la vérification de type améliorent la productivité des développeurs.
*   **Compatibilité avec JavaScript** : TypeScript compile en JavaScript simple, ce qui le rend compatible avec tous les navigateurs et environnements JavaScript.

### Installation et configuration

1.  Installer Node.js et npm.
2.  Installer TypeScript globalement avec npm : `npm install -g typescript`.

### Compilation (tsc)

*   Utilisation du compilateur `tsc` pour compiler les fichiers TypeScript (`.ts`) en fichiers JavaScript (`.js`).
*   Commande de base : `tsc nom_fichier.ts`.

```bash
tsc mon_fichier.ts
```

## 2. Bases du Langage

### Types primitifs (string, number, boolean, null, undefined, symbol, bigint)

*   `string` : Chaînes de caractères.
*   `number` : Nombres (entiers et flottants).
*   `boolean` : Booléens (true ou false).
*   `null` : Absence de valeur intentionnelle.
*   `undefined` : Variable non initialisée.
*   `symbol` (ES6) : Identificateur unique.
*   `bigint` (ES2020) : Entiers de taille arbitraire.

```typescript
let nom: string = "John";
let age: number = 30;
let estValide: boolean = true;
let valeurNull: null = null;
let valeurIndefinie: undefined = undefined;
let symbole: symbol = Symbol("description");
let grandNombre: bigint = 12345678901234567890n;
```

### Annotations de type

*   Permettent de spécifier le type d'une variable, d'un paramètre de fonction ou d'une valeur de retour.
*   Syntaxe : `nom_variable: type`.

```typescript
let nom: string = "John";
function add(a: number, b: number): number {
    return a + b;
}
```

### Inférence de type

*   TypeScript peut inférer le type d'une variable à partir de sa valeur initiale.

```typescript
let age = 30; // TypeScript infère que age est de type number
```

### Variables et constantes

*   `let` : Déclare une variable avec une portée de bloc.
*   `const` : Déclare une constante (valeur non modifiable).
*   `var` : Déclare une variable avec une portée de fonction (à éviter).

```typescript
let age = 30;
const PI = 3.14159;
```

### Opérateurs

*   Arithmétiques : `+`, `-`, `*`, `/`, `%`, `**` (exponentiation)
*   Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
*   Logiques : `&&`, `||`, `!`
*   Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
*   Incrémentation/Décrémentation : `++`, `--`
*   Comparaison stricte : `===` (valeur et type), `!==`

```typescript
let x = 10;
let y = 5;
let sum = x + y;
let isEqual = (x == y);
let condition = (x > 0 && y < 10);
x++;
```

### Structures de contrôle

*   `if`, `else if`, `else` : Conditionnelles
*   `for`, `while`, `do-while` : Boucles
*   `switch` : Sélection multiple

```typescript
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

*   Blocs de code réutilisables.
*   Déclaration : `function nomFonction(paramètres: type): type_retour { // corps }`
*   Fonctions fléchées : `(paramètres: type) => type_retour { // corps }`

```typescript
function add(a: number, b: number): number {
    return a + b;
}

let multiply = (a: number, b: number): number => {
    return a * b;
}

console.log(add(5, 3));
console.log(multiply(5, 3));
```
## 3. Types Avancés

### Tableaux et Tuples

*   **Tableaux** : Collections ordonnées d'éléments du même type.
*   **Tuples** : Collections ordonnées d'éléments de types différents (taille fixe).

```typescript
let nombres: number[] = [1, 2, 3, 4, 5];
let personnes: string[] = ["Alice", "Bob", "Charlie"];

let coordonnees: [number, number] = [10, 20]; // Tuple
let personne: [string, number] = ["John", 30];
```

### Enums

*   Permettent de définir un ensemble de constantes nommées.

```typescript
enum Couleur {
    Rouge,
    Vert,
    Bleu
}

let couleurPreferee: Couleur = Couleur.Bleu;
```

### Any, Unknown, Void, Never

*   `any` : Type dynamique (désactive la vérification de type).  À éviter autant que possible.
*   `unknown` : Type sûr pour représenter une valeur inconnue (nécessite un cast avant utilisation).
*   `void` : Indique qu'une fonction ne retourne aucune valeur.
*   `never` : Indique qu'une fonction ne termine jamais son exécution (ex: boucle infinie, exception).

```typescript
let valeur: any = 10;
valeur = "Hello";

let valeurInconnue: unknown = "World";
// let longueur: number = valeurInconnue.length; // Erreur
let longueur: number = (valeurInconnue as string).length; // Cast

function afficherMessage(): void {
    console.log("Message");
}

function erreur(): never {
    throw new Error("Erreur");
}
```

### Union Types et Intersection Types

*   **Union Types** : Permettent de spécifier qu'une variable peut avoir plusieurs types possibles.
*   **Intersection Types** : Permettent de combiner plusieurs types en un seul.

```typescript
let resultat: string | number = "Hello";
resultat = 10;

interface A {
    a: number;
}

interface B {
    b: string;
}

type C = A & B; // Intersection type

let c: C = {
    a: 10,
    b: "Hello"
};
```

### Alias de type

*   Permettent de donner un nom à un type existant.

```typescript
type Chaine = string;
let nom: Chaine = "John";

type Coordonnees = [number, number];
let point: Coordonnees = [10, 20];
```
## 4. Interfaces

### Déclaration et utilisation des interfaces

*   Une interface définit un contrat pour les objets, les fonctions et les classes.
*   Elle spécifie les propriétés et les méthodes qu'un objet doit implémenter.

```typescript
interface Personne {
    nom: string;
    age: number;
    direBonjour(): void;
}

let personne: Personne = {
    nom: "John",
    age: 30,
    direBonjour: function() {
        console.log("Bonjour, je suis " + this.nom);
    }
};
```

### Interfaces pour les objets, fonctions, classes

*   Les interfaces peuvent être utilisées pour définir la structure des objets, des fonctions et des classes.

```typescript
// Interface pour un objet
interface Point {
    x: number;
    y: number;
}

// Interface pour une fonction
interface AddFunction {
    (a: number, b: number): number;
}

let add: AddFunction = function(a: number, b: number): number {
    return a + b;
}

// Interface pour une classe
interface Animal {
    nom: string;
    faireDuBruit(): void;
}

class Chien implements Animal {
    nom: string;

    constructor(nom: string) {
        this.nom = nom;
    }

    faireDuBruit(): void {
        console.log("Woof!");
    }
}
```

### Extension d'interfaces

*   Une interface peut hériter des propriétés et des méthodes d'une autre interface.

```typescript
interface A {
    a: number;
}

interface B extends A {
    b: string;
}

let b: B = {
    a: 10,
    b: "Hello"
};
```
## 5. Classes

### Déclaration et utilisation des classes

*   Utilisation du mot-clé `class` pour définir une classe.
*   Constructeur : méthode spéciale `constructor`.
*   Utilisation du mot-clé `this` pour référencer l'objet courant.

```typescript
class Personne {
    nom: string;
    age: number;

    constructor(nom: string, age: number) {
        this.nom = nom;
        this.age = age;
    }

    direBonjour(): void {
        console.log("Bonjour, je suis " + this.nom);
    }
}

let personne = new Personne("John", 30);
personne.direBonjour();
```

### Modificateurs d'accès (public, private, protected)

*   `public` : Accessible depuis n'importe où (par défaut).
*   `private` : Accessible uniquement depuis la classe où il est défini.
*   `protected` : Accessible depuis la classe où il est défini et depuis ses sous-classes.

```typescript
class MaClasse {
    public attributPublic: string = "Public";
    private attributPrive: string = "Prive";
    protected attributProtege: string = "Protege";

    public afficherAttributs(): void {
        console.log(this.attributPublic);
        console.log(this.attributPrive);
        console.log(this.attributProtege);
    }
}

let obj = new MaClasse();
console.log(obj.attributPublic); // Accessible
// console.log(obj.attributPrive); // Erreur : non accessible
```

### Héritage

*   Permet à une classe (sous-classe) d'hériter des propriétés et des méthodes d'une autre classe (super-classe).
*   Utilisation du mot-clé `extends`.

```typescript
class Animal {
    nom: string;

    constructor(nom: string) {
        this.nom = nom;
    }

    faireDuBruit(): void {
        console.log("Bruit générique");
    }
}

class Chien extends Animal {
    faireDuBruit(): void {
        console.log("Woof!");
    }
}

let chien = new Chien("Fido");
chien.faireDuBruit(); // Woof!
```

### Classes abstraites

*   Une classe abstraite ne peut pas être instanciée directement.
*   Elle peut contenir des méthodes abstraites (sans implémentation).
*   Les classes qui héritent d'une classe abstraite doivent implémenter toutes ses méthodes abstraites.

```typescript
abstract class Forme {
    abstract calculerAire(): number;
}

class Cercle extends Forme {
    rayon: number;

    constructor(rayon: number) {
        super();
        this.rayon = rayon
    }
    calculerAire(): number {
        return Math.PI * this.rayon * this.rayon;
    }
}
```
## 6. Génériques (Generics)

### Fonctions génériques

*   Les génériques permettent d'écrire des fonctions qui peuvent fonctionner avec différents types de données.
*   Utilisation de la syntaxe `<T>` pour définir un type générique.

```typescript
function identite<T>(arg: T): T {
    return arg;
}

let valeurString: string = identite<string>("Hello");
let valeurNombre: number = identite<number>(10);
```

### Interfaces génériques

*   Les interfaces génériques permettent de définir des interfaces qui peuvent fonctionner avec différents types de données.

```typescript
interface Resultat<T> {
    valeur: T;
    succes: boolean;
}

let resultatString: Resultat<string> = {
    valeur: "Hello",
    succes: true
};

let resultatNombre: Resultat<number> = {
    valeur: 10,
    succes: false
};
```

### Classes génériques

*   Les classes génériques permettent de définir des classes qui peuvent fonctionner avec différents types de données.

```typescript
class Boite<T> {
    valeur: T;

    constructor(valeur: T) {
        this.valeur = valeur;
    }

    getValeur(): T {
        return this.valeur;
    }
}

let boiteString = new Boite<string>("Hello");
let boiteNombre = new Boite<number>(10);
```

### Contraintes de type

*   Permettent de limiter les types de données qui peuvent être utilisés avec un générique.

```typescript
interface AvecLongueur {
    length: number;
}

function afficherLongueur<T extends AvecLongueur>(arg: T): number {
    return arg.length;
}

console.log(afficherLongueur("Hello")); // 5
// console.log(afficherLongueur(10)); // Erreur : number n'a pas de propriété length
```
## 7. Modules

### Import et Export

*   Les modules permettent d'organiser le code en fichiers séparés et de réutiliser le code.
*   Utilisation des mots-clés `import` et `export`.

```typescript
// module.ts
export interface Personne {
    nom: string;
    age: number;
}

export function direBonjour(personne: Personne): void {
    console.log("Bonjour, " + personne.nom);
}

// main.ts
import { Personne, direBonjour } from "./module";

let personne: Personne = {
    nom: "John",
    age: 30
};

direBonjour(personne);
```

### Espaces de noms (Namespaces)

*   Les espaces de noms permettent d'organiser le code en groupes logiques (dépréciés au profit des modules).

```typescript
namespace MonEspaceDeNom {
    export interface MaInterface {
        // ...
    }
}
```
## 8. Décorateurs

### Utilisation des décorateurs

*   Les décorateurs sont des fonctions qui modifient le comportement des classes, des méthodes, des propriétés ou des paramètres.
*   Utilisation de la syntaxe `@decorateur` pour appliquer un décorateur.

### Création de décorateurs

```typescript
function log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;

    descriptor.value = function(...args: any[]) {
        console.log("Appel de " + propertyKey + " avec les arguments: " + JSON.stringify(args));
        const result = originalMethod.apply(this, args);
        console.log("Résultat: " + result);
        return result;
    };
}

class MaClasse {
    @log
    add(a: number, b: number): number {
        return a + b;
    }
}

let obj = new MaClasse();
obj.add(5, 3);
```
## 9. Configuration du Compilateur (tsconfig.json)

### Options courantes

*   `compilerOptions` :
    *   `target` : Version de JavaScript cible (ex: "ES5", "ES6", "ESNext").
    *   `module` : Système de modules utilisé (ex: "CommonJS", "ESNext").
    *   `outDir` : Répertoire de sortie pour les fichiers JavaScript compilés.
    *   `rootDir` : Répertoire racine des fichiers TypeScript.
    *   `sourceMap` : Génère des fichiers source map pour faciliter le débogage.
    *   `strict` : Active toutes les options de vérification de type strict.
    *   `esModuleInterop` : Permet d'importer des modules CommonJS comme des modules ES.

### Inclusion et exclusion de fichiers

*   `include` : Liste des fichiers ou des motifs de fichiers à inclure dans la compilation.
*   `exclude` : Liste des fichiers ou des motifs de fichiers à exclure de la compilation.

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "outDir": "./dist",
    "rootDir": "./src",
    "sourceMap": true,
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```
## 10. Intégration avec des Frameworks JavaScript

### React, Angular, Vue.js

*   TypeScript peut être utilisé avec les frameworks JavaScript populaires tels que React, Angular et Vue.js.
*   Des définitions de type (DefinitelyTyped) sont disponibles pour la plupart des bibliothèques JavaScript, ce qui permet de bénéficier de la vérification de type dans ces frameworks.

### Node.js

*   TypeScript peut être utilisé pour développer des applications Node.js côté serveur.
*   Le code TypeScript est compilé en JavaScript avant d'être exécuté par Node.js.
## 11. Tests en TypeScript

### Utilisation d'outils de test JavaScript (Jest, Mocha) avec TypeScript

*   TypeScript peut être testé avec les mêmes outils que JavaScript (ex: Jest, Mocha).
*   Il est nécessaire d'utiliser un transpileur (ex: ts-jest, ts-node) pour exécuter le code TypeScript dans l'environnement de test.
## 12. Bonnes Pratiques

### Conventions de nommage

*   Utiliser le camelCase pour les noms de variables et de fonctions.
*   Utiliser le PascalCase pour les noms de classes et d'interfaces.
*   Utiliser des noms clairs et descriptifs.

### Gestion des erreurs

*   Utiliser les blocs `try...catch` pour gérer les exceptions.
*   Utiliser des types stricts pour éviter les erreurs de type.
*   Utiliser des outils de linting pour détecter les erreurs potentielles.

### Utilisation stricte des types

*   Activer l'option `strict` dans le fichier `tsconfig.json` pour bénéficier d'une vérification de type plus rigoureuse.
## 13. Ressources et Communauté

### Documentation officielle

*   [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/typescript)](https://www.reddit.com/r/typescript/)

---
title: CSS Variables (Custom Properties) - Pour un code plus dynamique
tags:
  - CSS
  - Variables
  - Custom Properties
draft: false
---

# Article 8 : CSS Variables (Custom Properties) - Pour Un Code plus Dynamique

## Introduction

Pendant longtemps, les développeurs CSS ont rêvé d'avoir des variables natives pour stocker des valeurs réutilisables comme les couleurs, les tailles de police ou les espacements. Cette fonctionnalité était l'un des principaux attraits des préprocesseurs CSS comme SASS ou LESS. Cependant, les variables des préprocesseurs ont une limite majeure : elles sont traitées *avant* que le CSS n'atteigne le navigateur. Une fois compilées en CSS natif, elles n'existent plus et ne peuvent pas être modifiées dynamiquement, par exemple via JavaScript ou en réponse à des changements d'état.

Les **variables CSS natives**, officiellement appelées **Custom Properties for Cascading Variables**, résolvent ce problème. Elles vivent dans le navigateur, participent à la cascade CSS, et peuvent être lues et modifiées en temps réel. Cela ouvre de nouvelles possibilités pour créer des designs plus dynamiques, des thèmes gérables et des systèmes de design flexibles.

Cet article vous fera découvrir la puissance des variables CSS natives : comment les déclarer, les utiliser, gérer leur portée et les exploiter pour rendre votre CSS plus puissant et plus facile à maintenir.

## Contenu Principal

Les variables CSS sont des entités définies par l'auteur d'une feuille de style qui contiennent des valeurs spécifiques réutilisables à travers un document. Elles fonctionnent comme n'importe quelle autre propriété CSS en termes de cascade et d'héritage.

### Syntaxe Des Variables CSS

La syntaxe des variables CSS est simple et se compose de deux parties : la déclaration et l'utilisation.

* **Déclaration (--ma-variable) :**
    Les variables CSS sont déclarées avec un préfixe double tiret (`--`), suivi d'un nom (qui peut inclure des lettres, des chiffres, des tirets et des underscores). La déclaration se fait à l'intérieur d'un bloc de règles, comme n'importe quelle autre propriété.

    ```css
    :root { /* Déclaration d\'une variable globale */
      --primary-color: #007bff;
      --spacing-unit: 8px;
    }
    ```

    Le sélecteur `:root` est une pseudo-classe qui cible l'élément racine du document (généralement `<html>`), ce qui est l'endroit habituel pour déclarer des variables qui doivent être accessibles globalement.

    Vous pouvez déclarer des variables dans n'importe quel sélecteur, ce qui limite leur portée à ce sélecteur et à ses descendants.

    ```css
    .card { /* Déclaration d\'une variable locale au sélecteur .card */
      --card-border-color: #ccc;
    }
    ```

* **Utilisation (var(--ma-variable)) :**
    Pour utiliser la valeur d'une variable CSS, vous utilisez la fonction `var()` en lui passant le nom de la variable en argument.

    ```css
    body {
      background-color: #f4f4f4;
      padding: calc(var(--spacing-unit) * 2); /* Utilisation de la variable avec calc() */
    }

    h1 {
      color: var(--primary-color);
    }
    ```

* **Valeurs par défaut :**
    La fonction `var()` accepte un deuxième argument facultatif, qui est une valeur de secours (fallback). Cette valeur sera utilisée si la variable spécifiée n'est pas trouvée ou n'est pas valide dans la portée actuelle.

    ```css
    .element {
      color: var(--secondary-color, purple); /* Utilise --secondary-color si elle existe, sinon utilise purple */
      border: 1px solid var(--card-border-color, black); /* Utilise --card-border-color si elle existe, sinon utilise black */
    }
    ```

    Cela est utile pour rendre vos composants plus robustes, car ils peuvent fonctionner même si certaines variables ne sont pas définies globalement.

### Portée Des Variables

L'un des aspects les plus puissants des variables CSS est qu'elles respectent les règles de la cascade et de l'héritage CSS, tout comme les propriétés standard.

* **Variables globales (:root) :**
    Déclarer des variables dans le sélecteur `:root` les rend accessibles à tous les éléments du document. C'est l'endroit idéal pour définir des valeurs globales qui font partie de votre système de design (couleurs principales, typographie de base, espacements standards).

    ```css
    :root {
      --font-family-base: \'Arial\', sans-serif;\n
      --text-color: #333;
    }

    body {
      font-family: var(--font-family-base); /* Hérite de la variable définie sur :root */
      color: var(--text-color);
    }
    ```

* **Variables locales (dans un sélecteur) :**
    Vous pouvez déclarer des variables à l'intérieur de n'importe quel sélecteur. Ces variables ne seront accessibles qu'aux éléments ciblés par ce sélecteur et à leurs éléments descendants. Cela permet de créer des variables spécifiques à des composants ou des sections particulières.

    ```css
    .theme-dark {
      --background-color: #333;
      --text-color: #f4f4f4;
    }

    .theme-light {
      --background-color: #f4f4f4;
      --text-color: #333;
    }
    ```

    Ici, les variables `--background-color` et `--text-color` sont définies localement aux classes `.theme-dark` et `.theme-light`.

* **Cascade et héritage :**
    Si une variable est déclarée dans plusieurs règles, la règle la plus spécifique (selon les règles de spécificité CSS) l'emporte. Les variables déclarées sur un élément parent sont héritées par ses enfants, à moins qu'un enfant ne redéclare la même variable.

    ```css
    :root {
      --main-bg: blue;
    }

    div {
      --main-bg: red; /* Redéfinit la variable pour les divs et leurs descendants */
      background-color: var(--main-bg); /* Sera rouge */
    }

    span {
      background-color: var(--main-bg); /* Hérite la variable de son parent (div si à l\'intérieur) ou de :root si pas dans un div */
    }
    ```

    Cela signifie que vous pouvez facilement surcharger des variables pour des sections spécifiques de votre site, ce qui est idéal pour les thèmes ou les variations de composants.

### Cas D'utilisation

Les variables CSS sont incroyablement polyvalentes. Voici quelques exemples concrets de leur utilité :

* **Systèmes de couleurs :** Définissez votre palette de couleurs principale avec des noms sémantiques (ex: `--color-primary`, `--color-secondary`, `--color-success`, `--color-error`).

    ```css
    :root {
      --color-brand: #6200ee; /* Votre couleur principale */
      --color-text-dark: #212121;
      --color-text-light: #ffffff;
      --color-background-light: #f5f5f5;
      --color-background-dark: #121212;
    }
    ```

    Utilisez ensuite ces variables dans toute votre feuille de style. Changer une couleur globale devient aussi simple que de modifier une seule ligne dans le sélecteur `:root`.

* **Thèmes (clair/sombre) :** Combinez les variables locales avec la cascade. Définissez des variables pour les couleurs de texte et de fond par défaut, puis créez une classe (par exemple, `.theme-dark`) qui redéfinit ces mêmes variables pour un thème sombre. En appliquant cette classe à l'élément `<body>` ou à un conteneur, vous changez facilement le thème de toute la section.

    ```css
    /* Thème par défaut (clair) */
    :root {
      --page-bg: var(--color-background-light);
      --page-text: var(--color-text-dark);
    }

    /* Thème sombre - surcharge les variables */
    .theme-dark {
      --page-bg: var(--color-background-dark);
      --page-text: var(--color-text-light);
    }

    body {
      background-color: var(--page-bg);
      color: var(--page-text);
    }
    ```

* **Espacement cohérent :** Définissez une échelle d'espacement basée sur une unité de base.

    ```css
    :root {
      --spacing-sm: 8px;
      --spacing-md: 16px;
      --spacing-lg: 24px;
    }

    .card {
      padding: var(--spacing-md);
      margin-bottom: var(--spacing-lg);
    }
    ```

* **Réutilisation de valeurs complexes :** Stockez des valeurs complexes comme des ombres portées ou des dégradés.

    ```css
    :root {
      --fancy-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }

    .element-with-shadow {
      box-shadow: var(--fancy-shadow);
    }
    ```

### Manipulation Dynamique Avec JavaScript

C'est là que les variables CSS deviennent vraiment dynamiques et surpassent les variables des préprocesseurs. Comme elles existent dans le DOM, vous pouvez les lire et les modifier avec JavaScript.

* **Lecture des variables :**
    Utilisez `getComputedStyle()` pour lire la valeur finale calculée d'une variable sur un élément.

    ```javascript
    const element = document.querySelector(\':root\'); // Ou tout autre élément
    const primaryColor = getComputedStyle(element).getPropertyValue(\'--primary-color\').trim();
    console.log(primaryColor); // Affiche la valeur actuelle de --primary-color
    ```

* **Modification des variables :**
    Utilisez `style.setProperty()` sur un élément pour modifier dynamiquement la valeur d'une variable pour cet élément et ses descendants.

    ```javascript
    const element = document.querySelector(\':root\'); // Modifier une variable globale
    // const element = document.querySelector(\'.my-component\'); // Modifier une variable locale

    element.style.setProperty(\'--primary-color\', \'#ff4500\'); // Change la couleur principale
    element.style.setProperty(\'--spacing-unit\', \'12px\'); // Change l\'unité d\'espacement
    ```

    Cela est extrêmement utile pour implémenter des thèmes basculables (sombre/clair), des paramètres personnalisables par l'utilisateur, ou des animations complexes contrôlées par JavaScript modifiant des propriétés CSS indirectement via des variables.

## En Pratique

Passons à quelques exemples concrets pour voir les variables CSS en action.

### Création D'un Système De Design Simple Avec Variables

Définissons des variables pour les couleurs, la typographie et l'espacement de base dans un fichier `style.css`.

```css
:root {
  /* Couleurs */
  --color-primary: #007bff;
  --color-secondary: #6c757d;
  --color-success: #28a745;
  --color-danger: #dc3545;
  --color-light: #f8f9fa;
  --color-dark: #343a40;
  --color-text: var(--color-dark);
  --color-background: var(--color-light);

  /* Typographie */
  --font-family-sans-serif: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  --font-size-base: 1rem; /* 16px par défaut */
  --line-height-base: 1.5;

  /* Espacement */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
}

body {
  font-family: var(--font-family-sans-serif);
  font-size: var(--font-size-base);
  line-height: var(--line-height-base);
  color: var(--color-text);
  background-color: var(--color-background);
  padding: var(--space-md);
}

h1, h2, h3 {
  color: var(--color-primary);
}

button {
  padding: var(--space-sm) var(--space-md);
  background-color: var(--color-primary);
  color: white;
  border: none;
  border-radius: var(--space-xs);
  cursor: pointer;
}

button:hover {
  background-color: var(--color-dark);
}
```

Maintenant, tous vos éléments utilisent ces variables. Si votre marque change de couleur principale, il suffit de modifier `--color-primary` à un seul endroit.

### Implémentation D'un Thème sombre/clair

En étendant l'exemple précédent, ajoutez une classe pour surcharger les variables de thème.

```css
/* Surcharge pour le thème sombre */
.theme-dark {
  --color-text: var(--color-light);
  --color-background: var(--color-dark);
  --color-primary: #bb86fc; /* Peut aussi changer les couleurs d\'accentuation */
}
```

Dans votre HTML, basculez la classe `theme-dark` sur le `<body>` (ou un autre conteneur) pour changer instantanément le thème.

```html
<body class="theme-dark">
  <h1>Mon Titre</h1>
  <p>Ceci est un paragraphe en thème sombre.</p>
  <button>Cliquez moi</button>
</body>

<!-- Pour le thème clair -->
<!-- <body> -->
<!--   <h1>Mon Titre</h1> -->
<!--   <p>Ceci est un paragraphe en thème clair.</p> -->
<!--   <button>Cliquez moi</button> -->
<!-- </body> -->
```

Un simple script JavaScript peut gérer la bascule de classe, éventuellement en sauvegardant le choix de l'utilisateur dans le stockage local.

### Adaptation Responsive Avec Variables CSS

Bien que les media queries soient le principal outil pour le design responsive, les variables CSS peuvent les compléter en permettant de modifier des valeurs clés en fonction de la taille de l'écran.

```css
/dev/null/style.css#L33-43
:root {
  --fluid-padding: 1rem;
}

body {
  padding: var(--fluid-padding);
}

@media (min-width: 768px) {
  :root {
    --fluid-padding: 2rem; /* Change la valeur de la variable sur les écrans plus larges */
  }
}
```

Ici, le padding du corps s'adapte grâce à la variable `--fluid-padding` dont la valeur est modifiée dans la media query. Vous pouvez faire de même pour la taille de police, l'espacement, etc.

## Conclusion

Les variables CSS (Custom Properties) sont une addition majeure et très bienvenue au langage CSS. Elles apportent une capacité de réutilisation et de dynamisme qui était auparavant limitée aux préprocesseurs. En comprenant leur syntaxe, leur portée et leur interaction avec la cascade, vous pouvez créer des systèmes de design plus flexibles, des thèmes facilement basculables et rendre votre code CSS beaucoup plus propre et maintenable.

Contrairement aux variables de préprocesseurs qui disparaissent après la compilation, les variables CSS natives résident dans le navigateur, ce qui permet de les manipuler en temps réel avec JavaScript et de les faire participer pleinement à la cascade et aux media queries.

Elles se combinent également très bien avec d'autres fonctionnalités CSS modernes comme `calc()` pour effectuer des calculs basés sur les variables, ou même avec les media queries et les pseudo-classes pour des adaptations conditionnelles.

Le support des navigateurs pour les variables CSS est excellent aujourd'hui, ce qui vous permet de les utiliser en toute confiance dans vos projets.

## Comparaison Avec Les Variables De Préprocesseurs

| Caractéristique       | Variables Préprocesseurs (SASS, LESS) | Variables CSS Natives (--*)      |
| :-------------------- | :------------------------------------ | :------------------------------ |
| Exécution             | Au moment de la compilation           | Dans le navigateur (runtime)    |
| Accès dynamique (JS)  | Non                                   | Oui (lecture et écriture)     |
| Cascade/Héritage      | Non (résolues avant)                  | Oui (participent à la cascade)  |
| Portée                | Définie par le préprocesseur (@import) | Définie par le sélecteur (DOM) |
| Fallback (valeur par défaut) | Souvent intégré dans la syntaxe   | Intégré dans `var()`          |

Bien que les préprocesseurs offrent d'autres fonctionnalités (imbrication, mixins, boucles) qui restent utiles, les variables CSS natives sont supérieures pour tout ce qui nécessite une flexibilité au moment de l'exécution ou une intégration avec la cascade.

## Combinaison Avec `calc()` Et Autres Fonctions CSS

Les variables CSS sont particulièrement puissantes lorsqu'elles sont combinées avec des fonctions CSS comme `calc()`, `min()`, `max()`, et `clamp()`.

```css
:root {
  --base-size: 16px;
  --scale-factor: 1.5;
  --min-font: 1rem;
  --max-font: 2rem;
}

.element {
  font-size: calc(var(--base-size) * var(--scale-factor)); /* Calcul basé sur des variables */
  padding: calc(var(--base-size) / 2);
}

.responsive-text {
  /* Taille de police fluide entre 1rem et 2rem, dépendante de la largeur du viewport et d\'une taille idéale */
  font-size: clamp(var(--min-font), calc(1rem + 2vw), var(--max-font));
}
```

Cette capacité à effectuer des calculs et à utiliser des fonctions basées sur des valeurs stockées dans des variables rend le CSS incroyablement flexible et permet de créer des designs véritablement adaptatifs et basés sur des règles claires.

## Ressources Pour Approfondir

* [MDN Web Docs - Utilisation des variables CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)
* [Une introduction aux variables CSS (Custom Properties)](https://grafikart.fr/tutoriels/variables-css-1021)

En intégrant les variables CSS dans votre pratique quotidienne, vous ferez un grand pas vers l'écriture de CSS plus moderne, plus propre et plus puissant.

```

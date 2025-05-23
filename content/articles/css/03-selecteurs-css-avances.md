---
title: Sélecteurs CSS avancés
tags:
  - CSS
  - Sélecteurs
draft: false
---

# Article 3: Sélecteurs CSS Avancés

## Introduction

Dans l'article précédent, nous avons abordé les sélecteurs CSS fondamentaux comme les sélecteurs de type, de classe et d'ID. Si ces derniers sont suffisants pour cibler des éléments simples, les pages web modernes nécessitent souvent une capacité de ciblage beaucoup plus précise. C'est là qu'interviennent les sélecteurs CSS avancés.

Maîtriser les sélecteurs avancés vous permet de cibler des éléments en fonction de leur relation avec d'autres, de leurs attributs spécifiques, de leur état (interaction utilisateur, position dans la structure) ou même de parties spécifiques de leur contenu. Utiliser les bons sélecteurs rend votre CSS plus efficace, plus lisible et plus facile à maintenir, car vous pouvez appliquer des styles sans avoir à ajouter inutilement des classes ou des IDs à votre HTML.

Cet article va explorer ces différents types de sélecteurs avancés et vous montrer comment les utiliser pour cibler précisément les éléments de votre page web.

## Contenu Principal

Les sélecteurs CSS avancés peuvent être regroupés en plusieurs catégories : les sélecteurs de relation, les sélecteurs d'attribut, les pseudo-classes et les pseudo-éléments.

### Sélecteurs De relation

Ces sélecteurs ciblent des éléments en fonction de leur position par rapport à d'autres éléments dans l'arbre HTML.

* **Sélecteur descendant (espace)** : Cible un élément qui est un descendant (enfant, petit-enfant, etc.) d'un autre élément spécifié.

    ```css
    article p {
        color: #333; /* Cible tous les paragraphes à l'intérieur d'un article */
    }
    ```

* **Sélecteur d'enfant direct (>)** : Cible un élément qui est l'enfant direct d'un autre élément spécifié.

    ```css
    ul > li {
        border-bottom: 1px solid #ccc; /* Cible uniquement les li qui sont enfants directs d'un ul */
    }
    ```

* **Sélecteur adjacent (+)** : Cible le premier élément qui suit immédiatement un autre élément spécifié, et qui a le même parent.

    ```css
    h2 + p {
        margin-top: 0; /* Cible le paragraphe qui suit immédiatement un h2 */
    }
    ```

* **Sélecteur frère général (~)** : Cible tous les éléments qui suivent un autre élément spécifié, et qui ont le même parent.

    ```css
    h2 ~ p {
        text-indent: 1em; /* Cible tous les paragraphes qui suivent un h2 (pas seulement le premier) */
    }
    ```

### Sélecteurs D'attribut

Ces sélecteurs ciblent des éléments en fonction de la présence ou de la valeur de leurs attributs HTML.

* **[attr]** : Cible les éléments qui possèdent l'attribut spécifié, quelle que soit sa valeur.

    ```css
    a[href] {
        text-decoration: none; /* Cible tous les liens qui ont un attribut href */
    }
    ```

* **[attr=valeur]** : Cible les éléments dont l'attribut spécifié a exactement la valeur indiquée.

    ```css
    input[type="text"] {
        border: 1px solid blue; /* Cible les inputs dont le type est exactement "text" */
    }
    ```

* **[attr^=valeur] (commence par)** : Cible les éléments dont l'attribut spécifié commence par la chaîne de caractères indiquée.

    ```css
    a[href^="https://"] {
        color: green; /* Cible les liens dont l'URL commence par "https://" */
    }
    ```

* **[attr$=valeur] (finit par)** : Cible les éléments dont l'attribut spécifié se termine par la chaîne de caractères indiquée.

    ```css
    a[href$=".pdf"] {
        font-weight: bold; /* Cible les liens dont l'URL se termine par ".pdf" */
    }
    ```

* **[attr*=valeur] (contient)** : Cible les éléments dont l'attribut spécifié contient la chaîne de caractères indiquée n'importe où.

    ```css
    a[href*="example"] {
        text-decoration: underline; /* Cible les liens dont l'URL contient "example" */
    }
    ```

### Pseudo-classes

Les pseudo-classes vous permettent de cibler des éléments en fonction de leur état particulier ou de leur position dans l'arbre du document.

* **:hover** : Cible un élément lorsque l'utilisateur le survole avec le pointeur de la souris.
* **:active** : Cible un élément lorsqu'il est activé (par exemple, cliqué).
* **:focus** : Cible un élément lorsqu'il a le focus (par exemple, sélectionné par la touche Tab).

    ```css
    button:hover {
        opacity: 0.8;
    }

    input:focus {
        border-color: blue;
    }
    ```

* **:first-child** : Cible le premier enfant d'un parent.
* **:last-child** : Cible le dernier enfant d'un parent.
* **:nth-child(n)** : Cible les enfants d'un parent en fonction d'une formule (n est la position, peut être un nombre, `odd`, `even`, ou une expression comme `2n+1`).

    ```css
    li:first-child {
        font-weight: bold;
    }

    li:last-child {
        border-bottom: none;
    }

    li:nth-child(odd) {
        background-color: #f0f0f0; /* Cible les éléments li impairs */
    }
    ```

* **:not(selector)** : Cible les éléments qui NE correspondent PAS au sélecteur spécifié entre parenthèses.

    ```css
    div:not(.sidebar) {
        margin-left: 20px; /* Cible tous les div sauf ceux ayant la classe "sidebar" */
    }
    ```

* **:empty** : Cible les éléments qui n'ont aucun contenu (ni texte, ni enfants).

    ```css
    p:empty {
        display: none; /* Cache les paragraphes vides */
    }
    ```

### Pseudo-éléments

Les pseudo-éléments vous permettent de cibler et de styliser des parties spécifiques d'un élément ou de générer du contenu qui n'existe pas réellement dans le HTML. On les préfixe généralement par deux doubles-points (`::`) pour les distinguer des pseudo-classes, même si la notation avec un seul double-point (`:`) est historiquement acceptée pour la plupart d'entre eux.

* **::before** : Crée un pseudo-élément qui est le premier enfant de l'élément ciblé. Souvent utilisé avec la propriété `content`.
* **::after** : Crée un pseudo-élément qui est le dernier enfant de l'élément ciblé. Souvent utilisé avec la propriété `content`.

    ```css
    a::before {
        content: url("icon.png"); /* Ajoute une icône avant chaque lien */
        margin-right: 5px;
    }

    p::after {
        content: " [Fin]"; /* Ajoute le texte "[Fin]" après chaque paragraphe */
        font-size: 0.8em;
        color: gray;
    }
    ```

* **::first-letter** : Cible la première lettre du premier ligne de bloc d'un élément.

    ```css
    p::first-letter {
        font-size: 2em;
        font-weight: bold;
        float: left;
        margin-right: 5px;
    }
    ```

* **::first-line** : Cible la première ligne de texte d'un élément de bloc.

    ```css
    p::first-line {
        font-variant: small-caps;
    }
    ```

* **::selection** : Cible la partie d'un élément que l'utilisateur a sélectionnée (mis en surbrillance) avec la souris ou le clavier.

    ```css
    ::selection {
        background-color: yellow;
        color: black;
    }
    ```

## En Pratique

Pour bien comprendre ces sélecteurs, la meilleure approche est de les utiliser.

1. **Exemples pratiques pour chaque type de sélecteur** : Créez une page HTML simple avec différentes structures imbriquées (listes, divs, spans, liens avec différents attributs, inputs, etc.). Appliquez ensuite les sélecteurs de relation et d'attributs pour styliser des éléments spécifiques sans utiliser de classes ou d'IDs. Observez comment les styles s'appliquent.
2. **Création d'effets interactifs avec les pseudo-classes** : Utilisez les pseudo-classes `:hover`, `:active` et `:focus` pour changer l'apparence des boutons, des liens ou des champs de formulaire lorsque l'utilisateur interagit avec eux. Expérimentez avec les transitions CSS pour rendre ces changements plus fluides.
3. **Générateur de contenu avec ::before et ::after** : Utilisez les pseudo-éléments `::before` et `::after` pour ajouter des icônes, des guillemets décoratifs, ou d'autres éléments visuels sans modifier le HTML. N'oubliez pas que ces pseudo-éléments nécessitent la propriété `content`.

Utilisez les outils de développement de votre navigateur (Inspecteur) pour visualiser les sélecteurs appliqués et comprendre pourquoi un style s'applique ou non.

## Conclusion

Les sélecteurs CSS avancés sont des outils puissants qui vous permettent de cibler précisément les éléments de votre page web, rendant votre CSS plus robuste et plus facile à gérer. Comprendre les sélecteurs de relation, d'attribut, les pseudo-classes et les pseudo-éléments est essentiel pour écrire du CSS efficace.

N'oubliez pas que l'utilisation de sélecteurs trop complexes peut augmenter la spécificité et potentiellement rendre votre CSS plus difficile à surcharger. Il est important de trouver un équilibre.

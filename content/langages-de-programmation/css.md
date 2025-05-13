---
title: CSS
draft: false
tags:
  - css
  - stylesheet
description: Langage de feuille de style utilisé pour décrire la présentation d'un document écrit en HTML ou XML.
---

## Sommaire

1.  Introduction à CSS
    *   Qu'est-ce que CSS ?
    *   Historique et versions (CSS3)
    *   Comment appliquer du CSS (inline, interne, externe)
    *   Sélecteurs de base
2.  Sélecteurs CSS
    *   Sélecteurs d'éléments, de classes, d'ID
    *   Sélecteurs d'attributs
    *   Pseudo-classes et pseudo-éléments
    *   Combinateurs
3.  Propriétés CSS Courantes
    *   Couleurs et arrière-plans
    *   Typographie (police, taille, poids, style)
    *   Modèle de boîte (margin, padding, border)
    *   Dimensions (width, height)
4.  Disposition (Layout)
    *   Modèle de flux normal
    *   Display (block, inline, inline-block, none)
    *   Positionnement (static, relative, absolute, fixed, sticky)
    *   Float et Clear
    *   Flexbox
    *   CSS Grid
5.  Responsive Design
    *   Media Queries
    *   Unités relatives (%, vw, vh, em, rem)
    *   Images flexibles
6.  Transitions et Animations
    *   Transitions CSS
    *   Keyframes et animations CSS
7.  Transformation
    *   Transformations 2D et 3D (translate, rotate, scale, skew)
8.  Sass et Less (Préprocesseurs CSS)
    *   Variables, Mixins, Nesting
    *   Compilation
9.  Méthodologies CSS
    *   BEM, OOCSS, SMACSS
10. Bonnes Pratiques
    *   Organisation du code CSS
    *   Commentaires
    *   Performance
11. Outils de Développement
    *   Inspecteur de navigateur
    *   Validateurs CSS
12. Ressources et Communauté
    *   Documentation MDN Web Docs
    *   Communautés en ligne
## 1. Introduction à CSS

### Qu'est-ce que CSS ?

CSS (Cascading Style Sheets) est un langage de feuille de style utilisé pour décrire la présentation d'un document écrit en HTML ou XML. Il permet de contrôler la couleur, la police, la disposition et d'autres aspects de la présentation.

### Historique et versions (CSS3)

*   CSS1 (1996) : Les bases du CSS.
*   CSS2 (1998) : Ajout de fonctionnalités comme le positionnement absolu, les types de média.
*   CSS3 (début des années 2000 - en cours) : Modularisation du CSS, ajout de nombreuses nouvelles fonctionnalités (animations, transitions, flexbox, grid, etc.).

### Comment appliquer du CSS (inline, interne, externe)

*   **Inline**: Directement dans les balises HTML (attribut `style`).  À éviter pour la maintenabilité.
*   **Interne**: Dans la balise `<style>` à l'intérieur de la balise `<head>`.
*   **Externe**: Dans un fichier `.css` séparé, lié au HTML avec la balise `<link>`.  Méthode recommandée.

```html
<!DOCTYPE html>
<html>
<head>
    <title>CSS Example</title>
    <link rel="stylesheet" type="text/css" href="style.css">
    <style>
        /* Style interne */
        body {
            font-family: Arial, sans-serif;
        }
    </style>
</head>
<body>
    <p style="color: blue;">Texte en bleu (style inline)</p>
</body>
</html>
```

### Sélecteurs de base

*   **Sélecteur universel**: `*` (sélectionne tous les éléments)
*   **Sélecteur d'élément**: `p` (sélectionne tous les paragraphes)
*   **Sélecteur de classe**: `.ma-classe` (sélectionne tous les éléments avec la classe `ma-classe`)
*   **Sélecteur d'ID**: `#mon-id` (sélectionne l'élément avec l'ID `mon-id`)

```css
/* Sélecteur universel */
* {
    margin: 0;
    padding: 0;
}

/* Sélecteur d'élément */
p {
    color: black;
}

/* Sélecteur de classe */
.ma-classe {
    font-size: 16px;
}

/* Sélecteur d'ID */
#mon-id {
    font-weight: bold;
}
```

## 2. Sélecteurs CSS

### Sélecteurs d'éléments, de classes, d'ID

Déjà couverts dans les sélecteurs de base.

### Sélecteurs d'attributs

Sélectionnent les éléments en fonction de la présence ou de la valeur de leurs attributs.

*   `[attribut]` : Sélectionne les éléments qui ont l'attribut spécifié.
*   `[attribut=valeur]` : Sélectionne les éléments dont l'attribut a la valeur spécifiée.
*   `[attribut~=valeur]` : Sélectionne les éléments dont l'attribut contient la valeur spécifiée (séparée par des espaces).
*   `[attribut|=valeur]` : Sélectionne les éléments dont l'attribut commence par la valeur spécifiée, suivie d'un tiret.
*   `[attribut^=valeur]` : Sélectionne les éléments dont l'attribut commence par la valeur spécifiée.
*   `[attribut$=valeur]` : Sélectionne les éléments dont l'attribut se termine par la valeur spécifiée.
*   `[attribut*=valeur]` : Sélectionne les éléments dont l'attribut contient la valeur spécifiée.

```html
<a href="https://www.example.com">Example</a>
<a href="https://www.example.net">Example Net</a>
<input type="text" value="test">
```

```css
a[href] {
    color: green;
}

a[href="https://www.example.com"] {
    font-weight: bold;
}

input[type="text"] {
    border: 1px solid red;
}
```

### Pseudo-classes et pseudo-éléments

*   **Pseudo-classes**: Sélectionnent les éléments en fonction de leur état (ex: `:hover`, `:active`, `:focus`, `:visited`).
*   **Pseudo-éléments**: Créent des parties virtuelles d'un élément (ex: `::before`, `::after`, `::first-line`, `::first-letter`).

```html
<a href="#">Hover me</a>
<p>First line of this paragraph.</p>
```

```css
a:hover {
    color: red;
}

p::first-line {
    font-weight: bold;
}
```

### Combinateurs

Décrivent la relation entre les sélecteurs.

*   **Descendant**: `div p` (sélectionne tous les paragraphes à l'intérieur d'une `div`)
*   **Enfant**: `div > p` (sélectionne tous les paragraphes qui sont des enfants directs d'une `div`)
*   **Adjacent**: `h1 + p` (sélectionne le premier paragraphe qui suit immédiatement un `h1`)
*   **Général**: `h1 ~ p` (sélectionne tous les paragraphes qui suivent un `h1`)

```html
<div>
    <p>Paragraphe dans div</p>
    <article>
        <p>Paragraphe dans article dans div</p>
    </article>
</div>
<h1>Titre</h1>
<p>Paragraphe après h1</p>
<p>Autre paragraphe après h1</p>
```

```css
div p {
    color: blue; /* Tous les paragraphes dans div */
}

div > p {
    font-style: italic; /* Seulement le premier paragraphe dans div */
}

h1 + p {
    font-weight: bold; /* Seulement le premier paragraphe après h1 */
}

h1 ~ p {
    text-decoration: underline; /* Tous les paragraphes après h1 */
}
```

## 3. Propriétés CSS Courantes

### Couleurs et arrière-plans

*   `color`: Couleur du texte.
*   `background-color`: Couleur de l'arrière-plan.
*   `background-image`: Image d'arrière-plan.
*   `background-repeat`: Répétition de l'image d'arrière-plan.
*   `background-position`: Position de l'image d'arrière-plan.
*   `background-size`: Taille de l'image d'arrière-plan.

```css
body {
    color: #333;
    background-color: #f0f0f0;
    background-image: url("background.png");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}
```

### Typographie (police, taille, poids, style)

*   `font-family`: Police de caractères.
*   `font-size`: Taille de la police.
*   `font-weight`: Poids de la police (bold, normal, etc.).
*   `font-style`: Style de la police (italic, normal).
*   `line-height`: Hauteur de ligne.
*   `text-align`: Alignement du texte.
*   `text-decoration`: Décoration du texte (underline, none, etc.).

```css
p {
    font-family: Arial, sans-serif;
    font-size: 14px;
    font-weight: normal;
    font-style: normal;
    line-height: 1.5;
    text-align: justify;
    text-decoration: none;
}
```

### Modèle de boîte (margin, padding, border)

*   `margin`: Marge extérieure (espace autour de l'élément).
*   `padding`: Marge intérieure (espace entre le contenu et la bordure).
*   `border`: Bordure de l'élément.

```css
div {
    margin: 20px;
    padding: 10px;
    border: 1px solid black;
}
```

### Dimensions (width, height)

*   `width`: Largeur de l'élément.
*   `height`: Hauteur de l'élément.
*   `max-width`: Largeur maximale de l'élément.
*   `max-height`: Hauteur maximale de l'élément.
*   `min-width`: Largeur minimale de l'élément.
*   `min-height`: Hauteur minimale de l'élément.

```css
img {
    width: 100%; /* Prend toute la largeur disponible */
    height: auto; /* Hauteur automatique pour conserver les proportions */
    max-width: 500px; /* Largeur maximale de 500px */
}
```
## 4. Disposition (Layout)

### Modèle de flux normal

Le modèle de flux normal est la façon dont les éléments HTML sont affichés par défaut dans le navigateur. Les éléments de niveau bloc occupent toute la largeur disponible et sont placés les uns au-dessus des autres. Les éléments de niveau en ligne sont placés côte à côte, en fonction de l'espace disponible.

### Display (block, inline, inline-block, none)

La propriété `display` spécifie le type de boîte utilisée pour un élément.

*   `block`: L'élément se comporte comme un élément de niveau bloc.
*   `inline`: L'élément se comporte comme un élément de niveau en ligne.
*   `inline-block`: L'élément se comporte comme un élément de niveau en ligne, mais peut avoir une largeur et une hauteur spécifiées.
*   `none`: L'élément n'est pas affiché.

```css
div {
    display: block;
}

span {
    display: inline;
}

button {
    display: inline-block;
    width: 100px;
    height: 30px;
}

.hidden {
    display: none;
}
```

### Positionnement (static, relative, absolute, fixed, sticky)

La propriété `position` spécifie la méthode de positionnement utilisée pour un élément.

*   `static`: Positionnement par défaut (dans le flux normal).
*   `relative`: Positionné par rapport à sa position normale.
*   `absolute`: Positionné par rapport à son ancêtre positionné le plus proche (ou à l'élément `<html>` s'il n'y en a pas).
*   `fixed`: Positionné par rapport à la fenêtre du navigateur.
*   `sticky`: Positionné comme `relative` jusqu'à ce qu'il atteigne une certaine position, puis devient `fixed`.

```css
div {
    position: static;
}

.relative {
    position: relative;
    top: 20px;
    left: 30px;
}

.absolute {
    position: absolute;
    top: 50px;
    right: 0;
}

.fixed {
    position: fixed;
    bottom: 0;
    left: 0;
}

.sticky {
    position: sticky;
    top: 10px;
}
```

### Float et Clear

La propriété `float` positionne un élément à gauche ou à droite de son conteneur, permettant au texte et aux autres éléments de s'enrouler autour de lui. La propriété `clear` spécifie quels côtés d'un élément ne doivent pas avoir d'éléments flottants.

```css
img {
    float: left;
    margin-right: 10px;
}

.clearfix {
    clear: both;
}
```

### Flexbox

Flexbox est un modèle de disposition unidimensionnel qui permet de créer des interfaces utilisateur flexibles et réactives.

```css
.container {
    display: flex;
    flex-direction: row; /* ou column */
    justify-content: center; /* alignement horizontal */
    align-items: center; /* alignement vertical */
}

.item {
    flex: 1; /* Prend la même quantité d'espace que les autres éléments */
}
```

### CSS Grid

CSS Grid est un modèle de disposition bidimensionnel qui permet de créer des mises en page complexes avec des lignes et des colonnes.

```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr; /* 3 colonnes de largeur égale */
    grid-template-rows: auto auto;
    grid-gap: 10px; /* Espacement entre les éléments */
}

.grid-item {
    grid-column: 1 / 3; /* S'étend de la colonne 1 à la colonne 3 */
}
```
## 5. Responsive Design

### Media Queries

Les media queries permettent d'appliquer des styles différents en fonction des caractéristiques du périphérique (taille de l'écran, résolution, orientation, etc.).

```css
/* Styles pour les écrans de petite taille (max-width: 768px) */
@media (max-width: 768px) {
    body {
        font-size: 12px;
    }
    .container {
        width: 100%;
    }
}

/* Styles pour les écrans de grande taille (min-width: 992px) */
@media (min-width: 992px) {
    body {
        font-size: 16px;
    }
    .container {
        width: 960px;
    }
}
```

### Unités relatives (%, vw, vh, em, rem)

Les unités relatives permettent de définir des tailles qui s'adaptent à la taille de l'écran ou à la taille de la police.

*   `%`: Pourcentage de la taille de l'élément parent.
*   `vw`: Pourcentage de la largeur de la fenêtre du navigateur.
*   `vh`: Pourcentage de la hauteur de la fenêtre du navigateur.
*   `em`: Taille relative à la taille de la police de l'élément.
*   `rem`: Taille relative à la taille de la police de l'élément racine (`<html>`).

```css
body {
    font-size: 16px;
}

h1 {
    font-size: 2em; /* 2 fois la taille de la police du body */
}

.container {
    width: 80%; /* 80% de la largeur de l'élément parent */
}
```

### Images flexibles

Les images flexibles s'adaptent à la taille de l'écran sans perdre leur qualité.

```css
img {
    max-width: 100%;
    height: auto;
}
```
## 6. Transitions et Animations

### Transitions CSS

Les transitions CSS permettent de créer des animations simples en modifiant progressivement les valeurs des propriétés CSS.

```css
button {
    background-color: blue;
    color: white;
    transition: background-color 0.3s ease; /* Transition sur la couleur de fond */
}

button:hover {
    background-color: darkblue;
}
```

### Keyframes et animations CSS

Les keyframes permettent de définir des animations plus complexes en spécifiant les valeurs des propriétés CSS à différents moments de l'animation.

```css
@keyframes fadeIn {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}

.fade-in {
    animation: fadeIn 1s ease; /* Animation d'une durée de 1 seconde */
}
```
## 7. Transformations

### Transformations 2D et 3D (translate, rotate, scale, skew)

Les transformations permettent de modifier l'apparence d'un élément en le déplaçant, en le faisant pivoter, en le redimensionnant ou en le déformant.

*   `translate`: Déplace l'élément.
*   `rotate`: Fait pivoter l'élément.
*   `scale`: Redimensionne l'élément.
*   `skew`: Déforme l'élément.

```css
.translate {
    transform: translate(50px, 100px); /* Déplace l'élément de 50px à droite et 100px vers le bas */
}

.rotate {
    transform: rotate(45deg); /* Fait pivoter l'élément de 45 degrés */
}

.scale {
    transform: scale(1.2); /* Agrandit l'élément de 20% */
}

.skew {
    transform: skew(30deg, 20deg); /* Déforme l'élément */
}
```
## 8. Sass et Less (Préprocesseurs CSS)

### Variables, Mixins, Nesting

Sass et Less sont des préprocesseurs CSS qui ajoutent des fonctionnalités supplémentaires au CSS, telles que les variables, les mixins et le nesting.

*   **Variables**: Permettent de stocker des valeurs réutilisables.
*   **Mixins**: Permettent de définir des blocs de code réutilisables.
*   **Nesting**: Permet d'imbriquer les sélecteurs CSS.

```scss
/* Variables */
$primary-color: blue;
$font-size: 16px;

/* Mixin */
@mixin button-style {
    background-color: $primary-color;
    color: white;
    font-size: $font-size;
    padding: 10px 20px;
}

/* Nesting */
nav {
    ul {
        list-style: none;
        li {
            a {
                color: $primary-color;
            }
        }
    }
}

button {
    @include button-style; /* Utilisation du mixin */
}
```

### Compilation

Les fichiers Sass et Less doivent être compilés en CSS avant de pouvoir être utilisés dans un navigateur.

```bash
# Compilation d'un fichier Sass
sass style.scss style.css

# Compilation d'un fichier Less
lessc style.less style.css
```
## 9. Méthodologies CSS

### BEM, OOCSS, SMACSS

Les méthodologies CSS sont des ensembles de règles et de conventions qui permettent d'organiser et de structurer le code CSS de manière à le rendre plus maintenable et réutilisable.

*   **BEM (Block, Element, Modifier)**: Divise l'interface utilisateur en blocs indépendants, en éléments à l'intérieur de ces blocs et en modificateurs qui changent l'apparence des blocs ou des éléments.
*   **OOCSS (Object-Oriented CSS)**: Encourage la création d'objets CSS réutilisables qui peuvent être combinés pour créer des interfaces utilisateur complexes.
*   **SMACSS (Scalable and Modular Architecture for CSS)**: Divise le code CSS en cinq catégories : base, layout, module, state et theme.

```css
/* BEM */
.block {
}

.block__element {
}

.block--modifier {
}

/* Exemple */
.button {
    background-color: blue;
    color: white;
}

.button__label {
    font-size: 16px;
}

.button--primary {
    background-color: red;
}
```
## 10. Bonnes Pratiques

### Organisation du code CSS

*   Utiliser une structure de fichiers claire et cohérente.
*   Diviser le code CSS en modules réutilisables.
*   Utiliser des commentaires pour expliquer le code.
*   Éviter les sélecteurs trop spécifiques.
*   Utiliser des variables et des mixins pour éviter la duplication de code.

### Commentaires

*   Expliquer le but du code.
*   Décrire les relations entre les différents modules.
*   Indiquer les dépendances.

### Performance

*   Minifier le code CSS.
*   Utiliser des sprites CSS pour réduire le nombre de requêtes HTTP.
*   Éviter les règles CSS trop complexes.
*   Utiliser la propriété `will-change` pour améliorer les performances des animations.
## 11. Outils de Développement

### Inspecteur de navigateur

L'inspecteur de navigateur permet d'inspecter et de modifier le code CSS en temps réel.

*   Chrome DevTools
*   Firefox Developer Tools

### Validateurs CSS

Les validateurs CSS permettent de vérifier la syntaxe du code CSS et de détecter les erreurs.

*   [CSS Validator](https://jigsaw.w3.org/css-validator/)
## 12. Ressources et Communauté

### Documentation MDN Web Docs

La documentation MDN Web Docs est une ressource complète pour apprendre le CSS.

*   [MDN Web Docs CSS](https://developer.mozilla.org/fr/docs/Web/CSS)

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/css)](https://www.reddit.com/r/css/)

---
title: Layout CSS moderne - Flexbox expliqué simplement
tags:
  - CSS
  - Flexbox
  - Layout
draft: false
---
# Article 4 : Layout CSS moderne - Flexbox expliqué simplement

## Introduction

Avant l'arrivée de Flexbox et Grid, créer des mises en page complexes et réactives avec CSS était souvent un défi. Les méthodes traditionnelles, basées sur les flottants (`float`), le positionnement (`position`), ou le `display: inline-block`, pouvaient rapidement devenir compliquées à gérer, notamment pour l'alignement vertical ou la distribution d'espace dynamique. Flexbox a révolutionné la manière dont nous pensons le layout unidimensionnel (soit en ligne, soit en colonne), offrant une solution beaucoup plus intuitive et puissante pour aligner et distribuer l'espace entre les éléments d'un conteneur. Cet article va vous guider à travers les concepts fondamentaux de Flexbox pour vous permettre de créer des layouts flexibles et modernes.

## Contenu principal

### Concepts fondamentaux de Flexbox

Flexbox, de son nom complet "Flexible Box Module", est conçu pour disposer les éléments dans une seule dimension, soit une ligne, soit une colonne. Il fonctionne autour de deux types d'éléments :

*   **Le conteneur flex :** C'est l'élément parent auquel on applique `display: flex` ou `display: inline-flex`. Il devient alors un conteneur flex et ses enfants directs deviennent des éléments flex. C'est sur ce conteneur que l'on définit les propriétés qui affectent tous les éléments flex qu'il contient.
*   **Les éléments flex :** Ce sont les enfants directs du conteneur flex. Ce sont ces éléments que Flexbox va disposer et aligner. On peut également leur appliquer des propriétés individuelles.

Le cœur de Flexbox repose sur le concept d'axes :

*   **L'axe principal (main axis) :** C'est l'axe le long duquel les éléments flex sont disposés. Sa direction est déterminée par la propriété `flex-direction` sur le conteneur flex. Par défaut, il est horizontal (de gauche à droite).
*   **L'axe secondaire (cross axis) :** C'est l'axe perpendiculaire à l'axe principal. Il est utilisé pour aligner les éléments flex par rapport à cet axe. Par défaut, si l'axe principal est horizontal, l'axe secondaire est vertical (de haut en bas).

Comprendre ces deux axes est crucial car la plupart des propriétés Flexbox alignent les éléments soit le long de l'axe principal, soit le long de l'axe secondaire.

### Propriétés du conteneur flex

Ce sont les propriétés que l'on applique à l'élément parent qui a `display: flex`.

*   `display: flex;` ou `display: inline-flex;`: Transforme un élément en conteneur flex. `flex` crée un conteneur de type bloc, `inline-flex` crée un conteneur de type en ligne.
*   `flex-direction`: Définit la direction de l'axe principal.
    *   `row` (par défaut) : de gauche à droite.
    *   `row-reverse` : de droite à gauche.
    *   `column` : de haut en bas.
    *   `column-reverse` : de bas en haut.
*   `flex-wrap`: Spécifie si les éléments flex doivent passer à la ligne si l'espace manque.
    *   `nowrap` (par défaut) : les éléments restent sur une seule ligne (et peuvent déborder).
    *   `wrap` : les éléments passent à la ligne suivante si nécessaire.
    *   `wrap-reverse` : les éléments passent à la ligne précédente si nécessaire.
*   `justify-content`: Aligne les éléments flex le long de l'axe principal.
    *   `flex-start` (par défaut) : alignés au début de l'axe principal.
    *   `flex-end` : alignés à la fin de l'axe principal.
    *   `center` : centrés sur l'axe principal.
    *   `space-between` : les éléments sont répartis uniformément sur la ligne, le premier élément étant au début et le dernier à la fin.
    *   `space-around` : les éléments sont répartis uniformément sur la ligne avec un espace égal autour d'eux.
    *   `space-evenly` : les éléments sont répartis de manière à ce que l'espace entre deux éléments soit le même (y compris l'espace aux bords).
*   `align-items`: Aligne les éléments flex le long de l'axe secondaire *lorsqu'ils sont sur une seule ligne* (ou pour chaque ligne si `flex-wrap` est utilisé).
    *   `stretch` (par défaut) : les éléments s'étirent pour remplir le conteneur sur l'axe secondaire.
    *   `flex-start` : alignés au début de l'axe secondaire.
    *   `flex-end` : alignés à la fin de l'axe secondaire.
    *   `center` : centrés sur l'axe secondaire.
    *   `baseline` : alignés sur la ligne de base de leur contenu texte.
*   `align-content`: Aligne les lignes de flexbox le long de l'axe secondaire *lorsqu'il y a plusieurs lignes* (`flex-wrap: wrap`). N'a pas d'effet si le conteneur n'a qu'une seule ligne d'éléments.
    *   `stretch` (par défaut) : les lignes s'étirent pour remplir l'espace restant.
    *   `flex-start` : les lignes sont regroupées au début de l'axe secondaire.
    *   `flex-end` : les lignes sont regroupées à la fin de l'axe secondaire.
    *   `center` : les lignes sont centrées sur l'axe secondaire.
    *   `space-between` : les lignes sont uniformément réparties sur l'axe secondaire, la première étant au début et la dernière à la fin.
    *   `space-around` : les lignes sont uniformément réparties avec un espace égal autour d'elles.

### Propriétés des éléments flex

Ce sont les propriétés que l'on applique directement aux enfants du conteneur flex.

*   `flex-grow`: Définit la capacité d'un élément flex à grandir pour occuper l'espace disponible sur l'axe principal. C'est un facteur sans unité. Un facteur de 1 permet à l'élément de prendre tout l'espace restant s'il est le seul avec `flex-grow > 0`.
*   `flex-shrink`: Définit la capacité d'un élément flex à rétrécir pour éviter le dépassement du conteneur. Un facteur de 1 (par défaut) permet à l'élément de rétrécir si nécessaire. Un facteur de 0 empêche l'élément de rétrécir.
*   `flex-basis`: Définit la taille initiale d'un élément flex *avant* que l'espace restant ne soit distribué. Peut être une valeur de longueur (`px`, `%`, `em`, etc.) ou le mot clé `auto` (qui utilise la taille du contenu). Par défaut, c'est `auto`.
*   `flex`: Une notation raccourcie pour `flex-grow`, `flex-shrink`, et `flex-basis` (dans cet ordre). La valeur par défaut est `0 1 auto`. Les valeurs courantes sont :
    *   `flex: auto;` équivaut à `1 1 auto`.
    *   `flex: initial;` équivaut à `0 1 auto`.
    *   `flex: none;` équivaut à `0 0 auto`.
    *   `flex: 1;` équivaut à `1 1 0`.
*   `align-self`: Permet de surcharger l'alignement défini par `align-items` pour un élément flex spécifique le long de l'axe secondaire. Accepte les mêmes valeurs que `align-items`.
*   `order`: Spécifie l'ordre visuel des éléments flex. Par défaut, les éléments sont affichés dans l'ordre du document source (`order: 0`). Les éléments avec un `order` plus faible apparaissent avant ceux avec un `order` plus élevé.

## En pratique

Flexbox excelle dans les scénarios où vous devez aligner des éléments sur une seule ligne ou colonne et contrôler leur répartition d'espace.

*   **Création d'une barre de navigation responsive :** Une barre de navigation est un cas d'utilisation classique. On applique `display: flex` au conteneur `ul`. On utilise `justify-content` pour répartir les éléments `li` (les liens) et `align-items` pour les centrer verticalement. Avec `flex-wrap: wrap`, la navigation peut passer sur plusieurs lignes sur des écrans plus petits.

    ```html
    <nav>
      <ul>
        <li><a href="#">Accueil</a></li>
        <li><a href="#">À propos</a></li>
        <li><a href="#">Services</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>

    <style>
      nav ul {
        display: flex;
        list-style: none;
        padding: 0;
        justify-content: space-around; /* ou space-between, flex-start, center */
        align-items: center; /* centre les éléments verticalement */
        flex-wrap: wrap; /* permet aux éléments de passer à la ligne */
      }
      nav li {
        margin: 10px;
      }
    </style>
    ```

*   **Centrage vertical et horizontal parfait :** C'est un problème classique qui devient trivial avec Flexbox. Pour centrer un élément (l'enfant) dans un autre (le parent), il suffit d'appliquer `display: flex; justify-content: center; align-items: center;` au conteneur parent.

    ```html
    <div class="conteneur">
      <div class="element-a-centrer">
        Je suis centré !
      </div>
    </div>

    <style>
      .conteneur {
        display: flex;
        justify-content: center; /* Centre horizontalement */
        align-items: center; /* Centre verticalement */
        height: 200px; /* Exemple de hauteur pour le conteneur */
        border: 1px solid black;
      }
    </style>
    ```

*   **Layouts complexes avec imbrication de conteneurs flex :** Bien que Flexbox soit unidimensionnel, on peut créer des layouts complexes en imbriquant des conteneurs flex. Par exemple, une mise en page classique avec un en-tête, une barre latérale et un contenu principal peut être réalisée en utilisant Flexbox pour l'axe principal (rangées) et en appliquant ensuite Flexbox aux éléments de ces rangées pour gérer l'axe secondaire (colonnes) si nécessaire.

## Conclusion

Flexbox est un outil indispensable pour le layout CSS moderne. Il simplifie grandement l'alignement, la distribution d'espace et la création d'interfaces réactives unidimensionnelles. En maîtrisant les concepts de conteneur et éléments flex, ainsi que les axes principal et secondaire, vous serez en mesure de créer des composants et des sections de page flexibles et robustes.

Bien que puissant, Flexbox n'est pas une solution universelle. Pour les layouts bidimensionnels (lignes *et* colonnes en même temps, comme un tableau ou une grille complexe), CSS Grid est souvent plus approprié. Souvent, les deux sont utilisés conjointement, Flexbox pour aligner des éléments *dans* les cellules d'une grille, par exemple.

Le support des navigateurs pour Flexbox est excellent aujourd'hui. Cependant, il est toujours bon de tester vos layouts sur différents navigateurs et appareils pour assurer une compatibilité parfaite.

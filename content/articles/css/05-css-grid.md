---
title: CSS Grid , Créez des layouts complexes en toute simplicité
tags:
  - CSS
  - Grid
  - Layout
draft: false
---
# CSS Grid : Créez des layouts complexes en toute simplicité

## Introduction

Après avoir découvert la puissance de Flexbox pour aligner des éléments sur un seul axe, il est temps d'aborder un autre outil fondamental pour les mises en page web complexes : CSS Grid Layout, ou simplement CSS Grid.

Alors que Flexbox est conçu pour la distribution d'éléments sur un seul axe (ligne *ou* colonne), Grid est une solution bidimensionnelle (2D). Elle vous permet de structurer votre contenu en lignes *et* en colonnes simultanément. C'est ce qui rend Grid particulièrement adapté à la création de la structure globale d'une page, comme l'en-tête, le pied de page, la barre latérale et la zone de contenu principal.

Comprendre Grid est crucial pour maîtriser les techniques de layout modernes et construire des interfaces utilisateur robustes et flexibles.

## Contenu principal

CSS Grid fonctionne en définissant une grille sur un élément conteneur, puis en plaçant les éléments enfants de ce conteneur dans les cellules de cette grille.

### Concepts de base de CSS Grid

-   **Conteneur grid :** L'élément parent sur lequel vous appliquez `display: grid`. C'est lui qui définit la grille.
-   **Éléments grid :** Les enfants directs du conteneur grid. Ce sont eux qui seront placés dans la grille.
-   **Lignes (Rows) et colonnes (Columns) :** Les axes principaux de la grille. Vous définissez leur nombre et leur taille.
-   **Cellules (Cells) :** L'intersection d'une ligne et d'une colonne. C'est l'unité de base où les éléments sont placés.
-   **Zones (Areas) :** Vous pouvez nommer et regrouper plusieurs cellules pour former des zones rectangulaires, ce qui facilite le placement des éléments.

### Propriétés du conteneur grid

Ce sont les propriétés appliquées à l'élément sur lequel `display: grid` est défini :

-   `display: grid;`: Transforme l'élément en un conteneur grid.
-   `grid-template-columns` et `grid-template-rows`: Définissent la structure explicite de la grille en termes de colonnes et de lignes. Vous spécifiez la taille de chaque piste (colonne ou ligne) en utilisant des unités comme `px`, `%`, `auto`, ou la nouvelle unité `fr` (fraction de l'espace disponible).
    ```html
    .container {
      display: grid;
      grid-template-columns: 1fr 2fr 1fr; /* 3 colonnes: 1/4, 2/4, 1/4 de l'espace */
      grid-template-rows: auto 100px; /* 2 lignes: taille auto, puis 100px */
    }
    ```
-   `grid-template-areas`: Permet de définir des zones nommées dans la grille, rendant le layout plus lisible et plus facile à modifier.
    ```html
    .container {
      display: grid;
      grid-template-columns: 1fr 3fr;
      grid-template-rows: 50px auto 50px;
      grid-template-areas:
        "header header"
        "nav main"
        "footer footer";
    }
    ```
-   `gap` (ou `grid-row-gap`, `grid-column-gap`): Définit l'espace entre les pistes de la grille. `gap` est une notation raccourcie pour les deux.
    ```html
    .container {
      gap: 20px; /* 20px d'espace entre les lignes ET les colonnes */
    }
    ```
-   `justify-items` et `align-items`: Alignent les *contenus* des éléments grid *à l'intérieur de leurs cellules respectives* sur l'axe des colonnes (`justify-items`) et l'axe des lignes (`align-items`).
-   `justify-content` et `align-content`: Alignent la *grille entière* *à l'intérieur du conteneur grid* sur l'axe des colonnes (`justify-content`) et l'axe des lignes (`align-content`), si la grille n'occupe pas tout l'espace disponible.

### Propriétés des éléments grid

Ces propriétés sont appliquées aux enfants directs du conteneur grid :

-   `grid-column` et `grid-row`: Permettent de spécifier où un élément doit commencer et se terminer dans la grille, en faisant référence aux lignes de la grille. Vous pouvez utiliser les numéros de ligne (`grid-column: 1 / 3;` pour couvrir de la ligne 1 à 3, c'est-à-dire la première colonne) ou le mot clé `span` (`grid-column: span 2;` pour couvrir 2 colonnes).
-   `grid-area`: Permet de placer un élément en le faisant correspondre au nom d'une zone définie avec `grid-template-areas`. C'est une alternative très lisible à `grid-column` et `grid-row` pour les layouts complexes.
    ```html
    .header {
      grid-area: header; /* Place cet élément dans la zone nommée "header" */
    }
    ```
-   `justify-self` et `align-self`: Permettent d'aligner un *élément grid individuel* *à l'intérieur de sa propre cellule* sur l'axe des colonnes (`justify-self`) et l'axe des lignes (`align-self`).

### Fonctions spéciales utiles

-   `repeat(nombre, taille)`: Répète une définition de piste plusieurs fois. Par exemple, `repeat(3, 1fr)` est équivalent à `1fr 1fr 1fr`.
-   `minmax(min, max)`: Définit une taille de piste qui est au minimum `min` et au maximum `max`. Utile pour créer des pistes flexibles qui ne deviennent pas trop petites ou trop grandes.
-   `fr` (unité fractionnaire): Une unité qui représente une fraction de l'espace disponible dans le conteneur grid. L'espace disponible est calculé après que les éléments avec des tailles fixes ou automatiques ont été placés.
-   `auto-fill` et `auto-fit` (souvent utilisés avec `repeat` et `minmax`): Permettent de créer des grilles fluides et responsives sans définir explicitement le nombre de colonnes ou de lignes. La grille remplit ou ajuste automatiquement le nombre d'éléments par ligne en fonction de la taille du conteneur.

## En pratique

La meilleure façon d'apprendre Grid est de l'utiliser. Commencez par des exemples simples, comme créer une disposition de carte en 2 colonnes, puis progressez vers des layouts de page plus complexes utilisant `grid-template-areas`.

Les outils de développement de votre navigateur sont indispensables. Ils possèdent une vue spéciale pour visualiser les grilles, montrer les numéros de ligne, les espaces et les zones nommées. C'est un excellent moyen de déboguer et de comprendre comment votre grille fonctionne.

CSS Grid, combiné avec l'unité `fr` et les fonctions `repeat`/`minmax` avec `auto-fill`/`auto-fit`, permet de créer des grilles *responsives* avec très peu, voire pas du tout, de media queries pour les changements de layout fondamentaux.

## Conclusion

CSS Grid est un outil puissant et moderne pour créer des layouts bidimensionnels sur le web. Il est idéal pour la structure globale d'une page ou des sections complexes. Bien qu'il soit différent de Flexbox, ils ne sont pas en concurrence mais se complètent mutuellement. Flexbox reste excellent pour aligner des éléments sur un seul axe (par exemple, les éléments d'une barre de navigation ou les éléments à l'intérieur d'une cellule de grille), tandis que Grid excelle dans la création de la structure globale en 2D.

Maîtriser Grid, c'est ouvrir la porte à des possibilités de layout beaucoup plus flexibles et maintenables. N'oubliez pas d'utiliser les outils de développement de votre navigateur pour visualiser et comprendre vos grilles !

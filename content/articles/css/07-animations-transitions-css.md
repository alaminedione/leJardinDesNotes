---
title: Animations et transitions CSS , Donnez vie à vos interfaces
tags:
  - CSS
  - Animations
  - Transitions
draft: false
---
# Animations et transitions CSS : Donnez vie à vos interfaces

## Introduction

Dans le développement web moderne, l'apparence statique ne suffit plus. Les utilisateurs s'attendent à des interfaces dynamiques et réactives. Les animations et transitions CSS sont des outils puissants pour ajouter du mouvement, améliorer l'expérience utilisateur (UX) et rendre vos sites web plus engageants et intuitifs. Elles permettent de guider l'œil de l'utilisateur, de fournir un feedback visuel après une interaction, ou simplement d'ajouter une touche de personnalité.

Cet article explore comment utiliser les transitions et les animations avec CSS pur, sans nécessiter de JavaScript pour des effets simples à modérés. Nous verrons les propriétés clés pour chaque type d'animation et comment les mettre en œuvre en pratique.

## Contenu principal

CSS offre deux mécanismes principaux pour créer du mouvement : les **transitions** et les **animations**.

### Transitions CSS

Les transitions permettent de créer un changement fluide entre un état initial et un état final d'une propriété CSS lorsqu'un événement se produit (par exemple, survol de la souris, focus, modification de classe). Elles sont parfaites pour des changements simples et interactifs.

Une transition est définie en spécifiant quelle propriété doit être animée, combien de temps doit durer l'animation, et comment elle doit progresser.

*   `transition-property`: Spécifie le nom de la propriété CSS sur laquelle appliquer une transition (par exemple, `color`, `opacity`, `transform`). La valeur `all` (par défaut) applique la transition à toutes les propriétés qui changent.
*   `transition-duration`: Définit la durée de la transition en secondes (`s`) ou en millisecondes (`ms`). C'est la seule propriété obligatoire pour qu'une transition se déclenche.
*   `transition-timing-function`: Définit la courbe de vitesse de l'animation (comment l'animation progresse dans le temps). Les valeurs courantes incluent `ease` (par défaut, démarre lentement, accélère au milieu, ralentit à la fin), `linear` (vitesse constante), `ease-in` (démarre lentement), `ease-out` (finit lentement), `ease-in-out` (démarre et finit lentement). Nous explorerons cela plus en détail plus bas.
*   `transition-delay`: Définit un délai avant que la transition ne commence, en secondes (`s`) ou millisecondes (`ms`).

Il existe également une **notation raccourcie** `transition` qui combine toutes ces propriétés dans l'ordre : `transition: [property] [duration] [timing-function] [delay];`

Exemple :

```css
.button {
  background-color: blue;
  transition-property: background-color, transform; /* Transition sur la couleur de fond et la transformation */
  transition-duration: 0.3s; /* Dure 0.3 secondes */
  transition-timing-function: ease-in-out; /* Accélère puis ralentit */
}

.button:hover {
  background-color: navy;
  transform: scale(1.1); /* Change la taille au survol */
}
```

### Animations CSS

Les animations CSS permettent de créer des séquences d'animation plus complexes et plus contrôlées que les transitions. Elles ne nécessitent pas un changement d'état déclencheur (comme un `:hover`), mais peuvent démarrer dès le chargement de la page ou lorsqu'un élément est ajouté au DOM. Les animations sont définies à l'aide de la règle `@keyframes`.

La règle `@keyframes` définit les étapes (ou "keyfr**ames**") d'une animation. Chaque keyframe représente un pourcentage de la durée totale de l'animation, indiquant l'état des propriétés CSS à ce moment précis. Vous devez toujours définir les états `0%` (début, équivalent à `from`) et `100%` (fin, équivalent à `to`).

```css
@keyframes slidein {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(100px);
  }
}
/* ou */
@keyframes fadeout {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
```

Une fois les `@keyframes` définis, vous devez appliquer cette animation à un élément CSS en utilisant les propriétés d'animation :

*   `animation-name`: Le nom de l'animation définie avec `@keyframes`.
*   `animation-duration`: La durée de l'animation (obligatoire).
*   `animation-timing-function`: La courbe de vitesse de l'animation (comme pour les transitions).
*   `animation-delay`: Un délai avant le début de l'animation.
*   `animation-iteration-count`: Combien de fois l'animation doit se répéter. `infinite` pour une boucle sans fin.
*   `animation-direction`: Définit si l'animation doit jouer en avant (`normal`), en arrière (`reverse`), ou alterner entre avant et arrière (`alternate`, `alternate-reverse`).
*   `animation-fill-mode`: Définit l'état de l'élément avant le début de l'animation (`backwards`), après la fin (`forwards`), ou les deux (`both`). Par défaut, l'élément retrouve son état CSS normal après l'animation (`none`).
*   `animation-play-state`: Permet de mettre l'animation en pause (`paused`) ou de la reprendre (`running`). Utile pour le contrôle via JavaScript ou des pseudo-classes (ex: `:hover`).

Là aussi, une **notation raccourcie** `animation` est disponible : `animation: [name] [duration] [timing-function] [delay] [iteration-count] [direction] [fill-mode] [play-state];` (L'ordre des propriétés est important pour `duration` et `delay`, le premier nombre est la durée, le second le délai si présent).

Exemple d'application :

```css
.element {
  animation-name: slidein;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

### Fonctions de timing

Les fonctions de timing (ou fonctions d'accélération) définissent comment la vitesse d'une animation change au cours du temps.

*   `linear`: La vitesse est constante du début à la fin.
*   `ease` (par défaut) : L'animation démarre lentement, accélère au milieu, et ralentit à la fin.
*   `ease-in`: L'animation démarre lentement et accélère vers la fin.
*   `ease-out`: L'animation démarre rapidement et ralentit vers la fin.
*   `ease-in-out`: L'animation démarre et finit lentement, avec une vitesse maximale au milieu.
*   `cubic-bezier(n, n, n, n)`: Vous permet de définir votre propre courbe de vitesse à l'aide d'une fonction cubique de Bézier. Très flexible pour créer des effets personnalisés. De nombreux générateurs en ligne existent pour vous aider.
*   `steps(nombre, position)`: Divise l'animation en un nombre défini d'étapes de durée égale. Utile pour des animations de sprite ou des compteurs. `position` peut être `start` ou `end`.

### Propriétés animables

Toutes les propriétés CSS ne peuvent pas être animées. Seules les propriétés dont la valeur peut être interpolée (c'est-à-dire passer graduellement d'une valeur à une autre) sont animables.

Exemples de propriétés couramment animables :
*   Propriétés de couleur (`color`, `background-color`, `border-color`)
*   Propriétés de taille/position (`width`, `height`, `top`, `left`, `right`, `bottom`)
*   Propriétés de typographie (`font-size`, `letter-spacing`, `line-height`)
*   Transformations (`transform`: `translate`, `rotate`, `scale`, `skew`) - **Très performantes** car elles n'affectent pas le flux du document et sont gérées par le GPU.
*   Opacité (`opacity`) - **Très performante**.
*   Ombres (`box-shadow`, `text-shadow`)
*   Filtres (`filter`)

Propriétés qui ne sont généralement PAS animables : `display`, `position`, `float`, `margin-top`/`bottom` sur les éléments inline, etc. Animer des propriétés comme `width` ou `height` sur de nombreux éléments ou des propriétés qui déclenchent des reflows coûteux (`margin`, `padding`) peut impacter les performances. Préférez l'animation des propriétés `opacity` et `transform` lorsque possible.

## En pratique

### Création d'effets de survol interactifs

Les transitions sont parfaites pour ajouter des effets subtils et réactifs sur les états `:hover`, `:focus`, ou `:active`.

```html
<button class="interactive-button">Passez la souris</button>

<style>
  .interactive-button {
    padding: 10px 20px;
    font-size: 1em;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.1s ease-out; /* Transition sur 2 propriétés */
  }

  .interactive-button:hover {
    background-color: #0056b3; /* Changement de couleur au survol */
    transform: translateY(-2px); /* Léger déplacement vers le haut */
  }

  .interactive-button:active {
    background-color: #004085;
    transform: translateY(0); /* Revient à la position initiale au clic */
  }
</style>
```

### Animation d'un loader ou spinner

Les animations `@keyframes` sont idéales pour créer des éléments qui bouclent continuellement, comme les indicateurs de chargement.

```html
<div class="loader"></div>

<style>
  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  .loader {
    border: 4px solid #f3f3f3; /* Gris clair */
    border-top: 4px solid #3498db; /* Bleu */
    border-radius: 50%; /* Forme ronde */
    width: 40px;
    height: 40px;
    animation: spin 2s linear infinite; /* Applique l\'animation */
    margin: 20px; /* Juste pour l\'exemple de mise en page */
  }
</style>
```

### Séquence d'animations complexe

En utilisant plusieurs keyframes ou en combinant des délais, vous pouvez créer des séquences.

```html
<div class="sequenced-element"></div>

<style>
  @keyframes pulse-color {
    0% { background-color: red; }
    50% { background-color: blue; }
    100% { background-color: red; }
  }

  @keyframes move-fade {
    0% { transform: translateX(0) rotate(0deg); opacity: 1; }
    50% { transform: translateX(50px) rotate(180deg); opacity: 0.5; }
    100% { transform: translateX(100px) rotate(360deg); opacity: 0; }
  }

  .sequenced-element {
    width: 50px;
    height: 50px;
    margin: 20px;
    animation-name: pulse-color, move-fade; /* Applique deux animations simultanément */
    animation-duration: 3s, 5s; /* Durées différentes */
    animation-timing-function: ease-in-out, linear; /* Timing functions différentes */
    animation-iteration-count: infinite, 1; /* Boucle sur la couleur, une seule fois pour le mouvement/fade */
    animation-delay: 0s, 0.5s; /* Le mouvement commence après 0.5s */
  }
</style>
```

## Conclusion

Les animations et transitions CSS sont des outils puissants pour rendre vos interfaces plus vivantes et interactives. Les transitions sont idéales pour des changements d'état simples et déclenchés par l'utilisateur, tandis que les animations basées sur `@keyframes` permettent des séquences de mouvement plus complexes et autonomes.

En privilégiant l'animation des propriétés `opacity` et `transform`, vous pouvez obtenir des animations fluides et performantes qui sont gérées par le GPU du client. Soyez attentif à l'impact de l'animation sur les performances si vous animez des propriétés qui affectent le layout ou la peinture de nombreux éléments.

### Bonnes pratiques pour les animations

*   **Performance :** Animez les propriétés `opacity` et `transform` autant que possible. Utilisez `will-change` (avec parcimonie) pour indiquer au navigateur les propriétés qui vont être animées et potentiellement l'aider à optimiser.
*   **Subtilité :** Les animations doivent améliorer l'UX, pas la gêner. Évitez les animations excessives, clignotantes ou trop longues qui pourraient distraire ou frustrer l'utilisateur.
*   **Cohérence :** Utilisez des durées, des timings et des styles d'animation cohérents sur tout votre site pour une expérience utilisateur harmonieuse.
*   **Accessibilité :** C'est un point crucial.

### Accessibilité et réduction des mouvements

Les animations peuvent provoquer de la fatigue oculaire, des vertiges ou même des crises pour les personnes souffrant de troubles vestibulaires ou d'épilepsie. Il est essentiel de respecter les préférences de l'utilisateur. Le CSS propose la média query `prefers-reduced-motion`:

```css
@media (prefers-reduced-motion: reduce) {
  /* Désactive ou réduit drastiquement les animations complexes */
  .element-to-animate {
    animation: none !important; /* Supprime l'animation */
    transition: none !important; /* Supprime la transition */
    /* Ou appliquez un style statique */
    opacity: 1 !important;
    transform: none !important;
  }
}
```

Utiliser cette média query vous permet de proposer des animations par défaut, mais de les désactiver ou de les simplifier pour les utilisateurs qui l'ont spécifié dans les paramètres de leur système d'exploitation. C'est une pratique indispensable pour un web inclusif.

Dans les prochains articles, nous explorerons d'autres aspects du CSS moderne, comme les variables CSS, l'architecture CSS et les préprocesseurs, qui vous aideront à écrire un code plus efficace et maintenable.

---
title: HTML
draft: false
tags:
  - html
  - markup
description: Langage de balisage standard pour créer des pages web et structurer leur contenu.
---

## Sommaire

1.  Introduction à HTML
    *   Qu'est-ce que HTML ?
    *   Historique et versions (HTML5)
    *   Structure de base d'un document HTML
    *   Éditeurs de texte et navigateurs web
2.  Structure de Base d'une Page HTML
    *   Déclaration `<!DOCTYPE html>`
    *   Balises `<html>`, `<head>`, `<body>`
    *   Balise `<title>`
    *   Balises de métadonnées (`<meta>`)
    *   Lien vers des feuilles de style (`<link>`) et des scripts (`<script>`)
3.  Éléments de Texte
    *   Titres (`<h1>` à `<h6>`)
    *   Paragraphes (`<p>`)
    *   Sauts de ligne (`<br>`) et lignes horizontales (`<hr>`)
    *   Mise en forme du texte (gras, italique, souligné - `<strong>`, `<em>`, `<u>`)
    *   Citations (`<blockquote>`, `<q>`)
    *   Code (`<code>`, `<pre>`)
4.  Liens Hypertextes
    *   Création de liens (`<a>`)
    *   Liens internes et externes
    *   Ancres
5.  Images
    *   Insertion d'images (`<img>`)
    *   Attributs (src, alt, width, height)
    *   Formats d'image (JPEG, PNG, GIF, SVG)
6.  Listes
    *   Listes non ordonnées (`<ul>`, `<li>`)
    *   Listes ordonnées (`<ol>`, `<li>`)
    *   Listes de description (`<dl>`, `<dt>`, `<dd>`)
7.  Tableaux
    *   Création de tableaux (`<table>`, `<tr>`, `<th>`, `<td>`)
    *   Fusion de cellules (colspan, rowspan)
    *   En-tête, corps et pied de tableau (`<thead>`, `<tbody>`, `<tfoot>`)
8.  Formulaires
    *   Création de formulaires (`<form>`)
    *   Champs de saisie (`<input>` - text, password, checkbox, radio, submit, etc.)
    *   Zones de texte (`<textarea>`)
    *   Listes déroulantes (`<select>`, `<option>`)
    *   Boutons (`<button>`)
    *   Attributs de formulaire (action, method)
9.  Éléments Sémantiques (HTML5)
    *   `<header>`, `<nav>`, `<article>`, `<aside>`, `<footer>`, `<section>`
10. Multimédia
    *   Insertion de vidéos (`<video>`)
    *   Insertion d'audio (`<audio>`)
    *   Intégration de contenu externe (`<iframe>`)
11. Accessibilité (ARIA)
    *   Attributs ARIA
    *   Bonnes pratiques pour l'accessibilité
12. Bonnes Pratiques et Validation
    *   Structure du code
    *   Validation HTML
13. Ressources et Communauté
    *   Documentation MDN Web Docs
    *   Communautés en ligne
## 1. Introduction à HTML

### Qu'est-ce que HTML ?

HTML (HyperText Markup Language) est le langage de balisage standard pour créer des pages web et structurer leur contenu. Il est utilisé pour définir la structure et le contenu d'une page web, tels que le texte, les images, les liens et les formulaires.

### Historique et versions (HTML5)

*   HTML a été créé par Tim Berners-Lee en 1990.
*   HTML5 est la dernière version majeure de HTML, publiée en 2014.
*   HTML5 a introduit de nouvelles fonctionnalités telles que les éléments sémantiques, le support multimédia et les API pour les applications web.

### Structure de base d'un document HTML

Un document HTML de base se compose des éléments suivants :

*   `<!DOCTYPE html>` : Déclaration du type de document.
*   `<html>` : Élément racine du document.
*   `<head>` : Contient les métadonnées du document (titre, liens vers les feuilles de style, etc.).
*   `<body>` : Contient le contenu visible de la page web.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Ma Page Web</title>
</head>
<body>
    <h1>Bienvenue sur ma page web !</h1>
    <p>Ceci est un paragraphe de texte.</p>
</body>
</html>
```

### Éditeurs de texte et navigateurs web

*   Éditeurs de texte : Logiciels utilisés pour écrire le code HTML (ex: VS Code, Sublime Text, Notepad++).
*   Navigateurs web : Logiciels utilisés pour afficher les pages web (ex: Chrome, Firefox, Safari).

## 2. Structure de Base d'une Page HTML

### Déclaration `<!DOCTYPE html>`

*   Indique au navigateur la version de HTML utilisée dans le document.
*   Doit être la première ligne du document HTML.

### Balises `<html>`, `<head>`, `<body>`

*   `<html>` : Élément racine du document HTML.
*   `<head>` : Contient les métadonnées du document (titre, liens vers les feuilles de style, etc.).
*   `<body>` : Contient le contenu visible de la page web.

### Balise `<title>`

*   Définit le titre de la page web, affiché dans l'onglet du navigateur.
*   Doit être placée à l'intérieur de la balise `<head>`.

### Balises de métadonnées (`<meta>`)

*   Fournissent des informations sur le document (description, mots-clés, auteur, etc.).
*   Sont utilisées par les moteurs de recherche et les navigateurs web.
*   Doivent être placées à l'intérieur de la balise `<head>`.

```html
<meta charset="UTF-8">
<meta name="description" content="Description de ma page web">
<meta name="keywords" content="HTML, CSS, JavaScript">
<meta name="author" content="John Doe">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Lien vers des feuilles de style (`<link>`) et des scripts (`<script>`)

*   `<link>` : Permet de lier une feuille de style CSS au document HTML.
*   `<script>` : Permet d'inclure du code JavaScript dans le document HTML.
*   Doivent être placés à l'intérieur de la balise `<head>` (pour les feuilles de style) ou à la fin de la balise `<body>` (pour les scripts).

```html
<link rel="stylesheet" href="style.css">
<script src="script.js"></script>
```
## 3. Éléments de Texte

### Titres (`<h1>` à `<h6>`)

*   Utilisés pour définir les titres et sous-titres de la page web.
*   `<h1>` est le titre le plus important, `<h6>` est le moins important.

```html
<h1>Titre principal</h1>
<h2>Sous-titre</h2>
<h3>Sous-sous-titre</h3>
```

### Paragraphes (`<p>`)

*   Utilisés pour définir les paragraphes de texte.

```html
<p>Ceci est un paragraphe de texte.</p>
```

### Sauts de ligne (`<br>`) et lignes horizontales (`<hr>`)

*   `<br>` : Insère un saut de ligne.
*   `<hr>` : Insère une ligne horizontale.

```html
<p>Ceci est une ligne.<br>Ceci est une autre ligne.</p>
<hr>
```

### Mise en forme du texte (gras, italique, souligné - `<strong>`, `<em>`, `<u>`)

*   `<strong>` : Met le texte en gras (importance sémantique).
*   `<em>` : Met le texte en italique (emphase sémantique).
*   `<u>` : Souligne le texte (à éviter, car peut être confondu avec un lien).

```html
<p>Ceci est un texte <strong>important</strong>.</p>
<p>Ceci est un texte <em>mis en évidence</em>.</p>
<p>Ceci est un texte <u>souligné</u>.</p>
```

### Citations (`<blockquote>`, `<q>`)

*   `<blockquote>` : Utilisé pour les citations longues (affichées comme un bloc).
*   `<q>` : Utilisé pour les citations courtes (affichées entre guillemets).

```html
<blockquote cite="https://www.example.com">
    Ceci est une citation longue.
</blockquote>

<p>Comme disait l'autre : <q>Ceci est une citation courte.</q></p>
```

### Code (`<code>`, `<pre>`)

*   `<code>` : Utilisé pour afficher du code informatique en ligne.
*   `<pre>` : Utilisé pour afficher du code informatique préformaté (avec indentation et sauts de ligne).

```html
<p>La balise <code>&lt;p&gt;</code> est utilisée pour définir un paragraphe.</p>

<pre>
    <code>
        function myFunction() {
            alert("Hello, World!");
        }
    </code>
</pre>
```
## 4. Liens Hypertextes

### Création de liens (`<a>`)

*   La balise `<a>` (anchor) est utilisée pour créer des liens hypertextes vers d'autres pages web, des fichiers, des emplacements dans la même page, etc.
*   L'attribut `href` spécifie l'URL de la destination du lien.

```html
<a href="https://www.example.com">Visiter Example.com</a>
```

### Liens internes et externes

*   Liens externes : Pointent vers des pages web situées sur d'autres sites web.
*   Liens internes : Pointent vers des pages web situées sur le même site web.

```html
<a href="https://www.example.com">Lien externe</a>
<a href="/about.html">Lien interne</a>
```

### Ancres

*   Permettent de créer des liens vers des sections spécifiques d'une page web.
*   Utilisation de l'attribut `id` pour définir l'ancre de destination.
*   Utilisation du symbole `#` dans l'attribut `href` pour spécifier l'ancre.

```html
<h2>Table des matières</h2>
<ul>
    <li><a href="#introduction">Introduction</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
</ul>

<h2 id="introduction">Introduction</h2>
<p>...</p>

<h2 id="conclusion">Conclusion</h2>
<p>...</p>
```
## 5. Images

### Insertion d'images (`<img>`)

*   La balise `<img>` est utilisée pour insérer des images dans une page web.
*   L'attribut `src` spécifie l'URL de l'image.
*   L'attribut `alt` spécifie un texte alternatif pour l'image (important pour l'accessibilité).

```html
<img src="image.jpg" alt="Description de l'image">
```

### Attributs (src, alt, width, height)

*   `src` : URL de l'image.
*   `alt` : Texte alternatif (description de l'image).
*   `width` : Largeur de l'image (en pixels).
*   `height` : Hauteur de l'image (en pixels).

```html
<img src="image.jpg" alt="Description de l'image" width="500" height="300">
```

### Formats d'image (JPEG, PNG, GIF, SVG)

*   `JPEG` : Format d'image compressé, adapté aux photos.
*   `PNG` : Format d'image non compressé, adapté aux images avec des couleurs vives et des transparences.
*   `GIF` : Format d'image animé (supporte les animations).
*   `SVG` : Format d'image vectoriel, adapté aux logos et aux illustrations.
## 6. Listes

### Listes non ordonnées (`<ul>`, `<li>`)

*   Utilisées pour créer des listes d'éléments sans ordre particulier.
*   La balise `<ul>` (unordered list) définit la liste.
*   La balise `<li>` (list item) définit chaque élément de la liste.

```html
<ul>
    <li>Élément 1</li>
    <li>Élément 2</li>
    <li>Élément 3</li>
</ul>
```

### Listes ordonnées (`<ol>`, `<li>`)

*   Utilisées pour créer des listes d'éléments avec un ordre particulier.
*   La balise `<ol>` (ordered list) définit la liste.
*   La balise `<li>` (list item) définit chaque élément de la liste.

```html
<ol>
    <li>Élément 1</li>
    <li>Élément 2</li>
    <li>Élément 3</li>
</ol>
```

### Listes de description (`<dl>`, `<dt>`, `<dd>`)

*   Utilisées pour créer des listes de définitions.
*   La balise `<dl>` (description list) définit la liste.
*   La balise `<dt>` (description term) définit le terme.
*   La balise `<dd>` (description details) définit la description du terme.

```html
<dl>
    <dt>HTML</dt>
    <dd>Langage de balisage pour créer des pages web.</dd>
    <dt>CSS</dt>
    <dd>Langage de feuille de style pour mettre en forme les pages web.</dd>
</dl>
```
## 7. Tableaux

### Création de tableaux (`<table>`, `<tr>`, `<th>`, `<td>`)

*   La balise `<table>` définit un tableau.
*   La balise `<tr>` (table row) définit une ligne du tableau.
*   La balise `<th>` (table header) définit une cellule d'en-tête du tableau.
*   La balise `<td>` (table data) définit une cellule de données du tableau.

```html
<table>
    <tr>
        <th>Nom</th>
        <th>Âge</th>
    </tr>
    <tr>
        <td>John Doe</td>
        <td>30</td>
    </tr>
    <tr>
        <td>Jane Smith</td>
        <td>25</td>
    </tr>
</table>
```

### Fusion de cellules (colspan, rowspan)

*   L'attribut `colspan` permet de fusionner des cellules horizontalement.
*   L'attribut `rowspan` permet de fusionner des cellules verticalement.

```html
<table>
    <tr>
        <th colspan="2">Informations</th>
    </tr>
    <tr>
        <td>Nom</td>
        <td>John Doe</td>
    </tr>
</table>
```

### En-tête, corps et pied de tableau (`<thead>`, `<tbody>`, `<tfoot>`)

*   `<thead>` : Définit l'en-tête du tableau.
*   `<tbody>` : Définit le corps du tableau.
*   `<tfoot>` : Définit le pied de tableau.

```html
<table>
    <thead>
        <tr>
            <th>Nom</th>
            <th>Âge</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>John Doe</td>
            <td>30</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="2">Source: ...</td>
        </tr>
    </tfoot>
</table>
```
## 8. Formulaires

### Création de formulaires (`<form>`)

*   La balise `<form>` est utilisée pour créer un formulaire HTML.
*   L'attribut `action` spécifie l'URL à laquelle les données du formulaire seront envoyées.
*   L'attribut `method` spécifie la méthode HTTP utilisée pour envoyer les données (GET ou POST).

```html
<form action="/submit" method="post">
    <!-- Champs de formulaire -->
</form>
```

### Champs de saisie (`<input>` - text, password, checkbox, radio, submit, etc.)

*   La balise `<input>` est utilisée pour créer des champs de saisie de différents types.
*   L'attribut `type` spécifie le type de champ de saisie.

```html
<label for="name">Nom:</label><br>
<input type="text" id="name" name="name"><br>

<label for="password">Mot de passe:</label><br>
<input type="password" id="password" name="password"><br>

<input type="checkbox" id="agree" name="agree" value="agree">
<label for="agree">J'accepte les conditions</label><br>

<input type="radio" id="male" name="gender" value="male">
<label for="male">Homme</label>
<input type="radio" id="female" name="gender" value="female">
<label for="female">Femme</label><br>

<input type="submit" value="Envoyer">
```

### Zones de texte (`<textarea>`)

*   La balise `<textarea>` est utilisée pour créer une zone de texte multiligne.

```html
<label for="message">Message:</label><br>
<textarea id="message" name="message" rows="4" cols="50"></textarea>
```

### Listes déroulantes (`<select>`, `<option>`)

*   La balise `<select>` est utilisée pour créer une liste déroulante.
*   La balise `<option>` définit chaque option de la liste déroulante.

```html
<label for="country">Pays:</label><br>
<select id="country" name="country">
    <option value="france">France</option>
    <option value="usa">États-Unis</option>
    <option value="uk">Royaume-Uni</option>
</select>
```

### Boutons (`<button>`)

*   La balise `<button>` est utilisée pour créer un bouton.
*   Peut être utilisée à l'intérieur ou à l'extérieur d'un formulaire.

```html
<button type="button">Cliquez ici</button>
<button type="submit">Envoyer le formulaire</button>
```

### Attributs de formulaire (action, method)

*   `action` : Spécifie l'URL à laquelle les données du formulaire seront envoyées.
*   `method` : Spécifie la méthode HTTP utilisée pour envoyer les données (GET ou POST).

```html
<form action="/submit" method="post">
    <!-- ... -->
</form>
```
## 9. Éléments Sémantiques (HTML5)

### `<header>`, `<nav>`, `<article>`, `<aside>`, `<footer>`, `<section>`

*   HTML5 a introduit de nouveaux éléments sémantiques qui permettent de mieux structurer le contenu d'une page web et d'améliorer l'accessibilité.
*   `<header>` : Définit l'en-tête de la page ou d'une section.
*   `<nav>` : Définit une section de navigation.
*   `<article>` : Définit un article indépendant.
*   `<aside>` : Définit un contenu secondaire (ex: barre latérale).
*   `<footer>` : Définit le pied de page de la page ou d'une section.
*   `<section>` : Définit une section thématique.

```html
<header>
    <h1>Mon Site Web</h1>
    <nav>
        <ul>
            <li><a href="#">Accueil</a></li>
            <li><a href="#">À propos</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
</header>

<article>
    <h2>Titre de l'article</h2>
    <p>Contenu de l'article.</p>
</article>

<aside>
    <h3>Publicité</h3>
    <p>...</p>
</aside>

<footer>
    <p>© 2023 Mon Site Web</p>
</footer>
```
## 10. Multimédia

### Insertion de vidéos (`<video>`)

*   La balise `<video>` est utilisée pour insérer des vidéos dans une page web.
*   L'attribut `src` spécifie l'URL de la vidéo.
*   Les attributs `width` et `height` spécifient la largeur et la hauteur de la vidéo.
*   L'attribut `controls` ajoute des contrôles de lecture à la vidéo.

```html
<video src="video.mp4" width="640" height="360" controls>
    Votre navigateur ne supporte pas la balise vidéo.
</video>
```

### Insertion d'audio (`<audio>`)

*   La balise `<audio>` est utilisée pour insérer de l'audio dans une page web.
*   L'attribut `src` spécifie l'URL de l'audio.
*   L'attribut `controls` ajoute des contrôles de lecture à l'audio.

```html
<audio src="audio.mp3" controls>
    Votre navigateur ne supporte pas la balise audio.
</audio>
```

### Intégration de contenu externe (`<iframe>`)

*   La balise `<iframe>` est utilisée pour intégrer du contenu externe provenant d'autres sites web (ex: vidéos YouTube, cartes Google Maps).
*   L'attribut `src` spécifie l'URL du contenu à intégrer.

```html
<iframe src="https://www.youtube.com/embed/VIDEO_ID" width="560" height="315" frameborder="0" allowfullscreen></iframe>
```
## 11. Accessibilité (ARIA)

### Attributs ARIA

*   ARIA (Accessible Rich Internet Applications) est un ensemble d'attributs HTML qui permettent d'améliorer l'accessibilité des applications web pour les personnes handicapées.
*   Les attributs ARIA fournissent des informations supplémentaires sur le rôle, l'état et les propriétés des éléments HTML.

```html
<button aria-label="Fermer la fenêtre">Fermer</button>
<div role="dialog" aria-labelledby="dialog-title">
    <h2 id="dialog-title">Titre de la fenêtre</h2>
    <!-- Contenu de la fenêtre -->
</div>
```

### Bonnes pratiques pour l'accessibilité

*   Utiliser des balises HTML sémantiques.
*   Fournir un texte alternatif pour les images.
*   Utiliser des attributs ARIA pour améliorer l'accessibilité des éléments interactifs.
*   S'assurer que le contenu est accessible au clavier.
*   Fournir des contrastes de couleurs suffisants.
## 12. Bonnes Pratiques et Validation

### Structure du code

*   Utiliser une indentation cohérente.
*   Écrire du code HTML valide.
*   Séparer le contenu, la présentation et le comportement (HTML, CSS, JavaScript).
*   Utiliser des commentaires pour expliquer le code.

### Validation HTML

*   Valider le code HTML avec un validateur en ligne (ex: [W3C Markup Validator](https://validator.w3.org/)).
*   Corriger les erreurs de validation pour assurer la compatibilité et l'accessibilité.
## 13. Ressources et Communauté

### Documentation MDN Web Docs

*   [MDN Web Docs HTML](https://developer.mozilla.org/fr/docs/Web/HTML)

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/html)](https://www.reddit.com/r/html/)

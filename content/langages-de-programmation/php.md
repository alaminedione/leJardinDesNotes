---
title: PHP
draft: false
tags:
  - php
  - programming
description: Langage de script côté serveur, largement utilisé pour le développement web dynamique.
---

# Php

## Sommaire

1. Introduction à PHP
    * Qu'est-ce que PHP ?
    * Historique et évolution
    * Installation et configuration (avec un serveur web comme Apache ou Nginx)
    * Structure d'un script PHP
2. Bases du Langage
    * Syntaxe de base
    * Variables et types de données (scalaires, composés, spéciaux)
    * Opérateurs
    * Structures de contrôle (if, else, elseif, switch, while, do-while, for, foreach)
    * Fonctions
3. Tableaux (Arrays)
    * Tableaux indexés et associatifs
    * Manipulation des tableaux
4. Chaînes de Caractères
    * Manipulation des chaînes
    * Expressions régulières
5. Programmation Orientée Objet (POO) en PHP
    * Classes et Objets
    * Propriétés et Méthodes
    * Constructeurs et Destructeurs
    * Héritage
    * Interfaces et Classes abstraites
    * Visibilité (public, private, protected)
    * Traits
6. Gestion des Erreurs et Exceptions
    * Types d'erreurs
    * Gestion des exceptions (try-catch-finally)
7. Interaction avec les Bases de Données
    * Extensions (MySQLi, PDO)
    * Connexion à une base de données
    * Exécution de requêtes (SELECT, INSERT, UPDATE, DELETE)
    * Préparation des requêtes
8. Gestion des Sessions et Cookies
    * Sessions
    * Cookies
9. Inclusion de Fichiers
    * include, require, include_once, require_once
10. Développement Web avec PHP
    * Variables superglobales ($_GET, $_POST, $_SERVER, etc.)
    * Gestion des formulaires
    * Téléchargement de fichiers
    * Frameworks populaires (Laravel, Symfony, CodeIgniter)
11. Composer (Gestionnaire de Dépendances)
    * Installation et utilisation
    * Autoloading
12. Tests en PHP
    * PHPUnit
13. Bonnes Pratiques et PSR
    * Conventions de codage (PSR)
    * Sécurité
14. Ressources et Communauté
    * Documentation officielle
    * Communautés en ligne

## 1. Introduction à PHP

### Qu'est-ce Que PHP ?

PHP (Hypertext Preprocessor) est un langage de script côté serveur, largement utilisé pour le développement web dynamique. Il est conçu pour être intégré dans le code HTML et permet de créer des pages web interactives et personnalisées.

### Historique Et Évolution

* Créé par Rasmus Lerdorf en 1994.
* Initialement un ensemble de scripts Perl pour suivre les visites de son CV en ligne.
* Évolue rapidement pour devenir un langage de script complet.
* PHP 5 (2004) introduit un modèle objet plus robuste.
* PHP 7 (2015) améliore considérablement les performances et introduit de nouvelles fonctionnalités.
* PHP 8 (2020) continue d'améliorer les performances et ajoute de nouvelles fonctionnalités (ex: JIT compiler).

### Installation Et Configuration (avec Un Serveur Web Comme Apache Ou Nginx)

1. Installer un serveur web (Apache ou Nginx).
2. Installer PHP et les extensions nécessaires.
3. Configurer le serveur web pour traiter les fichiers PHP.

### Structure D'un Script PHP

* Le code PHP est délimité par les balises `<?php` et `?>`.
* Peut être intégré dans du code HTML.

```php
<!DOCTYPE html>
<html>
<head>
    <title>Ma Page PHP</title>
</head>
<body>
    <h1>Bienvenue !</h1>
    <?php
        echo "Bonjour, monde!";
    ?>
</body>
</html>
```

## 2. Bases Du Langage

### Syntaxe De Base

* Syntaxe inspirée de C, C++ et Perl.
* Utilisation de variables, de types de données, d'opérateurs et de structures de contrôle.
* Les instructions se terminent par un point-virgule (`;`).
* Sensible à la casse (majuscules et minuscules) pour les noms de variables.

```php
<?php
// Ceci est un commentaire

$nom = "John"; // Déclaration d'une variable
echo "Hello, " . $nom . "!"; // Affichage dans la console
?>
```

### Variables Et Types De Données (scalaires, Composés, spéciaux)

* Types scalaires :
    * `int` : Entiers.
    * `float` : Nombres à virgule flottante.
    * `string` : Chaînes de caractères.
    * `bool` : Booléens (true ou false).
* Types composés :
    * `array` : Tableaux.
    * `object` : Objets.
* Types spéciaux :
    * `resource` : Référence à une ressource externe (ex: connexion à une base de données).
    * `NULL` : Absence de valeur.

```php
<?php
$age = 30; // int
$nom = "John"; // string
$salaire = 50000.0; // float
$est_valide = true; // bool
$nombres = array(1, 2, 3); // array
$objet = new stdClass(); // object
$ressource = fopen("monfichier.txt", "r"); // resource
$valeur_nulle = NULL; // NULL
?>
```

### Opérateurs

* Arithmétiques : `+`, `-`, `*`, `/`, `%`, `**` (exponentiation)
* Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
* Logiques : `&&`, `||`, `!`
* Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `.=` (concaténation)
* Incrémentation/Décrémentation : `++`, `--`

```php
<?php
$x = 10;
$y = 5;
$sum = $x + $y;
$is_equal = ($x == $y);
$condition = ($x > 0 && $y < 10);
$x++;
?>
```

### Structures De Contrôle (if, Else, Elseif, Switch, While, Do-while, For, foreach)

* `if`, `elseif`, `else` : Conditionnelles
* `while` : Boucle while
* `do-while` : Boucle do-while
* `for` : Boucle for
* `foreach` : Boucle foreach (pour parcourir les tableaux)
* `switch` : Sélection multiple

```php
<?php
$score = 85;
if ($score > 90) {
    // ...
} elseif ($score > 80) {
    // ...
} else {
    // ...
}

for ($i = 0; $i < 5; $i++) {
    // ...
}

while ($score > 0) {
    // ...
    $score--;
}

foreach ($nombres as $nombre) {
    // ...
}

switch ($score) {
    case 100:
        // ...
        break;
    default:
        // ...
}
?>
```

### Fonctions

* Blocs de code réutilisables.
* Déclaration : `function nomFonction(paramètres) { // corps }`
* Retour de valeurs avec le mot-clé `return`.

```php
<?php
function add($a, $b) {
    return $a + $b;
}

$result = add(5, 3);
echo $result;
?>
```

## 3. Tableaux (Arrays)

### Tableaux Indexés Et Associatifs

* **Tableaux indexés** : Les éléments sont accessibles par un index numérique (à partir de 0).
* **Tableaux associatifs** : Les éléments sont accessibles par une clé (chaîne de caractères ou nombre).

```php
<?php
// Tableau indexé
$nombres = array(10, 20, 30);
echo $nombres[0]; // 10

// Tableau associatif
$ages = array(
    "Alice" => 30,
    "Bob" => 25
);
echo $ages["Alice"]; // 30
?>
```

### Manipulation Des Tableaux

* Fonctions courantes :
    * `count()` : Retourne le nombre d'éléments dans un tableau.
    * `array_push()` : Ajoute un élément à la fin d'un tableau.
    * `array_pop()` : Supprime le dernier élément d'un tableau.
    * `array_shift()` : Supprime le premier élément d'un tableau.
    * `array_unshift()` : Ajoute un élément au début d'un tableau.
    * `unset()` : Supprime un élément d'un tableau.

```php
<?php
$nombres = array(10, 20, 30);
echo count($nombres); // 3

array_push($nombres, 40); // Ajoute 40 à la fin
array_pop($nombres); // Supprime le dernier élément

unset($nombres[0]); // Supprime l'élément à l'index 0
?>
```

## 4. Chaînes De Caractères

### Manipulation Des Chaînes

* Concaténation : Utilisation de l'opérateur `.` (point).
* Fonctions courantes :
    * `strlen()` : Retourne la longueur d'une chaîne.
    * `strpos()` : Recherche la position d'une sous-chaîne dans une chaîne.
    * `substr()` : Extrait une partie d'une chaîne.
    * `str_replace()` : Remplace une sous-chaîne par une autre.
    * `strtolower()` : Convertit une chaîne en minuscules.
    * `strtoupper()` : Convertit une chaîne en majuscules.

```php
<?php
$nom = "John";
$message = "Hello, " . $nom . "!"; // Concaténation

echo strlen($message); // 13
echo strpos($message, "Hello"); // 0
echo substr($message, 0, 5); // Hello
echo str_replace("Hello", "Bonjour", $message); // Bonjour, John!
echo strtolower($message); // hello, john!
echo strtoupper($message); // HELLO, JOHN!
?>
```

### Expressions Régulières

* PHP supporte les expressions régulières avec les fonctions `preg_match`, `preg_replace`, etc.

```php
<?php
$chaine = "Mon numéro de téléphone est 0123456789";
if (preg_match("/[0-9]{10}/", $chaine)) {
    echo "Numéro de téléphone valide";
}
?>
```

## 5. Programmation Orientée Objet (POO) En PHP

### Classes Et Objets

* Une classe est un modèle pour créer des objets.
* Un objet est une instance d'une classe.

```php
<?php
class MaClasse {
    public $nom;

    public function __construct($nom) {
        $this->nom = $nom;
    }

    public function direBonjour() {
        echo "Bonjour, je suis " . $this->nom;
    }
}

$objet = new MaClasse("John");
$objet->direBonjour();
?>
```

### Propriétés Et Méthodes

* Les propriétés sont les attributs d'une classe.
* Les méthodes sont les fonctions d'une classe.

### Constructeurs Et Destructeurs

* Le constructeur est une méthode spéciale appelée lors de la création d'un objet (`__construct`).
* Le destructeur est une méthode spéciale appelée lors de la destruction d'un objet (`__destruct`).

### Héritage

* Permet à une classe (sous-classe) d'hériter des propriétés et des méthodes d'une autre classe (super-classe).
* Utilisation du mot-clé `extends`.

```php
<?php
class Animal {
    public $nom;

    public function __construct($nom) {
        $this->nom = $nom;
    }

    public function faireDuBruit() {
        echo "Bruit générique";
    }
}

class Chien extends Animal {
    public function faireDuBruit() {
        echo "Woof!";
    }
}

$chien = new Chien("Fido");
$chien->faireDuBruit(); // Woof!
?>
```

### Interfaces Et Classes Abstraites

* **Interface** : Contrat définissant un ensemble de méthodes qu'une classe doit implémenter.
* **Classe abstraite** : Classe qui ne peut pas être instanciée directement et qui peut contenir des méthodes abstraites (sans implémentation).

### Visibilité (public, Private, protected)

* `public` : Accessible depuis n'importe où.
* `private` : Accessible uniquement depuis la classe où elle est définie.
* `protected` : Accessible depuis la classe où elle est définie et depuis ses sous-classes.

### Traits

* Les traits sont un mécanisme de réutilisation de code dans les langages à héritage simple comme PHP.
* Un trait est un ensemble de méthodes qui peuvent être incluses dans une classe.

```php
<?php
trait MonTrait {
    public function direAuRevoir() {
        echo "Au revoir!";
    }
}

class MaClasse {
    use MonTrait;
}

$objet = new MaClasse();
$objet->direAuRevoir(); // Au revoir!
?>
```

## 6. Gestion Des Erreurs Et Exceptions

### Types D'erreurs

* **Erreurs de syntaxe** : Erreurs détectées lors de la compilation (ex: erreur de point-virgule).
* **Erreurs d'exécution** : Erreurs détectées lors de l'exécution du code (ex: division par zéro).
* **Exceptions** : Erreurs gérées avec les blocs `try…catch`.

### Gestion Des Exceptions (try-catch-finally)

* Utilisation des blocs `try…catch` pour capturer et gérer les exceptions.
* Le bloc `finally` est exécuté que l'exception soit levée ou non.

```php
<?php
try {
    // Code qui peut lever une exception
    $resultat = 10 / 0;
} catch (Exception $e) {
    // Gestion de l'exception
    echo "Erreur: " . $e->getMessage();
} finally {
    // Code exécuté dans tous les cas
    echo "Fin du bloc try-catch";
}
?>
```

## 7. Interaction Avec Les Bases De Données

### Extensions (MySQLi, PDO)

* **MySQLi** : Extension pour interagir avec les bases de données MySQL (améliorée par rapport à l'ancienne extension `mysql`).
* **PDO (PHP Data Objects)** : Interface d'accès aux bases de données, permettant d'utiliser différents types de bases de données avec la même API.

### Connexion à Une Base De Données

* Utilisation des fonctions `mysqli_connect` (pour MySQLi) ou de la classe `PDO`.

```php
<?php
// MySQLi
$conn = mysqli_connect("localhost", "mon_utilisateur", "mon_mot_de_passe", "ma_base_de_donnees");
if (!$conn) {
    die("Connexion échouée: " . mysqli_connect_error());
}

// PDO
try {
    $conn = new PDO("mysql:host=localhost;dbname=ma_base_de_donnees", "mon_utilisateur", "mon_mot_de_passe");
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $e) {
    echo "Connexion échouée: " . $e->getMessage();
}
?>
```

### Exécution De Requêtes (SELECT, INSERT, UPDATE, DELETE)

* Utilisation des fonctions `mysqli_query` (pour MySQLi) ou des méthodes `query` et `exec` (pour PDO).

### Préparation Des Requêtes

* La préparation des requêtes permet d'éviter les injections SQL.
* Utilisation des fonctions `mysqli_prepare` (pour MySQLi) ou des méthodes `prepare` (pour PDO).

## 8. Gestion Des Sessions Et Cookies

### Sessions

* Les sessions permettent de stocker des informations sur un utilisateur entre les requêtes.
* Utilisation des fonctions `session_start`, `$_SESSION`, `session_destroy`.

```php
<?php
session_start(); // Démarrage de la session

$_SESSION["nom"] = "John"; // Stockage d'une variable de session

echo "Bonjour, " . $_SESSION["nom"];

session_destroy(); // Destruction de la session
?>
```

### Cookies

* Les cookies sont de petits fichiers texte stockés sur l'ordinateur de l'utilisateur.
* Utilisation de la fonction `setcookie` pour créer un cookie et de la variable superglobale `$_COOKIE` pour accéder aux cookies.

```php
<?php
setcookie("nom", "John", time() + (86400 * 30), "/"); // Création d'un cookie valable 30 jours

echo "Bonjour, " . $_COOKIE["nom"];
?>
```

## 9. Inclusion De Fichiers

### Include, Require, include_once, require_once

* `include` : Inclut un fichier. Si le fichier n'est pas trouvé, une alerte est générée, mais le script continue.
* `require` : Inclut un fichier. Si le fichier n'est pas trouvé, une erreur fatale est générée et le script s'arrête.
* `include_once` : Inclut un fichier une seule fois.
* `require_once` : Inclut un fichier une seule fois.

```php
<?php
include 'monfichier.php';
require 'monfichier.php';

include_once 'monfichier.php';
require_once 'monfichier.php';
?>
```

## 10. Développement Web Avec PHP

### Variables Superglobales ($_GET, $_POST, $_SERVER, etc.)

* Les variables superglobales sont des variables prédéfinies qui sont toujours disponibles, quel que soit le scope.
* `$_GET` : Contient les paramètres passés dans l'URL (méthode GET).
* `$_POST` : Contient les données envoyées par un formulaire (méthode POST).
* `$_SERVER` : Contient des informations sur le serveur web et l'environnement d'exécution.

### Gestion Des Formulaires

* Récupération des données envoyées par un formulaire avec les variables `$_GET` ou `$_POST`.
* Validation des données du formulaire.
* Traitement des données du formulaire.

### Téléchargement De Fichiers

* Utilisation de la variable superglobale `$_FILES` pour gérer les fichiers téléchargés.
* Validation du type et de la taille des fichiers.
* Déplacement des fichiers téléchargés vers un répertoire de stockage.

### Frameworks Populaires (Laravel, Symfony, CodeIgniter)

* **Laravel** : Framework PHP open-source, élégant et puissant, offrant de nombreuses fonctionnalités (ORM, templating, routing, etc.).
* **Symfony** : Framework PHP open-source, flexible et réutilisable, adapté aux applications complexes.
* **CodeIgniter** : Framework PHP léger et simple à apprendre, idéal pour les projets de petite et moyenne taille.

## 11. Composer (Gestionnaire De Dépendances)

### Installation Et Utilisation

* Composer est un gestionnaire de dépendances pour PHP.
* Il permet de gérer les dépendances d'un projet PHP et de les installer facilement.

### Autoloading

* Composer permet de générer un fichier d'autoloading qui charge automatiquement les classes utilisées dans le projet.

## 12. Tests En PHP

### PHPUnit

* PHPUnit est un framework de test unitaire pour PHP.
* Il permet d'écrire des tests unitaires pour vérifier le comportement du code.

## 13. Bonnes Pratiques Et PSR

### Conventions De Codage (PSR)

* PSR (PHP Standards Recommendations) est un ensemble de recommandations pour le style de code PHP.
* Suivre les PSR permet d'assurer la cohérence et la lisibilité du code.

### Sécurité

* Éviter les injections SQL.
* Valider les données utilisateur.
* Protéger les sessions et les cookies.
* Utiliser des fonctions de hachage robustes pour stocker les mots de passe.

## 14. Ressources Et Communauté

### Documentation Officielle

* [PHP Manual](https://www.php.net/manual/fr/)

### Communautés En Ligne

* [Stack Overflow](https://stackoverflow.com/)
* [Reddit (r/php)](https://www.reddit.com/r/php/)

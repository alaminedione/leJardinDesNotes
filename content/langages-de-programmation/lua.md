---
title: Lua
draft: false
tags:
  - lua
  - programming
description: Langage de script léger, embarquable, conçu pour être étendu et intégré dans d'autres applications.
---

## Sommaire

1.  Introduction à Lua
    *   Qu'est-ce que Lua ?
    *   Historique et philosophie
    *   Installation et exécution
    *   Intégration dans d'autres langages (C, C++)
2.  Bases du Langage
    *   Syntaxe de base
    *   Variables et types de données (nil, booléen, nombre, chaîne, table, fonction, userdata, thread)
    *   Opérateurs
    *   Structures de contrôle (if, while, repeat, for)
    *   Fonctions
3.  Tables
    *   Création et manipulation des tables
    *   Utilisation comme tableaux et dictionnaires
    *   Métatables et métaméthodes
4.  Fonctions
    *   Déclaration et appel
    *   Fonctions anonymes (closures)
    *   Portée des variables (locale, globale, upvalue)
    *   Arguments variables
5.  Modules et Packages
    *   Système de modules (require)
    *   Création de modules
6.  Gestion des Erreurs
    *   pcall et xpcall
    *   Erreurs et messages d'erreur
7.  Entrées/Sorties (I/O)
    *   Lecture et écriture de fichiers
    *   Entrée/sortie standard
8.  Coroutines
    *   Création et gestion des coroutines
    *   Yield et Resume
9.  Garbage Collection
    *   Fonctionnement du ramasse-miettes
    *   Finalisateurs
10. C API
    *   Interaction entre Lua et C
    *   Empilement (Stack)
    *   Appel de fonctions C depuis Lua et vice-versa
11. Bonnes Pratiques
    *   Conventions de codage
    *   Optimisation
12. Ressources et Communauté
    *   Documentation officielle
    *   Communautés en ligne
## 1. Introduction à Lua

### Qu'est-ce que Lua ?

Lua est un langage de script léger, embarquable, conçu pour être étendu et intégré dans d'autres applications. Il est utilisé dans de nombreux domaines, tels que les jeux vidéo, les applications embarquées et les serveurs web.

### Historique et philosophie

*   Créé en 1993 par Roberto Ierusalimschy, Luiz Henrique de Figueiredo et Waldemar Celes à l'Université Pontificale Catholique de Rio de Janeiro, Brésil.
*   Objectifs : simplicité, portabilité, extensibilité.
*   Influencé par les langages SOL et DEL.

### Installation et exécution

1.  Télécharger Lua depuis [le site officiel](https://www.lua.org/download.html).
2.  Installer Lua en suivant les instructions spécifiques à votre système d'exploitation.
3.  Exécuter Lua en ligne de commande avec la commande `lua`.

```bash
lua mon_script.lua
```

### Intégration dans d'autres langages (C, C++)

*   Lua est conçu pour être facilement intégré dans d'autres langages, notamment C et C++.
*   L'API C de Lua permet d'étendre les fonctionnalités de Lua et d'utiliser Lua comme langage de script dans des applications C/C++.

## 2. Bases du Langage

### Syntaxe de base

*   Syntaxe simple et concise.
*   Pas de types de données statiques.
*   Utilisation de blocs de code délimités par les mots-clés `do` et `end`.
*   Les commentaires commencent par `--`.

```lua
-- Ceci est un commentaire

local nom = "John" -- Déclaration d'une variable locale
print("Hello, " .. nom .. "!") -- Affichage dans la console
```

### Variables et types de données (nil, booléen, nombre, chaîne, table, fonction, userdata, thread)

*   `nil` : Absence de valeur.
*   `boolean` : Booléens (true ou false).
*   `number` : Nombres (flottants par défaut).
*   `string` : Chaînes de caractères.
*   `table` : Tableaux associatifs (dictionnaires).
*   `function` : Fonctions.
*   `userdata` : Données définies par l'application hôte (C/C++).
*   `thread` : Coroutines (threads légers).

```lua
local age = 30 -- number
local nom = "John" -- string
local est_valide = true -- boolean
local valeur_nulle = nil -- nil

local personne = { -- table
    nom = "John",
    age = 30
}

local add = function(a, b) -- function
    return a + b
end
```

### Opérateurs

*   Arithmétiques : `+`, `-`, `*`, `/`, `%`, `^` (exponentiation)
*   Relationnels : `==`, `~=`, `<`, `>`, `<=`, `>=`
*   Logiques : `and`, `or`, `not`
*   Concaténation : `..`

```lua
local x = 10
local y = 5
local sum = x + y
local is_equal = (x == y)
local condition = (x > 0 and y < 10)
local message = "Hello, " .. "World!"
```

### Structures de contrôle (if, while, repeat, for)

*   `if`, `elseif`, `else` : Conditionnelles
*   `while` : Boucle while
*   `repeat...until` : Boucle repeat
*   `for` : Boucle for numérique et générique

```lua
local score = 85
if score > 90 then
    -- ...
elseif score > 80 then
    -- ...
else
    -- ...
end

local i = 0
while i < 5 do
    -- ...
    i = i + 1
end

repeat
    -- ...
until i >= 5

for i = 1, 5 do
    -- ...
end

local t = {1, 2, 3}
for i, v in ipairs(t) do
    print(i, v)
end
```

### Fonctions

*   Blocs de code réutilisables.
*   Déclaration : `function nomFonction(paramètres) // corps end`
*   Retour de plusieurs valeurs.

```lua
function add(a, b)
    return a + b
end

local result = add(5, 3)
print(result)
```
## 3. Tables

### Création et manipulation des tables

*   Les tables sont le principal mécanisme de structuration des données en Lua.
*   Elles peuvent être utilisées comme tableaux, dictionnaires ou objets.
*   Création : `local nom_table = {}`
*   Accès aux éléments : `nom_table[clé]` ou `nom_table.clé` (si la clé est une chaîne de caractères valide).

```lua
local personne = {} -- Création d'une table vide

personne.nom = "John" -- Ajout d'un champ
personne["age"] = 30 -- Ajout d'un autre champ

print(personne.nom) -- Accès à un champ
print(personne["age"]) -- Accès à un autre champ
```

### Utilisation comme tableaux et dictionnaires

*   Tableaux : Utilisation d'indices numériques (à partir de 1).
*   Dictionnaires : Utilisation de clés de type chaîne de caractères ou autre type.

```lua
-- Tableau
local nombres = {10, 20, 30}
print(nombres[1]) -- 10

-- Dictionnaire
local ages = {
    Alice = 30,
    Bob = 25
}
print(ages["Alice"]) -- 30
```

### Métatables et métaméthodes

*   Les métatables permettent de définir le comportement des tables lors de certaines opérations (ex: addition, soustraction, accès à un champ inexistant).
*   Les métaméthodes sont des fonctions spéciales définies dans la métatable qui sont appelées lors de ces opérations.

```lua
local t = {}
local mt = {
    __index = function(t, k)
        return "Valeur par défaut pour " .. k
    end
}
setmetatable(t, mt)

print(t.nom) -- Valeur par défaut pour nom
```
## 4. Fonctions

### Déclaration et appel

*   Déclaration : `function nomFonction(paramètres) // corps end`
*   Appel : `nomFonction(arguments)`

```lua
function add(a, b)
    return a + b
end

local result = add(5, 3)
print(result)
```

### Fonctions anonymes (closures)

*   Les fonctions anonymes sont des fonctions sans nom.
*   Elles sont souvent utilisées comme arguments à d'autres fonctions ou pour créer des closures.

```lua
local multiply = function(a, b)
    return a * b
end

print(multiply(5, 3))

function createMultiplier(factor)
    return function(x)
        return x * factor
    end
end

local double = createMultiplier(2)
print(double(5)) -- 10
```

### Portée des variables (locale, globale, upvalue)

*   `locale` : Variables déclarées avec le mot-clé `local` sont visibles uniquement dans le bloc où elles sont définies.
*   `globale` : Variables déclarées sans le mot-clé `local` sont globales (accessibles depuis n'importe où dans le programme).
*   `upvalue` : Variables locales d'une fonction englobante qui sont utilisées par une fonction interne (closure).

```lua
local x = 10 -- variable locale

function maFonction()
    y = 20 -- variable globale (car pas de 'local')
    local z = 30 -- variable locale

    local upvalue = 40
    local innerFunction = function()
        print(upvalue) -- upvalue
    end
    innerFunction()
end

maFonction()
print(y) -- 20
-- print(z) -- Erreur : z n'est pas visible ici
```

### Arguments variables

*   Lua permet de définir des fonctions qui acceptent un nombre variable d'arguments.
*   Utilisation de l'objet `arg` (déprécié) ou de la syntaxe `...` (vararg).

```lua
function afficherArguments(...)
    for i, v in ipairs(arg) do -- arg est déprécié
        print(i, v)
    end
end

function afficherArguments2(...)
  local args = {...}
  for i, v in ipairs(args) do
    print(i, v)
  end
end


afficherArguments(1, 2, 3)
afficherArguments2(4,5,6)
```
## 5. Modules et Packages

### Système de modules (require)

*   Lua utilise la fonction `require` pour charger et exécuter des modules.
*   Les modules sont des fichiers Lua qui retournent une table contenant les fonctions et les variables à exporter.

### Création de modules

1.  Créer un fichier Lua contenant le code du module.
2.  Retourner une table contenant les fonctions et les variables à exporter.
3.  Utiliser `require` pour charger le module.

```lua
-- mon_module.lua
local M = {}

function M.ma_fonction()
    print("Hello from mon_module!")
end

return M
```

```lua
-- main.lua
local mon_module = require("mon_module")
mon_module.ma_fonction() -- Hello from mon_module!
```
## 6. Gestion des Erreurs

### pcall et xpcall

*   `pcall` (protected call) : Appelle une fonction en mode protégé, capturant les erreurs éventuelles.
*   `xpcall` : Similaire à `pcall`, mais permet de spécifier un gestionnaire d'erreurs personnalisé.

```lua
local status, result = pcall(function()
    -- Code qui peut potentiellement lever une erreur
    error("Ceci est une erreur")
end)

if not status then
    print("Erreur:", result)
end
```

### Erreurs et messages d'erreur

*   La fonction `error` permet de lever une erreur.
*   Les messages d'erreur peuvent être des chaînes de caractères ou des objets Lua.

```lua
error("Ceci est une erreur")
```
## 7. Entrées/Sorties (I/O)

### Lecture et écriture de fichiers

*   Utilisation des fonctions `io.open`, `file:read`, `file:write`, `file:close`.

```lua
-- Écriture dans un fichier
local file, err = io.open("monfichier.txt", "w")
if file then
    file:write("Hello, fichier!")
    file:close()
else
    print("Erreur lors de l'ouverture du fichier:", err)
end

-- Lecture depuis un fichier
file, err = io.open("monfichier.txt", "r")
if file then
    local content = file:read("*all")
    file:close()
    print(content)
else
    print("Erreur lors de l'ouverture du fichier:", err)
end
```

### Entrée/sortie standard

*   Utilisation des fonctions `print` pour afficher et `io.read` pour lire depuis l'entrée standard.

```lua
print("Entrez votre nom:")
local nom = io.read()
print("Bonjour, " .. nom .. "!")
```
## 8. Coroutines

### Création et gestion des coroutines

*   Les coroutines sont des fonctions qui peuvent suspendre leur exécution et la reprendre plus tard.
*   Création : `coroutine.create(fonction)`
*   État : `coroutine.status(coroutine)` (running, suspended, normal, dead)

### Yield et Resume

*   `coroutine.yield()` : Suspend l'exécution de la coroutine.
*   `coroutine.resume()` : Reprend l'exécution de la coroutine.

```lua
co = coroutine.create(function (a,b)
  print("co-routine started")
  local x = coroutine.yield(a + b)
  print("co-routine resumed, x = " .. x)
  return a + b + x
end)

print("main", coroutine.resume(co, 12, 13))
print("main", coroutine.resume(co, 100))
print("main", coroutine.resume(co, 100))
```
## 9. Garbage Collection

### Fonctionnement du ramasse-miettes

*   Lua utilise un ramasse-miettes automatique pour gérer la mémoire.
*   Le ramasse-miettes libère automatiquement la mémoire qui n'est plus utilisée par le programme.

### Finalisateurs

*   Les finalisateurs sont des fonctions qui sont appelées lorsque le ramasse-miettes s'apprête à libérer un objet.
*   Ils permettent d'effectuer des opérations de nettoyage (ex: fermeture de fichiers).
## 10. C API

### Interaction entre Lua et C

*   Lua peut être étendu avec des fonctions écrites en C.
*   L'API C de Lua permet d'appeler des fonctions C depuis Lua et vice-versa.

### Empilement (Stack)

*   L'API C de Lua utilise une pile pour échanger des données entre Lua et C.
*   Les valeurs Lua sont poussées sur la pile et récupérées depuis la pile.

### Appel de fonctions C depuis Lua et vice-versa

*   Pour appeler une fonction C depuis Lua, il faut l'enregistrer auprès de Lua.
*   Pour appeler une fonction Lua depuis C, il faut la récupérer depuis l'environnement global de Lua.
## 11. Bonnes Pratiques

### Conventions de codage

*   Utiliser des noms clairs et descriptifs.
*   Indenter correctement le code.
*   Limiter la portée des variables (utiliser `local` autant que possible).
*   Écrire des commentaires pour expliquer le code.

### Optimisation

*   Éviter les allocations de mémoire inutiles.
*   Utiliser des algorithmes efficaces.
*   Profiler le code pour identifier les goulots d'étranglement.
## 12. Ressources et Communauté

### Documentation officielle

*   [Lua 5.1 Reference Manual](https://www.lua.org/manual/5.1/) (la version la plus utilisée)
*   [Lua 5.4 Reference Manual](https://www.lua.org/manual/5.4/) (dernière version)

### Communautés en ligne

*   [Lua Users Mailing List](http://lua-users.org/lists/lua-l/)
*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/lua)](https://www.reddit.com/r/lua/)

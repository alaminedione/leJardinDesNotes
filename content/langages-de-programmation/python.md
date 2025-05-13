---
title: Python
draft: false
tags:
  - python
  - programming
description: Langage de programmation interprété, de haut niveau et à typage dynamique, connu pour sa lisibilité et sa polyvalence.
---

## Sommaire

1.  Introduction à Python
    *   Qu'est-ce que Python ?
    *   Historique et philosophie (Zen of Python)
    *   Installation et environnements virtuels (venv, conda)
    *   Interpréteur Python
2.  Bases du Langage
    *   Syntaxe de base (indentation)
    *   Variables et types de données (numériques, chaînes, booléens)
    *   Opérateurs
    *   Structures de contrôle (if, for, while)
    *   Fonctions
3.  Structures de Données
    *   Listes
    *   Tuples
    *   Sets
    *   Dictionnaires
4.  Programmation Orientée Objet (POO) en Python
    *   Classes et Objets
    *   Héritage
    *   Polymorphisme
    *   Encapsulation (conventions)
5.  Modules et Packages
    *   Importation de modules
    *   Création de packages
    *   Gestion des paquets (pip)
6.  Gestion des Exceptions
    *   Blocs try-except-finally
    *   Levée d'exceptions
7.  Entrées/Sorties (I/O)
    *   Lecture et écriture de fichiers
    *   Entrée utilisateur
8.  Décorateurs et Générateurs
    *   Décorateurs
    *   Générateurs et itérateurs
9.  Développement Web avec Python
    *   Frameworks (Django, Flask, FastAPI)
    *   Requêtes HTTP (requests)
10. Data Science et Machine Learning
    *   Bibliothèques populaires (NumPy, Pandas, Scikit-learn, TensorFlow, PyTorch)
11. Tests en Python
    *   unittest, pytest
12. Bonnes Pratiques et PEP 8
    *   Conventions de codage (PEP 8)
    *   Documentation (docstrings)
13. Ressources et Communauté
    *   Documentation officielle
    *   Communautés en ligne (PyPI, Stack Overflow)
## 1. Introduction à Python

### Qu'est-ce que Python ?

Python est un langage de programmation interprété, de haut niveau et à typage dynamique, connu pour sa lisibilité et sa polyvalence. Il est utilisé dans de nombreux domaines, tels que le développement web, la science des données, l'apprentissage automatique et l'automatisation.

### Historique et philosophie (Zen of Python)

*   Créé par Guido van Rossum et publié en 1991.
*   Philosophie : "There should be one-- and preferably only one --obvious way to do it."
*   Le Zen de Python : Principes de conception du langage (affichés en tapant `import this` dans l'interpréteur Python).

### Installation et environnements virtuels (venv, conda)

1.  Télécharger Python depuis [le site officiel](https://www.python.org/downloads/).
2.  Installer Python en suivant les instructions spécifiques à votre système d'exploitation.
3.  Créer un environnement virtuel pour isoler les dépendances du projet.
    *   `venv` (module intégré) : `python3 -m venv mon_environnement`
    *   `conda` (Anaconda) : `conda create -n mon_environnement python=3.9`

### Interpréteur Python

*   Permet d'exécuter le code Python en ligne de commande.
*   Lancement : `python` ou `python3`.

## 2. Bases du Langage

### Syntaxe de base (indentation)

*   Python utilise l'indentation pour délimiter les blocs de code (au lieu des accolades).
*   L'indentation doit être cohérente (4 espaces par niveau).

```python
if True:
    print("Ceci est un bloc indenté")
```

### Variables et types de données (numériques, chaînes, booléens)

*   Types numériques : `int`, `float`, `complex`.
*   Chaînes de caractères : `str`.
*   Booléens : `bool` (True ou False).

```python
age = 30 # int
nom = "John" # str
salaire = 50000.0 # float
est_valide = True # bool
complexe = 1 + 2j # complex
```

### Opérateurs

*   Arithmétiques : `+`, `-`, `*`, `/`, `//` (division entière), `%`, `**` (exponentiation)
*   Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
*   Logiques : `and`, `or`, `not`
*   Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=`

```python
x = 10
y = 5
somme = x + y
est_egal = (x == y)
condition = (x > 0 and y < 10)
x += 1
```

### Structures de contrôle (if, for, while)

*   `if`, `elif`, `else` : Conditionnelles
*   `for` : Boucle for (pour parcourir les séquences)
*   `while` : Boucle while

```python
score = 85
if score > 90:
    # ...
elif score > 80:
    # ...
else:
    # ...

nombres = [1, 2, 3, 4, 5]
for nombre in nombres:
    # ...

i = 0
while i < 5:
    # ...
    i += 1
```

### Fonctions

*   Blocs de code réutilisables.
*   Définition : `def nom_fonction(paramètres): // corps`
*   Retour de valeurs avec le mot-clé `return`.

```python
def add(a, b):
    return a + b

resultat = add(5, 3)
print(resultat)
```
## 3. Structures de Données

### Listes

*   Séquences ordonnées et modifiables d'éléments.
*   Création : `[element1, element2, ...]`
*   Accès aux éléments : `liste[index]`
*   Manipulation : ajout, suppression, modification d'éléments.

```python
nombres = [1, 2, 3, 4, 5]
print(nombres[0]) # 1

nombres.append(6) # Ajoute 6 à la fin
nombres.insert(0, 0) # Insère 0 au début
del nombres[0] # Supprime le premier élément
```

### Tuples

*   Séquences ordonnées et non modifiables d'éléments.
*   Création : `(element1, element2, ...)`
*   Les tuples sont plus rapides et consomment moins de mémoire que les listes.

```python
coordonnees = (10, 20)
print(coordonnees[0]) # 10
```

### Sets

*   Collections non ordonnées d'éléments uniques.
*   Création : `{element1, element2, ...}` ou `set([element1, element2, ...])`
*   Opérations : union, intersection, différence.

```python
ensemble = {1, 2, 3, 4, 5}
ensemble2 = set([4, 5, 6, 7, 8])

union = ensemble | ensemble2 # Union
intersection = ensemble & ensemble2 # Intersection
difference = ensemble - ensemble2 # Différence
```

### Dictionnaires

*   Collections de paires clé-valeur.
*   Création : `{clé1: valeur1, clé2: valeur2, ...}`
*   Accès aux valeurs : `dictionnaire[clé]`
*   Manipulation : ajout, suppression, modification de paires clé-valeur.

```python
personne = {
    "nom": "John",
    "age": 30
}

print(personne["nom"]) # John

personne["ville"] = "New York" # Ajoute une clé-valeur
del personne["age"] # Supprime une clé-valeur
```
## 4. Programmation Orientée Objet (POO) en Python

### Classes et Objets

*   Une classe est un modèle pour créer des objets.
*   Un objet est une instance d'une classe.
*   Utilisation du mot-clé `class` pour définir une classe.
*   Utilisation du mot-clé `self` pour référencer l'objet courant.
*   Constructeur : méthode spéciale `__init__`.

```python
class Personne:
    def __init__(self, nom, age):
        self.nom = nom
        self.age = age

    def dire_bonjour(self):
        print(f"Bonjour, je suis {self.nom}")

personne = Personne("John", 30)
personne.dire_bonjour()
```

### Héritage

*   Permet à une classe (sous-classe) d'hériter des attributs et des méthodes d'une autre classe (super-classe).
*   Utilisation de la syntaxe `class SousClasse(SuperClasse):`.

```python
class Animal:
    def __init__(self, nom):
        self.nom = nom

    def faire_du_bruit(self):
        print("Bruit générique")

class Chien(Animal):
    def faire_du_bruit(self):
        print("Woof!")

chien = Chien("Fido")
chien.faire_du_bruit() # Woof!
```

### Polymorphisme

*   Permet à un objet de prendre plusieurs formes.
*   En Python, le polymorphisme est souvent réalisé grâce au duck typing (si un objet se comporte comme un canard, alors c'est un canard).

```python
class Canard:
    def cancaner(self):
        print("Coin!")

class Chat:
    def cancaner(self):
        print("Miaou!")

def faire_cancaner(animal):
    animal.cancaner()

canard = Canard()
chat = Chat()

faire_cancaner(canard) # Coin!
faire_cancaner(chat) # Miaou!
```

### Encapsulation (conventions)

*   Python ne possède pas de mécanismes d'encapsulation stricts (comme `private` en Java).
*   Convention : Utilisation d'un underscore (`_`) pour indiquer qu'un attribut ou une méthode est protégé et de deux underscores (`__`) pour indiquer qu'il est privé (name mangling).

```python
class MaClasse:
    def __init__(self):
        self._attribut_protege = 10
        self.__attribut_prive = 20

    def _methode_protegee(self):
        pass

    def __methode_privee(self):
        pass
```
## 5. Modules et Packages

### Importation de modules

*   Utilisation du mot-clé `import` pour importer des modules.
*   Possibilité d'importer des modules entiers ou des éléments spécifiques d'un module.
*   Utilisation du mot-clé `as` pour renommer un module.

```python
import math

print(math.sqrt(25))

from math import sqrt, pi

print(sqrt(25))
print(pi)

import math as m

print(m.sqrt(25))
```

### Création de packages

*   Un package est un répertoire contenant un fichier `__init__.py` (qui peut être vide).
*   Les modules du package sont placés dans le même répertoire.

### Gestion des paquets (pip)

*   `pip` est le gestionnaire de paquets par défaut pour Python.
*   Permet d'installer, de mettre à jour et de supprimer des paquets.

```bash
pip install nom_du_paquet
pip uninstall nom_du_paquet
pip freeze > requirements.txt # Exporte la liste des paquets installés
pip install -r requirements.txt # Installe les paquets à partir d'un fichier
```
## 6. Gestion des Exceptions

### Blocs try-except-finally

*   Utilisation des blocs `try...except` pour capturer et gérer les exceptions.
*   Le bloc `finally` est exécuté que l'exception soit levée ou non.

```python
try:
    # Code qui peut lever une exception
    resultat = 10 / 0
except ZeroDivisionError as e:
    # Gestion de l'exception
    print("Erreur:", e)
finally:
    # Code exécuté dans tous les cas
    print("Fin du bloc try-except")
```

### Levée d'exceptions

*   Utilisation du mot-clé `raise` pour lever une exception.

```python
raise ValueError("Ceci est une erreur")
```
## 7. Entrées/Sorties (I/O)

### Lecture et écriture de fichiers

*   Utilisation des fonctions `open`, `file.read`, `file.write`, `file.close`.

```python
# Écriture dans un fichier
with open("monfichier.txt", "w") as f:
    f.write("Hello, fichier!")

# Lecture depuis un fichier
with open("monfichier.txt", "r") as f:
    contenu = f.read()
    print(contenu)
```

### Entrée utilisateur

*   Utilisation de la fonction `input` pour lire l'entrée utilisateur.

```python
nom = input("Entrez votre nom: ")
print("Bonjour, " + nom + "!")
```
## 8. Décorateurs et Générateurs

### Décorateurs

*   Les décorateurs sont des fonctions qui modifient le comportement d'autres fonctions.
*   Utilisation de la syntaxe `@decorateur` pour appliquer un décorateur.

```python
def mon_decorateur(fonction):
    def wrapper():
        print("Avant l'appel de la fonction")
        fonction()
        print("Après l'appel de la fonction")
    return wrapper

@mon_decorateur
def ma_fonction():
    print("Ma fonction est exécutée")

ma_fonction()
```

### Générateurs et itérateurs

*   Les générateurs sont des fonctions qui produisent une séquence de valeurs en utilisant le mot-clé `yield`.
*   Les itérateurs sont des objets qui permettent de parcourir une séquence de valeurs.

```python
def mon_generateur(n):
    for i in range(n):
        yield i

for valeur in mon_generateur(5):
    print(valeur)
```
## 9. Développement Web avec Python

### Frameworks (Django, Flask, FastAPI)

*   **Django** : Framework web complet et robuste, offrant de nombreuses fonctionnalités (ORM, templating, routing, etc.).
*   **Flask** : Micro-framework web léger et flexible, idéal pour les applications de petite et moyenne taille.
*   **FastAPI** : Framework web moderne et performant, basé sur les annotations de type et l'asynchronisme.

### Requêtes HTTP (requests)

*   La bibliothèque `requests` permet d'envoyer des requêtes HTTP facilement.

```python
import requests

reponse = requests.get("https://www.example.com")
print(reponse.status_code)
print(reponse.content)
```
## 10. Data Science et Machine Learning

### Bibliothèques populaires (NumPy, Pandas, Scikit-learn, TensorFlow, PyTorch)

*   **NumPy** : Bibliothèque pour le calcul numérique avec des tableaux multidimensionnels.
*   **Pandas** : Bibliothèque pour la manipulation et l'analyse de données avec des DataFrames.
*   **Scikit-learn** : Bibliothèque pour l'apprentissage automatique (classification, régression, clustering, etc.).
*   **TensorFlow** : Framework pour l'apprentissage profond (deep learning) développé par Google.
*   **PyTorch** : Autre framework pour l'apprentissage profond développé par Facebook.
## 11. Tests en Python

### unittest, pytest

*   `unittest` : Module de test unitaire intégré à Python.
*   `pytest` : Framework de test tiers, plus simple et plus puissant que `unittest`.
## 12. Bonnes Pratiques et PEP 8

### Conventions de codage (PEP 8)

*   PEP 8 est le guide de style pour le code Python.
*   Il définit les conventions de nommage, l'indentation, la longueur des lignes, etc.
*   Utiliser un linter (ex: `flake8`, `pylint`) pour vérifier le respect de PEP 8.

### Documentation (docstrings)

*   Écrire des docstrings pour documenter les fonctions, les classes et les modules.
*   Les docstrings sont des chaînes de caractères placées en première ligne d'une fonction, d'une classe ou d'un module.
*   Utiliser l'outil `pydoc` ou Sphinx pour générer la documentation à partir des docstrings.
## 13. Ressources et Communauté

### Documentation officielle

*   [Python Documentation](https://docs.python.org/3/)

### Communautés en ligne (PyPI, Stack Overflow)

*   [PyPI (Python Package Index)](https://pypi.org/) : Dépôt de paquets Python.
*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/python)](https://www.reddit.com/r/python/)

---
title: C++
draft: false
tags:
  - cpp
  - programming
description: Extension du langage C, ajoutant des fonctionnalités de programmation orientée objet, générique et fonctionnelle.
---

# Cpp

## Sommaire

1. Introduction au C++
    * Qu'est-ce que le C++ ?
    * Historique et normes (C++11, C++14, C++17, C++20)
    * Compilation et liaison
    * Structure d'un programme C++
2. Bases du Langage
    * Syntaxe de base
    * Variables et types de données
    * Opérateurs
    * Structures de contrôle
    * Fonctions
    * Pointeurs et Références
3. Programmation Orientée Objet (POO) en C++
    * Classes et Objets
    * Constructeurs et Destructeurs
    * Encapsulation, Héritage, Polymorphisme
    * Fonctions virtuelles et Classes abstraites
4. Gestion de la Mémoire
    * Allocation statique, dynamique (new, delete)
    * Pointeurs intelligents (smart pointers)
5. Templates (Programmation Générique)
    * Templates de fonctions
    * Templates de classes
6. Bibliothèque Standard C++ (STL)
    * Conteneurs (Vector, List, Map, Set)
    * Algorithmes
    * Itérateurs
    * Flux d'entrée/sortie (iostream)
7. Gestion des Exceptions
    * Blocs try-catch
    * Levée d'exceptions
8. Multithreading
    * Le modèle mémoire C++
    * Threads (std::thread)
    * Mutexes et conditions variables
9. Nouvelles Fonctionnalités des Normes C++ Modernes
    * Lambdas
    * Auto
    * Rvalue references et move semantics
    * Concepts
10. Compilation et Débogage
    * Utilisation de G++
    * Options de compilation
    * Débogage avec GDB
11. Bonnes Pratiques et Patterns
    * Conventions de codage
    * Patterns de conception courants
    * RAII (Resource Acquisition Is Initialization)
12. Ressources et Communauté
    * Documentation
    * Communautés en ligne

## 1. Introduction Au C++

### Qu'est-ce Que Le C++ ?

Extension du C, ajoutant la POO, la programmation générique et fonctionnelle. Langage compilé, performant, utilisé pour systèmes d'exploitation, jeux, applications embarquées, etc.

### Historique Et Normes (C++11, C++14, C++17, C++20)

* **C++98/03**: Première norme standard.
* **C++11**: Ajout majeur (lambdas, auto, smart pointers, threads).
* **C++14**: Améliorations mineures.
* **C++17**: Améliorations (structured bindings, if constexpr).
* **C++20**: Ajouts significatifs (Concepts, Coroutines, Modules, Ranges).

### Compilation Et Liaison

1. **Préprocesseur**: Traite les directives (`#include`, `#define`).
2. **Compilation**: Convertit le code source (`.cpp`) en code objet (`.o`).
3. **Liaison (Linking)**: Combine les fichiers objet et les bibliothèques pour créer l'exécutable.

```cpp
// Exemple simple de compilation avec g++
// Sauvegarder sous main.cpp
#include <iostream>

int main() {
   std::cout << "Bonjour, monde!" << std::endl;
   return 0;
}
```

```bash
# Compiler : crée main.o
g++ -c main.cpp
# Lier : crée l'exécutable a.out (ou main sur Windows)
g++ main.o -o main
# Exécuter
./main
```

### Structure D'un Programme C++

```cpp
#include <iostream> // Inclusion de la bibliothèque iostream

int main() { // Fonction principale, point d'entrée du programme
   // Corps de la fonction main
   std::cout << "Hello, World!"; // Affichage à la console
   return 0; // Indique que le programme s'est terminé sans erreur
}
```

## 2. Bases Du Langage

### Syntaxe De Base

* Les instructions se terminent par un point-virgule (`;`).
* Les commentaires commencent par `//` (ligne unique) ou sont encadrés par `/* */` (bloc).
* Les blocs de code sont délimités par des accolades (`{}`).

```cpp
// Ceci est un commentaire sur une seule ligne

/*
Ceci est un
commentaire
sur plusieurs lignes
*/

int main() {
    int a = 10; // Instruction
    { // Bloc de code
        int b = 20;
    }
    return 0;
}
```

### Variables Et Types De Données

* Déclaration: `type nom_variable;`
* Initialisation: `type nom_variable = valeur;`

Types de base :
* `int`: Entiers
* `float`, `double`: Nombres à virgule flottante
* `char`: Caractères
* `bool`: Booléens (`true`, `false`)
* `void`: Absence de type

```cpp
int age = 30;
double price = 19.99;
char initial = 'A';
bool is_active = true;
```

### Opérateurs

* **Arithmétiques**: `+`, `-`, `*`, `/`, `%`
* **Relationnels**: `==`, `!=`, `<`, `>`, `<=`, `>=`
* **Logiques**: `&&` (ET), `||` (OU), `!` (NON)
* **Affectation**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`
* **Incrémentation/Décrémentation**: `++`, `--`

```cpp
int x = 10, y = 5;
int sum = x + y; // 15
bool is_equal = (x == y); // false
bool condition = (x > 0 && y < 10); // true
x++; // x devient 11
```

### Structures De Contrôle

* **Conditionnelles**: `if`, `else if`, `else`, `switch`
* **Boucles**: `for`, `while`, `do-while`

```cpp
int score = 85;
if (score > 90) {
    // ...
} else if (score > 80) {
    // ...
} else {
    // ...
}

for (int i = 0; i < 5; i++) {
    // ...
}

while (score > 0) {
    // ...
    score--;
}
```

### Fonctions

* Déclaration: `type_retour nom_fonction(paramètres);`
* Définition: `type_retour nom_fonction(paramètres) { // corps }`
* Appel: `nom_fonction(arguments);`

```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3); // Appel de fonction
    return 0;
}
```

### Pointeurs Et Références

* **Pointeur**: Variable qui stocke l'adresse mémoire d'une autre variable. Déclaration: `type* nom_pointeur;`
* **Référence**: Alias d'une variable existante. Déclaration: `type& nom_reference = variable_existante;`

```cpp
int var = 10;
int* ptr = &var; // ptr stocke l'adresse de var
int& ref = var; // ref est un alias de var

std::cout << *ptr; // Affiche la valeur pointée par ptr (10)
ref = 20; // Modifie var via la référence
std::cout << var; // Affiche 20
```

## 3. Programmation Orientée Objet (POO) En C++

### Classes Et Objets

* **Classe**: Modèle pour créer des objets. Définit les données (attributs) et les comportements (méthodes).
* **Objet**: Instance d'une classe.

```cpp
class Dog {
public: // Membres accessibles de l'extérieur
    std::string name;
    int age;

    void bark() {
        std::cout << name << " says Woof!" << std::endl;
    }
};

int main() {
    Dog my_dog; // Création d'un objet Dog
    my_dog.name = "Buddy";
    my_dog.age = 3;
    my_dog.bark(); // Appel de méthode
    return 0;
}
```

### Constructeurs Et Destructeurs

* **Constructeur**: Méthode spéciale appelée lors de la création d'un objet. Initialise l'objet. Nom identique à la classe.
* **Destructeur**: Méthode spéciale appelée lors de la destruction d'un objet. Nettoie les ressources. Nom de la classe précédé de `~`.

```cpp
class MyClass {
public:
    // Constructeur par défaut
    MyClass() {
        std::cout << "Constructeur appelé" << std::endl;
    }

    // Constructeur avec paramètres
    MyClass(int val) {
        std::cout << "Constructeur avec paramètre appelé: " << val << std::endl;
    }

    // Destructeur
    ~MyClass() {
        std::cout << "Destructeur appelé" << std::endl;
    }
};

int main() {
    MyClass obj1; // Appelle le constructeur par défaut
    MyClass obj2(10); // Appelle le constructeur avec paramètre
    // Les destructeurs sont appelés automatiquement à la fin de main()
    return 0;
}
```

### Encapsulation, Héritage, Polymorphisme

* **Encapsulation**: Regrouper données et méthodes au sein d'une classe. Contrôler l'accès (public, private, protected).
* **Héritage**: Une classe (dérivée) hérite des propriétés et comportements d'une autre classe (base). `class Derived : public Base { … };`
* **Polymorphisme**: Possibilité de traiter des objets de classes différentes de manière uniforme via une interface commune (souvent avec des pointeurs/références et des fonctions virtuelles).

```cpp
// Encapsulation
class Account {
private:
    double balance; // Donnée privée

public:
    void deposit(double amount) {
        balance += amount;
    }
};

// Héritage
class Animal {
public:
    void eat() { std::cout << "Eating..." << std::endl; }
};

class Dog : public Animal { // Dog hérite de Animal
public:
    void bark() { std::cout << "Woof!" << std::endl; }
};

// Polymorphisme (voir Fonctions virtuelles)
```

### Fonctions Virtuelles Et Classes Abstraites

* **Fonction virtuelle**: Fonction dans une classe de base déclarée avec le mot-clé `virtual`. Permet le polymorphisme dynamique (résolution de l'appel de fonction à l'exécution).
* **Classe abstraite**: Classe qui ne peut pas être instanciée directement. Contient au moins une fonction virtuelle pure (`= 0`). Sert de classe de base pour l'héritage.

```cpp
class Shape { // Classe de base abstraite
public:
    virtual double area() const = 0; // Fonction virtuelle pure
    virtual ~Shape() {} // Destructeur virtuel
};

class Circle : public Shape {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    double area() const override { // Implémentation de la fonction virtuelle pure
        return 3.14 * radius * radius;
    }
};

class Square : public Shape {
private:
    double side;
public:
    Square(double s) : side(s) {}
    double area() const override { // Implémentation de la fonction virtuelle pure
        return side * side;
    }
};

int main() {
    // Shape s; // Erreur: ne peut pas instancier une classe abstraite
    Shape* shape1 = new Circle(5);
    Shape* shape2 = new Square(4);

    std::cout << "Area of Circle: " << shape1->area() << std::endl; // Polymorphisme
    std::cout << "Area of Square: " << shape2->area() << std::endl;

    delete shape1;
    delete shape2;
    return 0;
}
```

## 4. Gestion De la Mémoire

### Allocation Statique, Dynamique (new, delete)

* **Allocation statique**: Mémoire allouée au moment de la compilation (variables globales, locales, membres de classe non-pointeurs). Gérée automatiquement.
* **Allocation dynamique**: Mémoire allouée à l'exécution sur le tas (heap) avec `new`. Doit être libérée explicitement avec `delete` pour éviter les fuites de mémoire.

```cpp
int static_var; // Allocation statique

int* dynamic_var = new int; // Allocation dynamique d'un entier
*dynamic_var = 10;
delete dynamic_var; // Libération de la mémoire

int* dynamic_array = new int[5]; // Allocation dynamique d'un tableau
dynamic_array[0] = 1;
delete[] dynamic_array; // Libération du tableau
```

### Pointeurs Intelligents (smart pointers)

Objets qui gèrent automatiquement la mémoire allouée dynamiquement, évitant les fuites de mémoire.

* `std::unique_ptr`: Pointeur qui possède exclusivement l'objet pointé. Ne peut pas être copié, seulement déplacé.
* `std::shared_ptr`: Pointeur qui partage la propriété de l'objet pointé. Utilise un compteur de références. L'objet est détruit quand le dernier `shared_ptr` est détruit.
* `std::weak_ptr`: Pointeur non-possédant. Utilisé avec `shared_ptr` pour éviter les références circulaires.

```cpp
#include <memory>

int main() {
    // unique_ptr
    std::unique_ptr<int> uptr = std::make_unique<int>(10);
    // std::unique_ptr<int> uptr2 = uptr; // Erreur: ne peut pas copier
    std::unique_ptr<int> uptr2 = std::move(uptr); // Déplacement

    // shared_ptr
    std::shared_ptr<int> sptr = std::make_shared<int>(20);
    std::shared_ptr<int> sptr2 = sptr; // Copie, le compteur de références augmente

    // weak_ptr
    std::weak_ptr<int> wptr = sptr; // Ne change pas le compteur de références

    return 0;
} // La mémoire est libérée automatiquement par les smart pointers
```

## 5. Templates (Programmation Générique)

Permet d'écrire du code qui fonctionne avec différents types de données sans répéter le code pour chaque type.

### Templates De Fonctions

Crée une famille de fonctions pour différents types.

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    int i_max = max(5, 10); // T est déduit comme int
    double d_max = max(3.14, 1.618); // T est déduit comme double
    return 0;
}
```

### Templates De Classes

Crée une famille de classes pour différents types.

```cpp
template <typename T>
class MyContainer {
private:
    T value;
public:
    MyContainer(T val) : value(val) {}
    T getValue() const { return value; }
};

int main() {
    MyContainer<int> int_container(100);
    MyContainer<std::string> string_container("Hello");

    std::cout << int_container.getValue() << std::endl;
    std::cout << string_container.getValue() << std::endl;

    return 0;
}
```

## 6. Bibliothèque Standard C++ (STL)

Ensemble de classes et fonctions templates fournissant des structures de données et algorithmes courants.

### Conteneurs (Vector, List, Map, Set)

Stockent des collections d'objets.

* `std::vector`: Tableau dynamique. Accès rapide par index.
* `std::list`: Liste doublement chaînée. Insertions/suppressions rapides n'importe où.
* `std::map`: Conteneur associatif clé-valeur trié. Accès rapide par clé.
* `std::set`: Conteneur d'éléments uniques triés.

```cpp
#include <vector>
#include <list>
#include <map>
#include <set>
#include <string>
#include <iostream>

int main() {
    std::vector<int> v = {1, 2, 3};
    v.push_back(4); // Ajoute un élément

    std::list<int> l = {10, 20, 30};
    l.push_front(5); // Ajoute au début

    std::map<std::string, int> m;
    m["apple"] = 1;
    m["banana"] = 2;
    std::cout << m["apple"] << std::endl; // Accès par clé

    std::set<int> s = {1, 2, 3, 2}; // Le 2 en double est ignoré
    for (int val : s) {
        std::cout << val << " "; // Affiche 1 2 3
    }
    std::cout << std::endl;

    return 0;
}
```

### Algorithmes

Fonctions templates pour effectuer des opérations sur des plages d'éléments (souvent avec des itérateurs).

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {10, 20, 5, 15};
    std::sort(v.begin(), v.end()); // Trie le vecteur

    for (int val : v) {
        std::cout << val << " "; // Affiche 5 10 15 20
    }
    std::cout << std::endl;

    int count = std::count(v.begin(), v.end(), 10); // Compte les occurrences de 10
    std::cout << "Count of 10: " << count << std::endl;

    return 0;
}
```

### Itérateurs

Objets qui permettent de parcourir les éléments des conteneurs. Se comportent comme des pointeurs.

* `begin()`: Retourne un itérateur sur le premier élément.
* `end()`: Retourne un itérateur "past-the-end".

```cpp
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};
    for (auto it = v.begin(); it != v.end(); ++it) {
        std::cout << *it << " "; // Accès à l'élément via l'itérateur
    }
    std::cout << std::endl;
    return 0;
}
```

### Flux d'entrée/sortie (iostream)

Gère les opérations d'entrée et de sortie (console, fichiers).

* `std::cin`: Flux d'entrée standard (clavier).
* `std::cout`: Flux de sortie standard (console).
* `std::cerr`: Flux d'erreur standard.
* `std::clog`: Flux de journalisation standard.

```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name; // Lit l'entrée de l'utilisateur
    std::cout << "Hello, " << name << "!" << std::endl; // Affiche la sortie
    return 0;
}
```

## 7. Gestion Des Exceptions

Mécanisme pour gérer les erreurs et autres événements exceptionnels pendant l'exécution.

### Blocs Try-catch

Utilisé pour intercepter et gérer les exceptions.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v(5);
    try {
        // Tente d'accéder à un élément hors limites
        v.at(10) = 100;
    } catch (const std::out_of_range& e) {
        // Attrape l'exception std::out_of_range
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

### Levée D'exceptions

Utilisé pour signaler qu'une erreur ou une condition exceptionnelle s'est produite.

```cpp
#include <iostream>
#include <stdexcept> // Pour std::runtime_error

double divide(double numerator, double denominator) {
    if (denominator == 0) {
        throw std::runtime_error("Division by zero error!"); // Lève une exception
    }
    return numerator / denominator;
}

int main() {
    try {
        double result = divide(10.0, 0.0);
        std::cout << "Result: " << result << std::endl;
    } catch (const std::runtime_error& e) {
        std::cerr << "Error: " << e.what() << std::endl; // Attrape et affiche l'erreur
    }
    return 0;
}
```

## 8. Multithreading

Permet d'exécuter plusieurs parties d'un programme simultanément.

### Le Modèle Mémoire C++

Définit comment les threads interagissent avec la mémoire. Assure la cohérence des données partagées.

### Threads (std::thread)

Représente un thread d'exécution.

```cpp
#include <iostream>
#include <thread>

void task() {
    std::cout << "Task running in a separate thread" << std::endl;
}

int main() {
    std::thread t(task); // Crée et lance un nouveau thread
    // Le thread principal continue son exécution

    t.join(); // Attend que le thread t se termine
    // t.detach(); // Détache le thread (il s'exécute indépendamment)

    std::cout << "Main thread finished" << std::endl;
    return 0;
}
```

### Mutexes Et Conditions Variables

Utilisés pour synchroniser l'accès aux ressources partagées et éviter les conditions de course.

* `std::mutex`: Verrouille l'accès à une section critique.
* `std::condition_variable`: Permet à un thread d'attendre qu'une certaine condition soit remplie.

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void worker_thread() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, []{ return ready; }); // Attend que ready soit true
    std::cout << "Worker thread is running" << std::endl;
}

int main() {
    std::thread worker(worker_thread);

    // Faire d'autres choses...

    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true; // Change la condition
    } // lock_guard libère le mutex en sortant du scope
    cv.notify_one(); // Notifie le thread en attente

    worker.join();
    return 0;
}
```

## 9. Nouvelles Fonctionnalités Des Normes C++ Modernes

Introduites dans C++11 et les normes ultérieures pour améliorer la productivité et les performances.

### Lambdas

Fonctions anonymes (sans nom) qui peuvent être définies et utilisées sur place. Utiles pour les algorithmes de la STL.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v = {1, 5, 2, 8, 3};
    int count_greater_than_3 = std::count_if(v.begin(), v.end(),
        [](int x){ return x > 3; }); // Lambda
    std::cout << "Count greater than 3: " << count_greater_than_3 << std::endl; // Affiche 2
    return 0;
}
```

### Auto

Permet au compilateur de déduire automatiquement le type d'une variable.

```cpp
#include <vector>
#include <iostream>

int main() {
    auto i = 10; // i est de type int
    auto d = 3.14; // d est de type double
    std::vector<int> v = {1, 2, 3};
    for (auto it = v.begin(); it != v.end(); ++it) { // it est un itérateur
        std::cout << *it << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

### Rvalue References Et Move Semantics

* **Rvalue reference (`&&`)**: Référence à une valeur temporaire (rvalue). Permet de distinguer les lvalues (qui ont une identité et persistent au-delà d'une expression) des rvalues.
* **Move semantics**: Permet de "déplacer" efficacement les ressources (comme la mémoire allouée dynamiquement) d'un objet rvalue à un autre, au lieu de faire une copie coûteuse. Utilisé dans les constructeurs et opérateurs d'affectation par déplacement (`&&`).

```cpp
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v1 = {1, 2, 3};
    std::vector<int> v2 = std::move(v1); // Déplace les ressources de v1 vers v2
    // Après le déplacement, v1 est dans un état valide mais indéterminé (souvent vide)
    std::cout << "v2 size: " << v2.size() << std::endl; // Affiche 3
    // std::cout << "v1 size: " << v1.size() << std::endl; // Peut afficher 0 ou autre, ne pas se fier
    return 0;
}
```

### Concepts (C++20)

Contraintes sur les paramètres de templates pour améliorer la lisibilité des erreurs de compilation et exprimer les intentions.

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <concepts> // Nécessite C++20

// Définit un concept pour les types qui peuvent être triés
template<typename T>
concept Sortable = requires(T a, T b) {
    { a < b } -> std::same_as<bool>; // a < b doit être valide et retourner un bool
    { a > b } -> std::same_as<bool>; // a > b doit être valide et retourner un bool
};

// Fonction template contrainte par le concept Sortable
template<Sortable T>
void print_sorted(std::vector<T>& v) {
    std::sort(v.begin(), v.end());
    for (const auto& val : v) {
        std::cout << val << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> numbers = {3, 1, 4, 1, 5, 9};
    print_sorted(numbers); // Fonctionne car int satisfait Sortable

    // std::vector<std::list<int>> lists;
    // print_sorted(lists); // Erreur de compilation claire car std::list ne satisfait pas Sortable

    return 0;
}
```

## 10. Compilation Et Débogage

### Utilisation De G++

G++ est le compilateur GNU pour C++.

```bash
# Compiler un seul fichier source
g++ main.cpp -o main

# Compiler plusieurs fichiers source
g++ file1.cpp file2.cpp -o program

# Compiler et lier séparément
g++ -c file1.cpp # Crée file1.o
g++ -c file2.cpp # Crée file2.o
g++ file1.o file2.o -o program # Lie les fichiers objet
```

### Options De Compilation

Quelques options courantes de G++:

* `-o <output>`: Spécifie le nom du fichier de sortie.
* `-c`: Compile seulement, ne lie pas.
* `-Wall`: Active la plupart des avertissements. Très recommandé.
* `-Wextra`: Active des avertissements supplémentaires.
* `-g`: Inclut les informations de débogage pour GDB.
* `-O<level>`: Optimise le code (`-O1`, `-O2`, `-O3`, `-Os`).
* `-std=<standard>`: Spécifie la norme C++ (`c++11`, `c++14`, `c++17`, `c++20`).
* `-I<directory>`: Ajoute un répertoire pour la recherche des fichiers d'en-tête.
* `-L<directory>`: Ajoute un répertoire pour la recherche des bibliothèques.
* `-l<library>`: Lie avec une bibliothèque (ex: `-lpthread` pour les threads).

```bash
# Exemple avec plusieurs options
g++ main.cpp -o main -Wall -Wextra -g -O2 -std=c++17 -Iinclude -Llib -lmylib
```

### Débogage Avec GDB

GDB (GNU Debugger) est un outil puissant pour trouver et corriger les erreurs dans les programmes C++.

1. **Compiler avec les informations de débogage**: Utilisez l'option `-g` lors de la compilation.

    ```bash
    g++ main.cpp -o main -g
    ```

2. **Lancer GDB**:

    ```bash
    gdb ./main
    ```

3. **Commandes GDB courantes**:
    * `run` (`r`): Exécute le programme.
    * `break <location>` (`b`): Définit un point d'arrêt (ligne, fonction). Ex: `b main.cpp:10`, `b my_function`.
    * `continue` (`c`): Continue l'exécution jusqu'au prochain point d'arrêt.
    * `next` (`n`): Exécute la ligne de code suivante (passe par-dessus les appels de fonction).
    * `step` (`s`): Exécute la ligne de code suivante (entre dans les appels de fonction).
    * `print <variable>` (`p`): Affiche la valeur d'une variable.
    * `info locals`: Affiche les variables locales.
    * `backtrace` (`bt`): Affiche la pile d'appels.
    * `quit` (`q`): Quitte GDB.

```gdb
# Exemple de session GDB
(gdb) break main.cpp:15
Breakpoint 1 at 0x...: file main.cpp, line 15.
(gdb) run
Starting program: /path/to/main

Breakpoint 1, main() at main.cpp:15
15          int x = 10;
(gdb) next
16          int y = 20;
(gdb) print x
$1 = 10
(gdb) continue
... programme continue ...
(gdb) quit
```

## 11. Bonnes Pratiques Et Patterns

Conseils pour écrire du code C++ propre, efficace et maintenable.

### Conventions De Codage

* Cohérence dans le nommage (variables, fonctions, classes).
* Indentation et formatage uniformes.
* Utilisation judicieuse des commentaires.
* Éviter les variables globales autant que possible.
* Préférer les constantes (`const`, `constexpr`).

### Patterns De Conception Courants

* **Singleton**: Assure qu'une classe n'a qu'une seule instance et fournit un point d'accès global à celle-ci.
* **Factory Method**: Définit une interface pour créer un objet, mais laisse les sous-classes décider quelle classe instancier.
* **Observer**: Définit une dépendance un-à-plusieurs entre objets, de sorte que lorsque un objet change d'état, tous ses dépendants sont notifiés et mis à jour automatiquement.

### RAII (Resource Acquisition Is Initialization)

Principe clé en C++ pour la gestion des ressources (mémoire, fichiers, verrous). Les ressources sont acquises lors de l'initialisation d'un objet et libérées automatiquement lorsque l'objet est détruit (grâce aux destructeurs). Les pointeurs intelligents sont un exemple de RAII.

```cpp
#include <fstream>
#include <iostream>

class FileHandler {
private:
    std::ofstream file;
public:
    FileHandler(const std::string& filename) {
        file.open(filename);
        if (!file.is_open()) {
            throw std::runtime_error("Could not open file");
        }
        std::cout << "File opened: " << filename << std::endl;
    }

    ~FileHandler() {
        if (file.is_open()) {
            file.close();
            std::cout << "File closed" << std::endl;
        }
    }

    void write(const std::string& data) {
        if (file.is_open()) {
            file << data;
        }
    }
};

int main() {
    try {
        FileHandler handler("my_log.txt");
        handler.write("Logging some data.\n");
        // Le fichier sera automatiquement fermé lorsque handler sortira du scope
    } catch (const std::runtime_error& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }
    return 0;
} // Le destructeur de handler est appelé ici, fermant le fichier
```

## 12. Ressources Et Communauté

### Documentation

* **cppreference.com**: Documentation de référence complète de la bibliothèque standard C++.
* **cplusplus.com**: Tutoriels et références sur le langage C++.
* **ISO C++ Standard**: La norme officielle du langage C++.

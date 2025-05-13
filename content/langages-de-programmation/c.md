---
title: C
draft: false
tags:
  - c
  - programming
description: Langage de programmation structuré, compilé, de bas niveau, largement utilisé pour les systèmes d'exploitation, les systèmes embarqués et les jeux.
---

## Sommaire

1.  Introduction au C
    *   Qu'est-ce que le C ?
    *   Historique et importance
    *   Compilation et liaison
    *   Structure d'un programme C
2.  Bases du Langage
    *   Syntaxe de base
    *   Variables et types de données (int, float, char, etc.)
    *   Opérateurs
    *   Structures de contrôle (if, for, while, switch)
    *   Fonctions
3.  Pointeurs
    *   Déclaration et utilisation des pointeurs
    *   Arithmétique des pointeurs
    *   Pointeurs et tableaux
    *   Allocation dynamique de mémoire (malloc, calloc, realloc, free)
4.  Tableaux et Chaînes de Caractères
    *   Déclaration et initialisation des tableaux
    *   Tableaux multidimensionnels
    *   Manipulation des chaînes de caractères (bibliothèque string.h)
5.  Structures et Unions
    *   Déclaration et utilisation des structures
    *   Structures imbriquées
    *   Unions
6.  Fichiers
    *   Ouverture et fermeture de fichiers (fopen, fclose)
    *   Lecture et écriture dans les fichiers (fprintf, fscanf, fread, fwrite)
7.  Préprocesseur C
    *   Directives (include, define, ifdef, etc.)
    *   Macros
8.  Gestion de la Mémoire
    *   Pile (Stack) et Tas (Heap)
    *   Allocation statique et dynamique
    *   Problèmes courants (fuites de mémoire, pointeurs pendants)
9.  Bibliothèque Standard C
    *   Principales bibliothèques (stdio.h, stdlib.h, string.h, math.h)
10. Compilation et Débogage
    *   Utilisation de GCC
    *   Options de compilation
    *   Débogage avec GDB
11. Bonnes Pratiques
    *   Conventions de codage
    *   Gestion des erreurs
12. Ressources et Communauté
    *   Documentation
    *   Communautés en ligne

## 1. Introduction au C

### Qu'est-ce que le C ?

Langage de programmation structuré, impératif, de bas niveau. Conçu pour être portable et efficace. Utilisé pour systèmes d'exploitation, systèmes embarqués, développement de pilotes, etc.

### Historique et importance

*   Développé par Dennis Ritchie chez Bell Labs dans les années 1970.
*   Fortement lié au développement du système d'exploitation Unix.
*   Influence majeure sur de nombreux langages (C++, Java, C#, etc.).
*   Toujours largement utilisé aujourd'hui pour sa performance et son contrôle bas niveau.

### Compilation et liaison

1.  **Préprocesseur**: Traite les directives (`#include`, `#define`).
2.  **Compilation**: Convertit le code source (`.c`) en code assembleur.
3.  **Assembleur**: Convertit le code assembleur en code objet (`.o`).
4.  **Liaison (Linking)**: Combine les fichiers objet et les bibliothèques pour créer l'exécutable.

```c
// Exemple simple de compilation avec gcc
// Sauvegarder sous main.c
#include <stdio.h>

int main() {
   printf("Bonjour, monde!\n");
   return 0;
}
```

```bash
# Compiler et lier : crée l'exécutable a.out (ou main sur Windows)
gcc main.c -o main
# Exécuter
./main
```

### Structure d'un programme C

```c
#include <stdio.h> // Inclusion de la bibliothèque standard d'entrée/sortie

int main() { // Fonction principale, point d'entrée du programme
   // Corps de la fonction main
   printf("Hello, World!"); // Affichage à la console
   return 0; // Indique que le programme s'est terminé sans erreur
}
```

## 2. Bases du Langage

### Syntaxe de base

*   Les instructions se terminent par un point-virgule (`;`).
*   Les commentaires commencent par `//` (ligne unique) ou sont encadrés par `/* */` (bloc).
*   Les blocs de code sont délimités par des accolades (`{}`).

```c
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

### Variables et types de données (int, float, char, etc.)

*   Déclaration: `type nom_variable;`
*   Initialisation: `type nom_variable = valeur;`

Types de base :
*   `int`: Entiers
*   `float`: Nombres à virgule flottante simple précision
*   `double`: Nombres à virgule flottante double précision
*   `char`: Caractères
*   `void`: Absence de type

```c
int age = 30;
float price = 19.99;
char initial = 'A';
```

### Opérateurs

*   **Arithmétiques**: `+`, `-`, `*`, `/`, `%`
*   **Relationnels**: `==`, `!=`, `<`, `>`, `<=`, `>=`
*   **Logiques**: `&&` (ET), `||` (OU), `!` (NON)
*   **Affectation**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`
*   **Incrémentation/Décrémentation**: `++`, `--`

```c
int x = 10, y = 5;
int sum = x + y; // 15
int is_equal = (x == y); // 0 (faux)
int condition = (x > 0 && y < 10); // 1 (vrai)
x++; // x devient 11
```

### Structures de contrôle (if, for, while, switch)

*   **Conditionnelles**: `if`, `else if`, `else`, `switch`
*   **Boucles**: `for`, `while`, `do-while`

```c
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

*   Déclaration: `type_retour nom_fonction(paramètres);`
*   Définition: `type_retour nom_fonction(paramètres) { // corps }`
*   Appel: `nom_fonction(arguments);`

```c
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3); // Appel de fonction
    return 0;
}
```

## 3. Pointeurs

### Déclaration et utilisation des pointeurs

*   Un pointeur est une variable qui stocke l'adresse mémoire d'une autre variable.
*   Déclaration: `type *nom_pointeur;`
*   Opérateur d'adresse: `&` (retourne l'adresse d'une variable)
*   Opérateur de déréférencement: `*` (accède à la valeur pointée par le pointeur)

```c
int var = 10;
int *ptr; // Déclaration d'un pointeur vers un entier

ptr = &var; // ptr stocke l'adresse de var

printf("Adresse de var: %p\n", &var); // Affiche l'adresse de var
printf("Valeur de ptr: %p\n", ptr); // Affiche la valeur de ptr (l'adresse de var)
printf("Valeur de var: %d\n", var); // Affiche la valeur de var (10)
printf("Valeur pointée par ptr: %d\n", *ptr); // Affiche la valeur pointée par ptr (10)

*ptr = 20; // Modifie la valeur de var via le pointeur
printf("Nouvelle valeur de var: %d\n", var); // Affiche 20
```

### Arithmétique des pointeurs

*   Possibilité d'incrémenter ou de décrémenter un pointeur pour accéder à des éléments contigus en mémoire (ex: éléments d'un tableau).
*   L'incrémentation d'un pointeur de 1 le fait avancer d'une taille de `type`.

```c
int arr[5] = {10, 20, 30, 40, 50};
int *ptr = arr; // ptr pointe vers le premier élément de arr

printf("Valeur de arr[0]: %d\n", *ptr); // 10
ptr++; // ptr pointe vers le prochain élément (arr[1])
printf("Valeur de arr[1]: %d\n", *ptr); // 20
```

### Pointeurs et tableaux

*   Le nom d'un tableau est équivalent à un pointeur vers son premier élément.
*   `arr[i]` est équivalent à `*(arr + i)`.

```c
int arr[5] = {10, 20, 30, 40, 50};
int *ptr = arr;

printf("arr[2]: %d\n", arr[2]); // 30
printf("*(arr + 2): %d\n", *(arr + 2)); // 30
printf("ptr[2]: %d\n", ptr[2]); // 30
printf("*(ptr + 2): %d\n", *(ptr + 2)); // 30
```

### Allocation dynamique de mémoire (malloc, calloc, realloc, free)

*   `malloc()`: Alloue un bloc de mémoire de la taille spécifiée (en octets). Ne l'initialise pas. Retourne un pointeur `void*`.
*   `calloc()`: Alloue un bloc de mémoire pour un nombre spécifié d'éléments d'une taille spécifiée. Initialise la mémoire à zéro. Retourne un pointeur `void*`.
*   `realloc()`: Redimensionne un bloc de mémoire précédemment alloué.
*   `free()`: Libère un bloc de mémoire précédemment alloué avec `malloc`, `calloc` ou `realloc`.

```c
#include <stdio.h>
#include <stdlib.h> // Pour malloc, calloc, realloc, free

int main() {
    int *ptr;

    // Allocation avec malloc
    ptr = (int*)malloc(5 * sizeof(int)); // Alloue de la mémoire pour 5 entiers
    if (ptr == NULL) {
        printf("Erreur d'allocation mémoire\n");
        return 1;
    }
    ptr[0] = 10;
    free(ptr); // Libère la mémoire

    // Allocation avec calloc
    ptr = (int*)calloc(5, sizeof(int)); // Alloue et initialise à zéro
    if (ptr == NULL) {
        printf("Erreur d'allocation mémoire\n");
        return 1;
    }
    free(ptr);

    return 0;
}
```

## 4. Tableaux et Chaînes de Caractères

### Déclaration et initialisation des tableaux

*   Un tableau est une collection d'éléments du même type stockés de manière contiguë en mémoire.
*   Déclaration: `type nom_tableau[taille];`
*   Initialisation: `type nom_tableau[taille] = {valeur1, valeur2, ...};`

```c
int numbers[5]; // Déclaration d'un tableau de 5 entiers
int values[3] = {10, 20, 30}; // Déclaration et initialisation
char message[] = "Hello"; // Déclaration et initialisation d'un tableau de caractères (chaîne)
```

### Tableaux multidimensionnels

*   Tableaux avec plusieurs dimensions (ex: matrices).
*   Déclaration: `type nom_tableau[taille1][taille2]...;`

```c
int matrix[3][3]; // Déclaration d'une matrice 3x3
int grid[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

### Manipulation des chaînes de caractères (bibliothèque string.h)

*   En C, les chaînes de caractères sont des tableaux de `char` se terminant par un caractère nul (`\0`).
*   La bibliothèque `string.h` fournit des fonctions pour manipuler les chaînes (ex: `strcpy`, `strlen`, `strcat`, `strcmp`).

```c
#include <stdio.h>
#include <string.h> // Pour les fonctions de manipulation de chaînes

int main() {
    char str1[20] = "Hello";
    char str2[] = " World";
    char dest[50];

    strcpy(dest, str1); // Copie str1 dans dest
    strcat(dest, str2); // Concatène str2 à la fin de dest

    printf("Chaîne concaténée: %s\n", dest); // Affiche "Hello World"
    printf("Longueur de la chaîne: %zu\n", strlen(dest)); // Affiche 11

    if (strcmp(str1, "Hello") == 0) {
        printf("str1 est égal à \"Hello\"\n");
    }

    return 0;
}
```

## 5. Structures et Unions

### Déclaration et utilisation des structures

*   Une structure est un type de données composite qui regroupe des variables de types différents sous un seul nom.
*   Déclaration:
    ```c
    struct nom_structure {
        type membre1;
        type membre2;
        ...
    };
    ```
*   Utilisation:
    ```c
    struct nom_structure nom_variable;
    nom_variable.membre1 = valeur;
    ```

```c
#include <stdio.h>

struct Person {
    char name[50];
    int age;
    float height;
};

int main() {
    struct Person person1;

    // Initialisation
    strcpy(person1.name, "John Doe");
    person1.age = 30;
    person1.height = 1.75;

    // Affichage
    printf("Nom: %s\n", person1.name);
    printf("Âge: %d\n", person1.age);
    printf("Taille: %.2f\n", person1.height);

    return 0;
}
```

### Structures imbriquées

*   Une structure peut contenir d'autres structures comme membres.

```c
#include <stdio.h>
#include <string.h>

struct Address {
    char street[100];
    char city[50];
    char zip[10];
};

struct Person {
    char name[50];
    int age;
    struct Address address; // Structure imbriquée
};

int main() {
    struct Person person1;

    strcpy(person1.name, "Jane Smith");
    person1.age = 25;
    strcpy(person1.address.street, "123 Main St");
    strcpy(person1.address.city, "Anytown");
    strcpy(person1.address.zip, "12345");

    printf("Nom: %s\n", person1.name);
    printf("Adresse: %s, %s %s\n", person1.address.street, person1.address.city, person1.address.zip);

    return 0;
}
```

### Unions

*   Une union est un type de données qui peut stocker différents types de données dans la même zone de mémoire. Seul un membre peut être utilisé à la fois.
*   Déclaration:
    ```c
    union nom_union {
        type membre1;
        type membre2;
        ...
    };
    ```

```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;

    data.i = 10;
    printf("data.i: %d\n", data.i);

    data.f = 22.5;
    printf("data.f: %.2f\n", data.f); // data.i est écrasé

    strcpy(data.str, "C Programming");
    printf("data.str: %s\n", data.str); // data.i et data.f sont écrasés

    return 0;
}
```

## 6. Fichiers

### Ouverture et fermeture de fichiers (fopen, fclose)

*   `fopen()`: Ouvre un fichier. Retourne un pointeur vers la structure `FILE`.
*   `fclose()`: Ferme un fichier.

Modes d'ouverture courants:
*   `"r"`: Lecture seule.
*   `"w"`: Écriture (écrase le contenu existant).
*   `"a"`: Ajout (écrit à la fin du fichier).
*   `"rb"`, `"wb"`, `"ab"`: Modes binaires correspondants.

```c
#include <stdio.h>

int main() {
    FILE *fp;

    // Ouverture en écriture
    fp = fopen("my_file.txt", "w");
    if (fp == NULL) {
        printf("Erreur lors de l'ouverture du fichier\n");
        return 1;
    }

    // Fermeture du fichier
    fclose(fp);
    printf("Fichier fermé\n");

    return 0;
}
```

### Lecture et écriture dans les fichiers (fprintf, fscanf, fread, fwrite)

*   `fprintf()`: Écrit des données formatées dans un fichier. Similaire à `printf`.
*   `fscanf()`: Lit des données formatées depuis un fichier. Similaire à `scanf`.
*   `fread()`: Lit un bloc de données depuis un fichier.
*   `fwrite()`: Écrit un bloc de données dans un fichier.

```c
#include <stdio.h>

int main() {
    FILE *fp;
    int num = 123;
    char str[] = "Hello, file!";

    // Ouverture en écriture
    fp = fopen("my_file.txt", "w");
    if (fp == NULL) {
        printf("Erreur lors de l'ouverture du fichier\n");
        return 1;
    }

    // Écriture formatée
    fprintf(fp, "Nombre: %d\n", num);
    fprintf(fp, "Chaîne: %s\n", str);
    fclose(fp);

    // Ouverture en lecture
    fp = fopen("my_file.txt", "r");
    if (fp == NULL) {
        printf("Erreur lors de l'ouverture du fichier\n");
        return 1;
    }

    int read_num;
    char read_str[50];
    fscanf(fp, "Nombre: %d\n", &read_num);
    fscanf(fp, "Chaîne: %s\n", read_str);
    fclose(fp);

    printf("Lu depuis le fichier: Nombre = %d, Chaîne = %s\n", read_num, read_str);

    return 0;
}
```

## 7. Préprocesseur C

### Directives (include, define, ifdef, etc.)

*   Le préprocesseur est une partie du compilateur qui traite le code source avant la compilation proprement dite.
*   Les directives commencent par `#`.
*   `#include`: Inclut le contenu d'un fichier d'en-tête.
*   `#define`: Définit une macro.
*   `#ifdef`, `#ifndef`, `#endif`: Compilation conditionnelle.

```c
#include <stdio.h> // Inclut la bibliothèque standard d'entrée/sortie
#define PI 3.14159 // Définit une macro pour PI

#ifdef DEBUG
    #define DEBUG_PRINT(x) printf("DEBUG: %s = %d\n", #x, x)
#else
    #define DEBUG_PRINT(x)
#endif

int main() {
    printf("PI = %f\n", PI);
    int value = 10;
    DEBUG_PRINT(value); // Ne sera affiché que si DEBUG est défini
    return 0;
}
```

### Macros

*   Substitutions de texte effectuées par le préprocesseur.
*   Peuvent être utilisées pour définir des constantes, des fonctions inline, etc.
*   Attention aux effets de bord et à la lisibilité.

```c
#include <stdio.h>

#define SQUARE(x) ((x) * (x)) // Macro pour calculer le carré

int main() {
    int num = 5;
    int result = SQUARE(num); // result = ((num) * (num)) = 25
    printf("SQUARE(%d) = %d\n", num, result);

    // Attention aux effets de bord
    int i = 5;
    printf("SQUARE(i++) = %d\n", SQUARE(i++)); // ((i++) * (i++)) -> i est incrémenté deux fois!
    printf("i = %d\n", i); // i = 7
    return 0;
}
```

## 8. Gestion de la Mémoire

### Pile (Stack) et Tas (Heap)

*   **Pile (Stack)**: Zone de mémoire utilisée pour stocker les variables locales, les arguments de fonction et les adresses de retour. Gérée automatiquement par le compilateur. Taille limitée.
*   **Tas (Heap)**: Zone de mémoire utilisée pour l'allocation dynamique. Gérée manuellement par le programmeur (avec `malloc`, `calloc`, `realloc`, `free`).

### Allocation statique et dynamique

*   **Allocation statique**: Mémoire allouée au moment de la compilation (variables globales, locales). Taille fixe.
*   **Allocation dynamique**: Mémoire allouée à l'exécution (avec `malloc`, `calloc`, `realloc`). Taille peut être déterminée à l'exécution.

### Problèmes courants (fuites de mémoire, pointeurs pendants)

*   **Fuites de mémoire**: Mémoire allouée dynamiquement qui n'est pas libérée avec `free`.
*   **Pointeurs pendants**: Pointeur qui pointe vers une zone de mémoire qui a déjà été libérée.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = (int*)malloc(sizeof(int));

    // ... utiliser ptr ...

    // Oublier de libérer la mémoire -> fuite de mémoire
    // free(ptr);

    ptr = NULL; // Pour éviter de créer un pointeur pendant

    return 0;
}
```

## 9. Bibliothèque Standard C

### Principales bibliothèques (stdio.h, stdlib.h, string.h, math.h)

*   `stdio.h`: Fonctions d'entrée/sortie standard (ex: `printf`, `scanf`, `fopen`, `fclose`).
*   `stdlib.h`: Fonctions utilitaires (ex: `malloc`, `calloc`, `free`, `atoi`, `exit`).
*   `string.h`: Fonctions de manipulation de chaînes de caractères (ex: `strcpy`, `strlen`, `strcmp`).
*   `math.h`: Fonctions mathématiques (ex: `sqrt`, `sin`, `cos`, `pow`).

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

int main() {
    printf("sqrt(25) = %f\n", sqrt(25)); // math.h
    char str[20] = "Hello";
    printf("strlen(\"%s\") = %zu\n", str, strlen(str)); // string.h
    int num = atoi("123"); // stdlib.h
    printf("atoi(\"123\") = %d\n", num);
    return 0;
}
```

## 9. Bibliothèque Standard C

### Principales bibliothèques (stdio.h, stdlib.h, string.h, math.h)

*   `stdio.h`: Fonctions d'entrée/sortie standard (ex: `printf`, `scanf`, `fopen`, `fclose`).
*   `stdlib.h`: Fonctions utilitaires (ex: `malloc`, `calloc`, `free`, `atoi`, `exit`).
*   `string.h`: Fonctions de manipulation de chaînes de caractères (ex: `strcpy`, `strlen`, `strcmp`).
*   `math.h`: Fonctions mathématiques (ex: `sqrt`, `sin`, `cos`, `pow`).

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

int main() {
    printf("sqrt(25) = %f\n", sqrt(25)); // math.h
    char str[20] = "Hello";
    printf("strlen(\"%s\") = %zu\n", str, strlen(str)); // string.h
    int num = atoi("123"); // stdlib.h
    printf("atoi(\"123\") = %d\n", num);
    return 0;
}
```

## 8. Gestion de la Mémoire

### Pile (Stack) et Tas (Heap)

*   **Pile (Stack)**: Zone de mémoire utilisée pour stocker les variables locales, les arguments de fonction et les adresses de retour. Gérée automatiquement par le compilateur. Taille limitée.
*   **Tas (Heap)**: Zone de mémoire utilisée pour l'allocation dynamique. Gérée manuellement par le programmeur (avec `malloc`, `calloc`, `realloc`, `free`).

### Allocation statique et dynamique

*   **Allocation statique**: Mémoire allouée au moment de la compilation (variables globales, locales). Taille fixe.
*   **Allocation dynamique**: Mémoire allouée à l'exécution (avec `malloc`, `calloc`, `realloc`). Taille peut être déterminée à l'exécution.

### Problèmes courants (fuites de mémoire, pointeurs pendants)

*   **Fuites de mémoire**: Mémoire allouée dynamiquement qui n'est pas libérée avec `free`.
*   **Pointeurs pendants**: Pointeur qui pointe vers une zone de mémoire qui a déjà été libérée.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = (int*)malloc(sizeof(int));

    // ... utiliser ptr ...

    // Oublier de libérer la mémoire -> fuite de mémoire
    // free(ptr);

    ptr = NULL; // Pour éviter de créer un pointeur pendant

    return 0;
}
```

## 9. Bibliothèque Standard C

### Principales bibliothèques (stdio.h, stdlib.h, string.h, math.h)

*   `stdio.h`: Fonctions d'entrée/sortie standard (ex: `printf`, `scanf`, `fopen`, `fclose`).
*   `stdlib.h`: Fonctions utilitaires (ex: `malloc`, `calloc`, `free`, `atoi`, `exit`).
*   `string.h`: Fonctions de manipulation de chaînes de caractères (ex: `strcpy`, `strlen`, `strcmp`).
*   `math.h`: Fonctions mathématiques (ex: `sqrt`, `sin`, `cos`, `pow`).

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

int main() {
    printf("sqrt(25) = %f\n", sqrt(25)); // math.h
    char str[20] = "Hello";
    printf("strlen(\"%s\") = %zu\n", str, strlen(str)); // string.h
    int num = atoi("123"); // stdlib.h
    printf("atoi(\"123\") = %d\n", num);
    return 0;
}
```
## 10. Compilation et Débogage

### Utilisation de GCC

*   GCC (GNU Compiler Collection) est un compilateur largement utilisé pour le C.
*   Commande de base pour compiler : `gcc nom_fichier.c -o nom_executable`

```bash
# Compiler un fichier C
gcc main.c -o main
```

### Options de compilation

*   `-Wall`: Affiche tous les avertissements.
*   `-Werror`: Traite les avertissements comme des erreurs.
*   `-g`: Ajoute des informations de débogage pour GDB.
*   `-O0`, `-O1`, `-O2`, `-O3`: Niveaux d'optimisation (de aucun à maximal).

```bash
# Compiler avec avertissements et informations de débogage
gcc -Wall -g main.c -o main
```

### Débogage avec GDB

*   GDB (GNU Debugger) est un débogueur en ligne de commande.
*   Permet d'exécuter le programme pas à pas, d'inspecter les variables, de définir des points d'arrêt, etc.

```bash
# Démarrer GDB
gdb main

# Commandes GDB courantes
# break main  (point d'arrêt dans la fonction main)
# run         (démarrer l'exécution)
# next        (passer à la ligne suivante)
# print var   (afficher la valeur de la variable var)
# continue    (continuer l'exécution)
# quit        (quitter GDB)
```

## 11. Bonnes Pratiques

### Conventions de codage

*   Utiliser des noms de variables et de fonctions clairs et descriptifs.
*   Indenter correctement le code.
*   Ajouter des commentaires pour expliquer le code complexe.
*   Éviter les variables globales autant que possible.
*   Utiliser des fonctions pour diviser le code en modules réutilisables.

### Gestion des erreurs

*   Vérifier les valeurs de retour des fonctions (ex: `malloc`, `fopen`).
*   Utiliser des codes de retour pour indiquer les erreurs.
*   Afficher des messages d'erreur clairs et informatifs.

## 12. Ressources et Communauté

### Documentation

*   [Documentation officielle du C](https://en.cppreference.com/w/c)
*   [Man pages](https://man7.org/linux/man-pages/)

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/C_Programming)](https://www.reddit.com/r/C_Programming/)

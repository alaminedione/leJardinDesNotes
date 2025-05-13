---
title: Java
draft: false
tags:
  - java
  - programming
description: Langage de programmation orienté objet, largement utilisé pour les applications d'entreprise, mobiles (Android) et web.
---

## Sommaire

1.  Introduction à Java
    *   Qu'est-ce que Java ?
    *   Historique et principes (WORA)
    *   Environnement d'exécution (JVM, JRE, JDK)
    *   Compilation et exécution
2.  Bases du Langage
    *   Syntaxe de base
    *   Variables et types de données (primitifs et objets)
    *   Opérateurs
    *   Structures de contrôle (conditions, boucles)
    *   Méthodes
3.  Programmation Orientée Objet (POO) en Java
    *   Classes et Objets
    *   Encapsulation, Héritage, Polymorphisme
    *   Interfaces et Classes Abstraites
    *   Packages
4.  Gestion des Exceptions
    *   Types d'exceptions (Checked, Unchecked)
    *   Blocs try-catch-finally
    *   Déclaration et levée d'exceptions
5.  Collections Framework
    *   Interfaces principales (List, Set, Map)
    *   Implémentations courantes (ArrayList, HashSet, HashMap)
    *   Itérateurs
6.  Entrées/Sorties (I/O)
    *   Flux (Streams)
    *   Lecture et écriture de fichiers
    *   Sérialisation
7.  Multithreading
    *   Création de threads
    *   Synchronisation
    *   États des threads
8.  Java Standard Library (API)
    *   Classes utiles (String, Math, Date)
    *   Utilisation de l'API
9.  Développement Web avec Java
    *   Servlets et JSP
    *   Frameworks (Spring, Jakarta EE)
10. Développement Mobile avec Android
    *   Introduction à Android
    *   Composants d'application
    *   Gestion de l'interface utilisateur
11. Tests en Java
    *   JUnit, Mockito
12. Bonnes Pratiques et Patterns
    *   Conventions de codage
    *   Patterns de conception courants
13. Ressources et Communauté
    *   Documentation officielle
    *   Communautés en ligne
## 1. Introduction à Java

### Qu'est-ce que Java ?

Java est un langage de programmation orienté objet, de haut niveau, largement utilisé pour les applications d'entreprise, mobiles (Android) et web. Il est connu pour sa portabilité, sa sécurité et sa robustesse.

### Historique et principes (WORA)

*   Développé par James Gosling chez Sun Microsystems (acquise par Oracle).
*   Première version en 1995.
*   Principe "Write Once, Run Anywhere" (WORA) : Le code Java peut être exécuté sur n'importe quelle plateforme disposant d'une JVM.

### Environnement d'exécution (JVM, JRE, JDK)

*   **JVM (Java Virtual Machine)** : Machine virtuelle Java, responsable de l'exécution du bytecode Java.
*   **JRE (Java Runtime Environment)** : Environnement d'exécution Java, contient la JVM et les bibliothèques nécessaires pour exécuter les programmes Java.
*   **JDK (Java Development Kit)** : Kit de développement Java, contient le JRE et les outils nécessaires pour développer des applications Java (compilateur, débogueur, etc.).

### Compilation et exécution

1.  Écrire le code source Java (`.java`).
2.  Compiler le code source en bytecode (`.class`) avec le compilateur `javac`.
3.  Exécuter le bytecode avec la commande `java`.

```bash
# Compilation
javac MonProgramme.java

# Exécution
java MonProgramme
```

## 2. Bases du Langage

### Syntaxe de base

*   Orienté objet : Tout est objet en Java (sauf les types primitifs).
*   Syntaxe similaire à C++ et C#.
*   Utilisation de classes et de méthodes.

```java
public class MonProgramme {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Variables et types de données (primitifs et objets)

*   Types primitifs : `int`, `float`, `double`, `boolean`, `char`, `byte`, `short`, `long`.
*   Objets : Instances de classes (ex: `String`, `Integer`, `ArrayList`).

```java
int age = 30;
String nom = "John";
double salaire = 50000.0;
boolean estValide = true;
```

### Opérateurs

*   Arithmétiques : `+`, `-`, `*`, `/`, `%`
*   Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
*   Logiques : `&&`, `||`, `!`
*   Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
*   Incrémentation/Décrémentation : `++`, `--`

```java
int x = 10;
int y = 5;
int sum = x + y;
boolean isEqual = (x == y);
boolean condition = (x > 0 && y < 10);
x++;
```

### Structures de contrôle (conditions, boucles)

*   `if`, `else if`, `else` : Conditionnelles
*   `for`, `while`, `do-while` : Boucles
*   `switch` : Sélection multiple

```java
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

switch (score) {
    case 100:
        // ...
        break;
    default:
        // ...
}
```

### Méthodes

*   Blocs de code réutilisables.
*   Déclaration : `type_retour nom_methode(paramètres) { // corps }`

```java
public static int add(int a, int b) {
    return a + b;
}

public static void main(String[] args) {
    int result = add(5, 3);
    System.out.println(result);
}
```
## 3. Programmation Orientée Objet (POO) en Java

### Classes et Objets

*   Une classe est un modèle ou un plan pour créer des objets.
*   Un objet est une instance d'une classe.

```java
class Voiture {
    String marque;
    String modele;

    public Voiture(String marque, String modele) {
        this.marque = marque;
        this.modele = modele;
    }
}

Voiture maVoiture = new Voiture("Renault", "Clio");
```

### Encapsulation, Héritage, Polymorphisme

*   **Encapsulation** : Regrouper les données (attributs) et les méthodes qui les manipulent au sein d'une classe.
*   **Héritage** : Permettre à une classe (sous-classe) d'hériter des attributs et des méthodes d'une autre classe (super-classe).
*   **Polymorphisme** : Permettre à un objet de prendre plusieurs formes (ex: surcharge de méthodes, interfaces).

```java
// Encapsulation
class Personne {
    private String nom;

    public String getNom() {
        return nom;
    }

    public void setNom(String nom) {
        this.nom = nom;
    }
}

// Héritage
class Etudiant extends Personne {
    private String numeroEtudiant;
}

// Polymorphisme
class Forme {
    public double calculerAire() {
        return 0;
    }
}

class Cercle extends Forme {
    private double rayon;

    @Override
    public double calculerAire() {
        return Math.PI * rayon * rayon;
    }
}
```

### Interfaces et Classes Abstraites

*   **Interface** : Contrat définissant un ensemble de méthodes qu'une classe doit implémenter.
*   **Classe Abstraite** : Classe qui ne peut pas être instanciée directement et qui peut contenir des méthodes abstraites (sans implémentation).

```java
// Interface
interface Animal {
    void faireDuBruit();
}

// Classe Abstraite
abstract class Forme {
    public abstract double calculerAire();
}
```

### Packages

*   Permettent d'organiser les classes en groupes logiques.
*   Utilisation du mot-clé `package` pour définir le package.
*   Utilisation du mot-clé `import` pour importer des classes d'autres packages.

```java
package com.example.monprogramme;

public class MaClasse {
    // ...
}
```

```java
import com.example.monprogramme.MaClasse;

public class Main {
    public static void main(String[] args) {
        MaClasse obj = new MaClasse();
    }
}
```
## 4. Gestion des Exceptions

### Types d'exceptions (Checked, Unchecked)

*   **Checked Exceptions** : Exceptions qui doivent être gérées explicitement dans le code (ex: `IOException`).  Le compilateur vérifie si elles sont gérées.
*   **Unchecked Exceptions** : Exceptions qui ne sont pas obligées d'être gérées explicitement (ex: `NullPointerException`, `ArrayIndexOutOfBoundsException`).  Elles se produisent généralement à l'exécution.

### Blocs try-catch-finally

*   `try` : Contient le code qui peut potentiellement lever une exception.
*   `catch` : Contient le code qui gère l'exception.
*   `finally` : Contient le code qui est exécuté que l'exception soit levée ou non (ex: fermeture de ressources).

```java
try {
    // Code qui peut lever une exception
    FileInputStream file = new FileInputStream("monfichier.txt");
} catch (FileNotFoundException e) {
    // Gestion de l'exception
    System.out.println("Fichier non trouvé: " + e.getMessage());
} finally {
    // Code exécuté dans tous les cas
    System.out.println("Fin du bloc try-catch");
}
```

### Déclaration et levée d'exceptions

*   Utilisation du mot-clé `throws` dans la signature d'une méthode pour déclarer qu'elle peut lever une exception.
*   Utilisation du mot-clé `throw` pour lever une exception.

```java
public static void maMethode() throws IOException {
    // ...
    throw new IOException("Erreur d'entrée/sortie");
}
```
## 5. Collections Framework

### Interfaces principales (List, Set, Map)

*   **List** : Collection ordonnée d'éléments (permet les doublons).
*   **Set** : Collection non ordonnée d'éléments uniques (ne permet pas les doublons).
*   **Map** : Collection de paires clé-valeur (chaque clé est unique).

### Implémentations courantes (ArrayList, HashSet, HashMap)

*   `ArrayList` : Implémentation de l'interface `List` basée sur un tableau redimensionnable.
*   `HashSet` : Implémentation de l'interface `Set` basée sur une table de hachage.
*   `HashMap` : Implémentation de l'interface `Map` basée sur une table de hachage.

```java
List<String> liste = new ArrayList<>();
liste.add("Element 1");
liste.add("Element 2");

Set<String> ensemble = new HashSet<>();
ensemble.add("Element 1");
ensemble.add("Element 2");

Map<String, Integer> map = new HashMap<>();
map.put("Alice", 30);
map.put("Bob", 25);
```

### Itérateurs

*   Permettent de parcourir les éléments d'une collection.

```java
List<String> liste = new ArrayList<>();
liste.add("Element 1");
liste.add("Element 2");

Iterator<String> iterator = liste.iterator();
while (iterator.hasNext()) {
    String element = iterator.next();
    System.out.println(element);
}
```
## 6. Entrées/Sorties (I/O)

### Flux (Streams)

*   Les flux (streams) sont utilisés pour lire et écrire des données.
*   Flux d'entrée (InputStream) : Utilisés pour lire des données.
*   Flux de sortie (OutputStream) : Utilisés pour écrire des données.

### Lecture et écriture de fichiers

*   Utilisation des classes `FileInputStream`, `FileOutputStream`, `BufferedReader`, `BufferedWriter`.

```java
import java.io.*;

public class Main {
    public static void main(String[] args) {
        try {
            // Écriture dans un fichier
            BufferedWriter writer = new BufferedWriter(new FileWriter("monfichier.txt"));
            writer.write("Hello, fichier!");
            writer.close();

            // Lecture depuis un fichier
            BufferedReader reader = new BufferedReader(new FileReader("monfichier.txt"));
            String line = reader.readLine();
            System.out.println(line);
            reader.close();
        } catch (IOException e) {
            System.out.println("Erreur d'entrée/sortie: " + e.getMessage());
        }
    }
}
```

### Sérialisation

*   Permet de convertir un objet en une séquence d'octets pour le stocker dans un fichier ou le transmettre sur le réseau.
*   Utilisation des interfaces `Serializable`, `ObjectInputStream`, `ObjectOutputStream`.
## 7. Multithreading

### Création de threads

*   Deux façons de créer des threads :
    *   Implémenter l'interface `Runnable`.
    *   Hériter de la classe `Thread`.

```java
// Implémentation de Runnable
class MonThread implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread en cours d'exécution");
    }
}

Thread thread = new Thread(new MonThread());
thread.start();

// Héritage de Thread
class MonThread2 extends Thread {
    @Override
    public void run() {
        System.out.println("Thread en cours d'exécution");
    }
}

MonThread2 thread2 = new MonThread2();
thread2.start();
```

### Synchronisation

*   Permet de contrôler l'accès concurrent à une ressource partagée.
*   Utilisation du mot-clé `synchronized`.

```java
public synchronized void incrementerCompteur() {
    compteur++;
}
```

### États des threads

*   New (Nouveau)
*   Runnable (Prêt à être exécuté)
*   Running (En cours d'exécution)
*   Blocked (Bloqué)
*   Waiting (En attente)
*   Timed Waiting (En attente temporaire)
*   Terminated (Terminé)
## 8. Java Standard Library (API)

### Classes utiles (String, Math, Date)

*   `String` : Classe pour manipuler les chaînes de caractères.
*   `Math` : Classe contenant des méthodes mathématiques (ex: `sqrt`, `sin`, `cos`).
*   `Date` : Classe pour représenter les dates et les heures.

### Utilisation de l'API

```java
String message = "Hello, World!";
System.out.println(message.length()); // Longueur de la chaîne

double racine = Math.sqrt(25); // Racine carrée de 25

Date date = new Date();
System.out.println(date); // Date et heure actuelles
```
## 9. Développement Web avec Java

### Servlets et JSP

*   **Servlets** : Composants Java utilisés pour créer des applications web dynamiques.
*   **JSP (JavaServer Pages)** : Technologie permettant de créer des pages web dynamiques en intégrant du code Java dans du code HTML.

### Frameworks (Spring, Jakarta EE)

*   **Spring** : Framework open-source pour le développement d'applications Java d'entreprise.
*   **Jakarta EE (anciennement Java EE)** : Ensemble de spécifications pour le développement d'applications Java d'entreprise.
## 10. Développement Mobile avec Android

### Introduction à Android

*   Android est un système d'exploitation mobile basé sur le noyau Linux et développé par Google.
*   Java (et Kotlin) sont les langages de programmation principaux pour le développement d'applications Android.

### Composants d'application

*   **Activités (Activities)** : Écrans de l'application.
*   **Services (Services)** : Composants exécutés en arrière-plan.
*   **Fournisseurs de contenu (Content Providers)** : Composants permettant de partager des données entre les applications.
*   **Récepteurs de diffusion (Broadcast Receivers)** : Composants réagissant aux événements du système.

### Gestion de l'interface utilisateur

*   Utilisation de XML pour définir l'interface utilisateur.
*   Utilisation de Java pour gérer la logique de l'interface utilisateur.
## 11. Tests en Java

### JUnit, Mockito

*   **JUnit** : Framework de test unitaire pour Java.
*   **Mockito** : Framework de mocking pour Java (permet de créer des objets factices pour isoler le code testé).
## 12. Bonnes Pratiques et Patterns

### Conventions de codage

*   Suivre les conventions de codage Java (ex: [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)).
*   Utiliser des noms clairs et descriptifs.
*   Écrire du code lisible et maintenable.

### Patterns de conception courants

*   Singleton
*   Factory
*   Observer
*   Strategy
## 13. Ressources et Communauté

### Documentation officielle

*   [Oracle Java Documentation](https://docs.oracle.com/en/java/)

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/java)](https://www.reddit.com/r/java/)

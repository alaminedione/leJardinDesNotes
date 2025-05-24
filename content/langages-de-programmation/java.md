---
title: Java
draft: false
tags:
  - java
  - programming
description: Langage de programmation orienté objet, largement utilisé pour les applications d'entreprise, mobiles (Android) et web.
---

# Java

## Sommaire

1. Introduction à Java
    * Qu'est-ce que Java ?
    * Historique et principes (WORA)
    * Environnement d'exécution (JVM, JRE, JDK)
    * Compilation et exécution
    * Écosystème Java et cas d'utilisation
2. Bases du Langage
    * Syntaxe de base
    * Variables et types de données (primitifs et objets)
    * Opérateurs
    * Structures de contrôle (conditions, boucles)
    * Méthodes
    * Tableaux
3. Programmation Orientée Objet (POO) en Java
    * Classes et Objets
    * Encapsulation, Héritage, Polymorphisme
    * Interfaces et Classes Abstraites
    * Packages
    * Constructeurs et `this`
4. Gestion des Exceptions
    * Types d'exceptions (Checked, Unchecked)
    * Blocs try-catch-finally
    * Déclaration et levée d'exceptions
    * `try-with-resources`
5. Collections Framework
    * Interfaces principales (List, Set, Map)
    * Implémentations courantes (ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap)
    * Itérateurs
    * Génériques et Collections
6. Entrées/Sorties (I/O)
    * Flux (Streams)
    * Lecture et écriture de fichiers
    * Sérialisation
    * NIO.2 (New I/O)
7. Multithreading
    * Création de threads
    * Synchronisation
    * États des threads
    * `Executors`, `Callable`, `Future` et `Locks`
8. Java Standard Library (API)
    * Classes utiles (String, Math, Date, LocalDate, LocalDateTime, Scanner, Random)
    * Utilisation de l'API
9. Développement Web avec Java
    * Servlets et JSP
    * Frameworks (Spring, Jakarta EE, Hibernate, JSF)
10. Développement Mobile avec Android
    * Introduction à Android
    * Composants d'application
    * Gestion de l'interface utilisateur
11. Tests en Java
    * JUnit, Mockito
    * Tests d'intégration et de performance
    * Outils de couverture de code
12. Bonnes Pratiques et Patterns
    * Conventions de codage
    * Patterns de conception courants (Singleton, Factory, Observer, Strategy, Builder, Adapter)
    * Principes SOLID
13. Génériques
    * Introduction aux génériques
    * Avantages et cas d'utilisation
    * Wildcards
14. Expressions Lambda et Streams API
    * Introduction aux expressions Lambda
    * Streams API (filtrage, mapping, réduction)
    * Méthodes de référence
15. JDBC (Java Database Connectivity)
    * Connexion à une base de données
    * Exécution de requêtes SQL
    * Gestion des résultats
16. Build Tools (Maven/Gradle)
    * Introduction à Maven
    * Introduction à Gradle
    * Gestion des dépendances et compilation
17. Logging
    * Introduction au logging
    * Frameworks de logging (Log4j, SLF4j, Logback)
    * Niveaux de log
18. Ressources et Communauté
    * Documentation officielle
    * Communautés en ligne
    * Livres et cours

## 1. Introduction à Java

### Qu'est-ce Que Java ?

Java est un langage de programmation orienté objet, de haut niveau, largement utilisé pour les applications d'entreprise, mobiles (Android) et web. Il est connu pour sa portabilité, sa sécurité et sa robustesse.

### Historique Et Principes (WORA)

* Développé par James Gosling chez Sun Microsystems (acquise par Oracle).
* Première version en 1995.
* Principe "Write Once, Run Anywhere" (WORA) : Le code Java peut être exécuté sur n'importe quelle plateforme disposant d'une JVM.

### Environnement D'exécution (JVM, JRE, JDK)

* **JVM (Java Virtual Machine)** : Machine virtuelle Java, responsable de l'exécution du bytecode Java.
* **JRE (Java Runtime Environment)** : Environnement d'exécution Java, contient la JVM et les bibliothèques nécessaires pour exécuter les programmes Java.
* **JDK (Java Development Kit)** : Kit de développement Java, contient le JRE et les outils nécessaires pour développer des applications Java (compilateur, débogueur, etc.).

### Compilation Et Exécution

1. Écrire le code source Java (`.java`).
2. Compiler le code source en bytecode (`.class`) avec le compilateur `javac`.
3. Exécuter le bytecode avec la commande `java`.

```bash
# Compilation
javac MonProgramme.java

# Exécution
java MonProgramme
```

### Écosystème Java Et Cas D'utilisation

* **Applications d'entreprise** : Java est le pilier des applications d'entreprise robustes et évolutives, souvent avec des frameworks comme Spring et Jakarta EE.
* **Développement Android** : Le langage principal pour la création d'applications mobiles natives sur Android.
* **Big Data** : Des technologies comme Apache Hadoop et Apache Spark sont écrites en Java (ou Scala, qui tourne sur la JVM).
* **Applications Web** : Bien que d'autres langages soient populaires, Java reste un choix solide pour le backend web.
* **Outils et Utilitaires** : De nombreux outils de développement (ex: Eclipse, IntelliJ IDEA) sont écrits en Java.
* **Internet des Objets (IoT)** : Java ME (Micro Edition) est utilisé pour les appareils embarqués.

## 2. Bases Du Langage

### Syntaxe De Base

* Orienté objet : Tout est objet en Java (sauf les types primitifs).
* Syntaxe similaire à C++ et C#.
* Utilisation de classes et de méthodes.

```java
public class MonProgramme {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Variables Et Types De Données (primitifs Et objets)

* Types primitifs : `int`, `float`, `double`, `boolean`, `char`, `byte`, `short`, `long`.
* Objets : Instances de classes (ex: `String`, `Integer`, `ArrayList`).

```java
int age = 30;
String nom = "John";
double salaire = 50000.0;
boolean estValide = true;
```

### Opérateurs

* Arithmétiques : `+`, `-`, `*`, `/`, `%`
* Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
* Logiques : `&&`, `||`, `!`
* Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
* Incrémentation/Décrémentation : `++`, `--`

```java
int x = 10;
int y = 5;
int sum = x + y;
boolean isEqual = (x == y);
boolean condition = (x > 0 && y < 10);
x++;
```

### Structures De Contrôle (conditions, boucles)

* `if`, `else if`, `else` : Conditionnelles
* `for`, `while`, `do-while` : Boucles
* `switch` : Sélection multiple

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

* Blocs de code réutilisables.
* Déclaration : `type_retour nom_methode(paramètres) { // corps }`

```java
public static int add(int a, int b) {
    return a + b;
}

public static void main(String[] args) {
    int result = add(5, 3);
    System.out.println(result);
}
```

### Tableaux

* Les tableaux sont des conteneurs d'objets de même type.
* Déclaration : `type[] nomTableau;` ou `type nomTableau[];`
* Initialisation : `nomTableau = new type[taille];` ou `type[] nomTableau = {val1, val2, …};`

```java
int[] nombres = new int[5]; // Déclare un tableau de 5 entiers
nombres[0] = 10;
nombres[1] = 20;

String[] noms = {"Alice", "Bob", "Charlie"}; // Déclare et initialise un tableau de chaînes
System.out.println(noms[0]); // Affiche "Alice"

// Parcourir un tableau
for (int i = 0; i < nombres.length; i++) {
    System.out.println(nombres[i]);
}

// Boucle for-each
for (String nom : noms) {
    System.out.println(nom);
}
```

## 3. Programmation Orientée Objet (POO) En Java

### Classes Et Objets

* Une classe est un modèle ou un plan pour créer des objets.
* Un objet est une instance d'une classe.

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

* **Encapsulation** : Regrouper les données (attributs) et les méthodes qui les manipulent au sein d'une classe.
* **Héritage** : Permettre à une classe (sous-classe) d'hériter des attributs et des méthodes d'une autre classe (super-classe).
* **Polymorphisme** : Permettre à un objet de prendre plusieurs formes (ex: surcharge de méthodes, interfaces).

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

### Interfaces Et Classes Abstraites

* **Interface** : Contrat définissant un ensemble de méthodes qu'une classe doit implémenter.
* **Classe Abstraite** : Classe qui ne peut pas être instanciée directement et qui peut contenir des méthodes abstraites (sans implémentation).

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

* Permettent d'organiser les classes en groupes logiques.
* Utilisation du mot-clé `package` pour définir le package.
* Utilisation du mot-clé `import` pour importer des classes d'autres packages.

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

### Constructeurs Et `this`

* **Constructeur** : Méthode spéciale utilisée pour initialiser les objets d'une classe. Il a le même nom que la classe et n'a pas de type de retour.
* **`this`** : Mot-clé de référence qui fait référence à l'objet courant. Il est souvent utilisé pour distinguer les attributs de classe des paramètres de méthode ayant le même nom.

```java
class Produit {
    String nom;
    double prix;

    // Constructeur par défaut
    public Produit() {
        this.nom = "Inconnu";
        this.prix = 0.0;
    }

    // Constructeur avec paramètres
    public Produit(String nom, double prix) {
        this.nom = nom; // 'this.nom' fait référence à l'attribut de la classe
        this.prix = prix;
    }

    public void afficherDetails() {
        System.out.println("Produit: " + this.nom + ", Prix: " + this.prix + "€");
    }
}

public class TestProduit {
    public static void main(String[] args) {
        Produit p1 = new Produit(); // Utilise le constructeur par défaut
        p1.afficherDetails(); // Affiche "Produit: Inconnu, Prix: 0.0€"

        Produit p2 = new Produit("Ordinateur", 1200.0); // Utilise le constructeur avec paramètres
        p2.afficherDetails(); // Affiche "Produit: Ordinateur, Prix: 1200.0€"
    }
}
```

## 4. Gestion Des Exceptions

### Types D'exceptions (Checked, Unchecked)

* **Checked Exceptions** : Exceptions qui doivent être gérées explicitement dans le code (ex: `IOException`). Le compilateur vérifie si elles sont gérées.
* **Unchecked Exceptions** : Exceptions qui ne sont pas obligées d'être gérées explicitement (ex: `NullPointerException`, `ArrayIndexOutOfBoundsException`). Elles se produisent généralement à l'exécution.

### Blocs Try-catch-finally

* `try` : Contient le code qui peut potentiellement lever une exception.
* `catch` : Contient le code qui gère l'exception.
* `finally` : Contient le code qui est exécuté que l'exception soit levée ou non (ex: fermeture de ressources).

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

### Déclaration Et Levée D'exceptions

* Utilisation du mot-clé `throws` dans la signature d'une méthode pour déclarer qu'elle peut lever une exception.
* Utilisation du mot-clé `throw` pour lever une exception.

```java
public static void maMethode() throws IOException {
    // ...
    throw new IOException("Erreur d'entrée/sortie");
}
```

### `try-with-resources`

* Introduit en Java 7, le bloc `try-with-resources` assure que les ressources qui implémentent l'interface `AutoCloseable` sont automatiquement fermées à la fin du bloc `try`, qu'une exception soit levée ou non. Cela simplifie la gestion des ressources et réduit les risques de fuites de ressources.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadFileExample {
    public static void main(String[] args) {
        // Le BufferedReader sera automatiquement fermé à la fin du bloc try
        try (BufferedReader reader = new BufferedReader(new FileReader("monfichier.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier : " + e.getMessage());
        }
    }
}
```

## 5. Collections Framework

### Interfaces Principales (List, Set, Map)

* **List** : Collection ordonnée d'éléments (permet les doublons).
* **Set** : Collection non ordonnée d'éléments uniques (ne permet pas les doublons).
* **Map** : Collection de paires clé-valeur (chaque clé est unique).

### Implémentations Courantes (ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap)

* `ArrayList` : Implémentation de l'interface `List` basée sur un tableau redimensionnable. Bonne performance pour l'accès aléatoire.
* `LinkedList` : Implémentation de l'interface `List` basée sur une liste doublement chaînée. Bonne performance pour les insertions et suppressions.
* `HashSet` : Implémentation de l'interface `Set` basée sur une table de hachage. N'assure aucun ordre.
* `TreeSet` : Implémentation de l'interface `Set` basée sur un arbre rouge-noir. Stocke les éléments dans un ordre trié.
* `HashMap` : Implémentation de l'interface `Map` basée sur une table de hachage. N'assure aucun ordre des clés.
* `TreeMap` : Implémentation de l'interface `Map` basée sur un arbre rouge-noir. Stocke les paires clé-valeur dans un ordre trié par clé.

```java
import java.util.*; // Importation pour toutes les classes de collections

List<String> arrayList = new ArrayList<>();
arrayList.add("Element 1");
arrayList.add("Element 2");

List<String> linkedList = new LinkedList<>();
linkedList.add("Element A");
linkedList.add("Element B");

Set<String> hashSet = new HashSet<>();
hashSet.add("Unique 1");
hashSet.add("Unique 2");

Set<String> treeSet = new TreeSet<>();
treeSet.add("Zebra");
treeSet.add("Apple");
treeSet.add("Banana"); // Les éléments seront triés alphabétiquement

Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("Alice", 30);
hashMap.put("Bob", 25);

Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Charlie", 40);
treeMap.put("David", 35); // Les clés seront triées alphabétiquement
```

### Itérateurs

* Permettent de parcourir les éléments d'une collection.

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

### Génériques Et Collections

* Les génériques permettent de créer des classes, interfaces et méthodes qui opèrent sur des types de données spécifiés comme paramètres. Cela permet de réutiliser le code et d'assurer la sécurité de type au moment de la compilation.
* Les collections en Java sont fortement typées grâce aux génériques, ce qui évite les erreurs de `ClassCastException` à l'exécution.

```java
// Exemple de List générique
List<String> noms = new ArrayList<>();
noms.add("Alice");
// noms.add(123); // Erreur de compilation si on essaie d'ajouter un entier

// Exemple de Map générique
Map<String, Integer> ages = new HashMap<>();
ages.put("Bob", 25);

// Méthode générique
public <T> void afficherElement(T element) {
    System.out.println("Élément : " + element);
}

// Utilisation de la méthode générique
afficherElement("Hello");
afficherElement(123);
```

## 6. Entrées/Sorties (I/O)

### Flux (Streams)

* Les flux (streams) sont utilisés pour lire et écrire des données.
* Flux d'entrée (InputStream) : Utilisés pour lire des données.
* Flux de sortie (OutputStream) : Utilisés pour écrire des données.

### Lecture Et Écriture De Fichiers

* Utilisation des classes `FileInputStream`, `FileOutputStream`, `BufferedReader`, `BufferedWriter`.

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

* Permet de convertir un objet en une séquence d'octets pour le stocker dans un fichier ou le transmettre sur le réseau.
* Utilisation des interfaces `Serializable`, `ObjectInputStream`, `ObjectOutputStream`.

### NIO.2 (New I/O)

* Introduit en Java 7, NIO.2 offre une API améliorée pour la manipulation des fichiers et des répertoires, ainsi que pour les opérations d'E/S asynchrones.
* Classes clés : `Path`, `Files`, `FileSystems`.

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

public class NIO2Example {
    public static void main(String[] args) {
        Path filePath = Paths.get("monfichier_nio2.txt");

        try {
            // Écrire dans un fichier
            String content = "Contenu écrit avec NIO.2";
            Files.write(filePath, content.getBytes());
            System.out.println("Fichier écrit avec succès.");

            // Lire un fichier
            List<String> lines = Files.readAllLines(filePath);
            System.out.println("Contenu du fichier :");
            for (String line : lines) {
                System.out.println(line);
            }

            // Vérifier si un fichier existe
            boolean exists = Files.exists(filePath);
            System.out.println("Le fichier existe : " + exists);

            // Supprimer un fichier
            Files.deleteIfExists(filePath);
            System.out.println("Fichier supprimé (si existant).");

        } catch (IOException e) {
            System.err.println("Erreur NIO.2 : " + e.getMessage());
        }
    }
}
```

## 7. Multithreading

### Création De Threads

* Deux façons de créer des threads :
    * Implémenter l'interface `Runnable`.
    * Hériter de la classe `Thread`.

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

* Permet de contrôler l'accès concurrent à une ressource partagée.
* Utilisation du mot-clé `synchronized`.

```java
public synchronized void incrementerCompteur() {
    compteur++;
}
```

### États Des Threads

* New (Nouveau)
* Runnable (Prêt à être exécuté)
* Running (En cours d'exécution)
* Blocked (Bloqué)
* Waiting (En attente)
* Timed Waiting (En attente temporaire)
* Terminated (Terminé)

### `Executors`, `Callable`, `Future` Et `Locks`

* **`Executors`** : Fournit des fabriques pour créer des pools de threads, simplifiant la gestion des threads.
* **`Callable`** : Interface similaire à `Runnable`, mais dont la méthode `call()` peut retourner un résultat et lever une exception.
* **`Future`** : Représente le résultat d'une exécution asynchrone. Permet de vérifier si la tâche est terminée, d'attendre sa complétion et d'obtenir son résultat.
* **`Locks`** : Offre des mécanismes de verrouillage plus flexibles et puissants que le mot-clé `synchronized`, comme `ReentrantLock`.

```java
import java.util.concurrent.*;
import java.util.concurrent.locks.ReentrantLock;

public class ConcurrencyExample {

    private static int count = 0;
    private static ReentrantLock lock = new ReentrantLock();

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        // Utilisation d'un ExecutorService avec Callable et Future
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Callable<Integer> task = () -> {
            int sum = 0;
            for (int i = 0; i < 100; i++) {
                sum += i;
            }
            return sum;
        };

        Future<Integer> future = executor.submit(task);
        System.out.println("Résultat de la tâche asynchrone : " + future.get()); // Bloque jusqu'à ce que le résultat soit disponible

        // Utilisation de ReentrantLock pour la synchronisation
        Runnable incrementTask = () -> {
            lock.lock(); // Acquiert le verrou
            try {
                for (int i = 0; i < 1000; i++) {
                    count++;
                }
            } finally {
                lock.unlock(); // Libère le verrou
            }
        };

        executor.submit(incrementTask);
        executor.submit(incrementTask);

        executor.shutdown(); // Arrête l'ExecutorService
        executor.awaitTermination(1, TimeUnit.MINUTES); // Attend la fin des tâches

        System.out.println("Compteur final (avec Lock) : " + count);
    }
}
```

## 8. Java Standard Library (API)

### Classes Utiles (String, Math, Date, LocalDate, LocalDateTime, Scanner, Random)

* `String` : Classe pour manipuler les chaînes de caractères. Immuable.
* `Math` : Classe utilitaire contenant des méthodes mathématiques statiques (ex: `sqrt`, `sin`, `cos`, `random`).
* `Date` : Classe pour représenter les dates et les heures (ancienne API, souvent remplacée par `java.time`).
* `LocalDate` : Représente une date sans heure ni fuseau horaire (partie de l'API `java.time` introduite en Java 8).
* `LocalDateTime` : Représente une date et une heure sans fuseau horaire (partie de l'API `java.time`).
* `Scanner` : Utilisé pour lire l'entrée de l'utilisateur (clavier) ou des fichiers.
* `Random` : Utilisé pour générer des nombres pseudo-aléatoires.

### Utilisation De l'API

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.util.Date;
import java.util.Random;
import java.util.Scanner;

public class APIExample {
    public static void main(String[] args) {
        // String
        String message = "Hello, World!";
        System.out.println("Longueur de la chaîne : " + message.length());
        System.out.println("Caractère à l'index 1 : " + message.charAt(1));
        System.out.println("Sous-chaîne : " + message.substring(7));

        // Math
        double racine = Math.sqrt(25);
        System.out.println("Racine carrée de 25 : " + racine);
        System.out.println("Nombre aléatoire entre 0.0 et 1.0 : " + Math.random());

        // Date (ancienne API)
        Date date = new Date();
        System.out.println("Date actuelle (ancienne API) : " + date);

        // LocalDate (nouvelle API de date/heure)
        LocalDate today = LocalDate.now();
        System.out.println("Date d'aujourd'hui : " + today);
        LocalDate specificDate = LocalDate.of(2023, 1, 15);
        System.out.println("Date spécifique : " + specificDate);

        // LocalDateTime (nouvelle API de date/heure)
        LocalDateTime now = LocalDateTime.now();
        System.out.println("Date et heure actuelles : " + now);

        // Scanner (pour l'entrée utilisateur)
        Scanner scanner = new Scanner(System.in);
        System.out.print("Entrez votre nom : ");
        // String nomUtilisateur = scanner.nextLine();
        // System.out.println("Bonjour, " + nomUtilisateur + "!");
        scanner.close(); // Toujours fermer le scanner

        // Random
        Random random = new Random();
        int randomNumber = random.nextInt(100); // Nombre aléatoire entre 0 (inclus) et 100 (exclus)
        System.out.println("Nombre aléatoire (0-99) : " + randomNumber);
    }
}
```

## 9. Développement Web Avec Java

### Servlets Et JSP

* **Servlets** : Composants Java utilisés pour créer des applications web dynamiques.
* **JSP (JavaServer Pages)** : Technologie permettant de créer des pages web dynamiques en intégrant du code Java dans du code HTML.

### Frameworks (Spring, Jakarta EE, Hibernate, JSF)

* **Spring** : Framework open-source très populaire pour le développement d'applications Java d'entreprise, offrant des modules pour la gestion des dépendances, la sécurité, l'accès aux données, etc.
* **Jakarta EE (anciennement Java EE)** : Ensemble de spécifications et d'APIs pour le développement d'applications d'entreprise distribuées et multi-tiers.
* **Hibernate** : Framework de mapping objet-relationnel (ORM) qui facilite l'interaction avec les bases de données en mappant les objets Java aux tables de la base de données.
* **JSF (JavaServer Faces)** : Framework basé sur des composants pour la construction d'interfaces utilisateur web.

## 10. Développement Mobile Avec Android

### Introduction à Android

* Android est un système d'exploitation mobile basé sur le noyau Linux et développé par Google.
* Java (et Kotlin) sont les langages de programmation principaux pour le développement d'applications Android.

### Composants D'application

* **Activités (Activities)** : Écrans de l'application.
* **Services (Services)** : Composants exécutés en arrière-plan.
* **Fournisseurs de contenu (Content Providers)** : Composants permettant de partager des données entre les applications.
* **Récepteurs de diffusion (Broadcast Receivers)** : Composants réagissant aux événements du système.

### Gestion De L'interface Utilisateur

* Utilisation de XML pour définir l'interface utilisateur.
* Utilisation de Java pour gérer la logique de l'interface utilisateur.

## 11. Tests En Java

### JUnit, Mockito

* **JUnit** : Framework de test unitaire très répandu pour Java. Permet d'écrire et d'exécuter des tests pour vérifier le comportement des unités de code.
* **Mockito** : Framework de mocking pour Java. Il est utilisé pour créer des objets "mocks" (simulacres) afin d'isoler le code testé des dépendances externes, facilitant ainsi les tests unitaires.

### Tests D'intégration Et De Performance

* **Tests d'intégration** : Vérifient que différents modules ou services d'une application fonctionnent correctement ensemble. Souvent réalisés avec des frameworks comme Spring Test ou des outils de conteneurisation (ex: Testcontainers).
* **Tests de performance** : Évaluent la réactivité, la stabilité, l'évolutivité et l'utilisation des ressources d'une application sous une charge de travail particulière. Outils courants : JMeter, Gatling.

### Outils De Couverture De Code

* Mesurent le pourcentage de code source exécuté par les tests.
* Outils populaires : JaCoCo, Cobertura.

## 12. Bonnes Pratiques Et Patterns

### Conventions De Codage

* Suivre les conventions de codage Java (ex: [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)).
* Utiliser des noms clairs et descriptifs.
* Écrire du code lisible et maintenable.

### Patterns De Conception Courants

* **Singleton** : Assure qu'une classe n'a qu'une seule instance et fournit un point d'accès global à cette instance.
* **Factory** : Fournit une interface pour créer des objets dans une super-classe, mais permet aux sous-classes de modifier le type d'objets qui seront créés.
* **Observer** : Définit une dépendance un-à-plusieurs entre objets, de sorte que lorsqu'un objet change d'état, tous ses dépendants sont avertis et mis à jour automatiquement.
* **Strategy** : Définit une famille d'algorithmes, encapsule chacun d'eux et les rend interchangeables. Permet à l'algorithme de varier indépendamment des clients qui l'utilisent.
* **Builder** : Sépare la construction d'un objet complexe de sa représentation, de sorte que le même processus de construction peut créer différentes représentations.
* **Adapter** : Permet à des interfaces incompatibles de travailler ensemble.

### Principes SOLID

* **S (Single Responsibility Principle)** : Une classe ne devrait avoir qu'une seule raison de changer.
* **O (Open/Closed Principle)** : Les entités logicielles (classes, modules, fonctions, etc.) doivent être ouvertes à l'extension, mais fermées à la modification.
* **L (Liskov Substitution Principle)** : Les objets d'un programme doivent pouvoir être remplacés par des instances de leurs sous-types sans altérer la justesse du programme.
* **I (Interface Segregation Principle)** : Les clients ne devraient pas être forcés de dépendre d'interfaces qu'ils n'utilisent pas.
* **D (Dependency Inversion Principle)** : Les modules de haut niveau ne devraient pas dépendre des modules de bas niveau. Les deux devraient dépendre d'abstractions. Les abstractions ne devraient pas dépendre des détails. Les détails devraient dépendre des abstractions.

## 13. Génériques

### Introduction Aux Génériques

* Les génériques permettent de créer des classes, interfaces et méthodes qui opèrent sur des types de données spécifiés comme paramètres. Cela permet de réutiliser le code et d'assurer la sécurité de type au moment de la compilation.

```java
// Exemple de classe générique
class Boite<T> {
    private T contenu;

    public Boite(T contenu) {
        this.contenu = contenu;
    }

    public T getContenu() {
        return contenu;
    }
}

// Utilisation
Boite<String> boiteDeTexte = new Boite<>("Bonjour");
String texte = boiteDeTexte.getContenu(); // Pas besoin de cast

Boite<Integer> boiteDeNombre = new Boite<>(123);
int nombre = boiteDeNombre.getContenu(); // Pas besoin de cast
```

### Avantages Et Cas D'utilisation

* **Sécurité de type au moment de la compilation** : Détecte les erreurs de type à la compilation plutôt qu'à l'exécution (`ClassCastException`).
* **Élimination des casts explicites** : Rend le code plus propre et plus lisible.
* **Réutilisation du code** : Permet d'écrire des algorithmes génériques qui fonctionnent avec différents types.
* **Collections typées** : Le Collections Framework de Java utilise intensivement les génériques (ex: `List<String>`, `Map<Integer, Double>`).

### Wildcards

* Les wildcards (`?`) sont utilisés dans les génériques pour représenter un type inconnu. Ils sont utiles pour la flexibilité des méthodes qui traitent des collections de types variés.
* **Wildcard supérieur (`? extends Type`)** : Indique que le type peut être `Type` ou n'importe quel sous-type de `Type`. Utilisé pour la lecture (producteur).
* **Wildcard inférieur (`? super Type`)** : Indique que le type peut être `Type` ou n'importe quel super-type de `Type`. Utilisé pour l'écriture (consommateur).

```java
import java.util.ArrayList;
import java.util.List;

public class WildcardExample {

    // Méthode qui accepte une liste de n'importe quel type qui étend Number
    public static void afficherNombres(List<? extends Number> liste) {
        for (Number n : liste) {
            System.out.println(n);
        }
    }

    // Méthode qui accepte une liste de n'importe quel type qui est un super-type de Integer
    public static void ajouterEntier(List<? super Integer> liste) {
        liste.add(10);
        liste.add(20);
    }

    public static void main(String[] args) {
        List<Integer> entiers = new ArrayList<>();
        entiers.add(1);
        entiers.add(2);
        afficherNombres(entiers); // Fonctionne

        List<Double> doubles = new ArrayList<>();
        doubles.add(1.1);
        doubles.add(2.2);
        afficherNombres(doubles); // Fonctionne

        List<Number> nombresGeneriques = new ArrayList<>();
        ajouterEntier(nombresGeneriques); // Fonctionne
        System.out.println("Nombres génériques après ajout : " + nombresGeneriques);

        List<Object> objets = new ArrayList<>();
        ajouterEntier(objets); // Fonctionne
        System.out.println("Objets après ajout : " + objets);
    }
}
```

## 14. Expressions Lambda Et Streams API

### Introduction Aux Expressions Lambda

* Introduites en Java 8, les expressions lambda fournissent un moyen concis de représenter une instance d'une interface fonctionnelle (une interface avec une seule méthode abstraite). Elles sont souvent utilisées pour écrire du code plus fonctionnel et plus lisible, notamment avec l'API Stream.

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;

public class LambdaExample {
    public static void main(String[] args) {
        // Ancien style (classe anonyme)
        Runnable oldRunnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("Ancien Runnable");
            }
        };
        new Thread(oldRunnable).start();

        // Nouveau style (expression lambda)
        Runnable newRunnable = () -> System.out.println("Nouveau Runnable (Lambda)");
        new Thread(newRunnable).start();

        // Lambda avec un paramètre
        Consumer<String> printMessage = message -> System.out.println("Message : " + message);
        printMessage.accept("Hello Lambda!");

        // Lambda avec plusieurs paramètres
        Calculator add = (a, b) -> a + b;
        System.out.println("Somme : " + add.calculate(5, 3));
    }
}

@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}
```

### Streams API (Filtrage, Mapping, Réduction)

* L'API Stream, introduite en Java 8, permet de traiter des collections de données de manière fonctionnelle et déclarative. Elle supporte des opérations de pipeline qui peuvent être exécutées en parallèle.
* **Filtrage (`filter`)** : Sélectionne les éléments qui satisfont une condition.
* **Mapping (`map`)** : Transforme chaque élément en un autre type ou valeur.
* **Réduction (`reduce`, `collect`)** : Combine les éléments d'un stream en un seul résultat.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamAPIExample {
    public static void main(String[] args) {
        List<Integer> nombres = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Filtrage et mapping
        List<Integer> carresPairs = nombres.stream()
                                           .filter(n -> n % 2 == 0) // Garde seulement les nombres pairs
                                           .map(n -> n * n)        // Calcule le carré de chaque nombre
                                           .collect(Collectors.toList()); // Collecte les résultats dans une nouvelle liste
        System.out.println("Carrés des nombres pairs : " + carresPairs); // Affiche [4, 16, 36, 64, 100]

        // Réduction (somme)
        int somme = nombres.stream()
                           .reduce(0, (a, b) -> a + b); // Calcule la somme de tous les nombres
        System.out.println("Somme de tous les nombres : " + somme); // Affiche 55

        // Opérations terminales (forEach)
        nombres.stream()
               .filter(n -> n > 5)
               .forEach(System.out::println); // Affiche les nombres supérieurs à 5
    }
}
```

### Méthodes De Référence

* Les méthodes de référence sont une fonctionnalité de Java 8 qui permet de faire référence à des méthodes ou des constructeurs sans les exécuter. Elles sont une forme compacte d'expressions lambda qui ne font rien d'autre qu'appeler une méthode existante.

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> noms = Arrays.asList("Alice", "Bob", "Charlie");

        // Utilisation d'une expression lambda
        noms.forEach(s -> System.out.println(s));

        // Utilisation d'une méthode de référence (équivalent à la lambda ci-dessus)
        noms.forEach(System.out::println);

        // Référence à une méthode statique
        Consumer<Integer> printer = Integer::toHexString; // Référence à la méthode statique Integer.toHexString
        printer.accept(255); // Affiche "ff"

        // Référence à une méthode d'instance d'un objet particulier
        String prefix = "LOG: ";
        Consumer<String> logPrinter = prefix::concat; // Référence à la méthode concat de l'instance prefix
        logPrinter.accept("Message"); // Cela ne va pas imprimer, juste retourner une nouvelle chaîne.
                                     // Pour imprimer, il faudrait faire System.out.println(prefix.concat("Message"));
                                     // ou utiliser une lambda plus explicite.
                                     // L'exemple ci-dessous est plus pertinent pour l'impression.
        Consumer<String> printWithPrefix = s -> System.out.println(prefix + s);
        printWithPrefix.accept("Another Message");

        // Référence à une méthode d'instance d'un type arbitraire
        List<String> mots = Arrays.asList("apple", "banana", "cat");
        mots.sort(String::compareToIgnoreCase); // Référence à la méthode compareToIgnoreCase de String
        System.out.println("Mots triés : " + mots); // Affiche [apple, banana, cat]
    }
}
```

## 15. JDBC (Java Database Connectivity)

* JDBC est une API Java standard pour la connexion et l'interaction avec des bases de données relationnelles. Elle permet aux applications Java d'exécuter des requêtes SQL, de récupérer des résultats et de gérer les transactions.

### Connexion À Une Base De Données

* Charger le pilote JDBC du SGBD.
* Établir une connexion à la base de données en utilisant `DriverManager.getConnection()`.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class JDBCConnectionExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("Connexion à la base de données établie avec succès !");
            // La connexion sera automatiquement fermée grâce à try-with-resources
        } catch (SQLException e) {
            System.err.println("Erreur de connexion à la base de données : " + e.getMessage());
        }
    }
}
```

### Exécution De Requêtes SQL

* Utiliser `Statement` pour exécuter des requêtes SQL statiques.
* Utiliser `PreparedStatement` pour exécuter des requêtes SQL précompilées avec des paramètres, ce qui améliore la sécurité (prévention des injections SQL) et les performances.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class JDBCQueryExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            // Création d'une table (si elle n'existe pas)
            try (Statement stmt = conn.createStatement()) {
                String createTableSQL = "CREATE TABLE IF NOT EXISTS users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50), age INT)";
                stmt.execute(createTableSQL);
                System.out.println("Table 'users' créée ou déjà existante.");
            }

            // Insertion de données avec PreparedStatement
            String insertSQL = "INSERT INTO users (name, age) VALUES (?, ?)";
            try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
                pstmt.setString(1, "Alice");
                pstmt.setInt(2, 30);
                pstmt.executeUpdate();

                pstmt.setString(1, "Bob");
                pstmt.setInt(2, 25);
                pstmt.executeUpdate();
                System.out.println("Données insérées avec succès.");
            }

            // Sélection de données
            String selectSQL = "SELECT id, name, age FROM users";
            try (Statement stmt = conn.createStatement();
                 ResultSet rs = stmt.executeQuery(selectSQL)) {
                while (rs.next()) {
                    int id = rs.getInt("id");
                    String name = rs.getString("name");
                    int age = rs.getInt("age");
                    System.out.println("ID: " + id + ", Nom: " + name + ", Âge: " + age);
                }
            }

        } catch (SQLException e) {
            System.err.println("Erreur JDBC : " + e.getMessage());
        }
    }
}
```

### Gestion Des Résultats

* L'objet `ResultSet` contient les résultats d'une requête `SELECT`.
* Utiliser les méthodes `next()` pour itérer sur les lignes et les méthodes `getXXX()` (ex: `getString()`, `getInt()`) pour récupérer les valeurs des colonnes.

## 16. Build Tools (Maven/Gradle)

* Les outils de build sont essentiels dans les projets Java pour automatiser des tâches comme la compilation du code source, la gestion des dépendances, l'exécution des tests, et la création de packages déployables (JAR, WAR).

### Introduction À Maven

* **Maven** est un outil de gestion de projet et de compréhension de projet basé sur le concept de Project Object Model (POM). Il utilise un fichier `pom.xml` pour définir la configuration du projet, les dépendances, les plugins, etc.
* **Convention over Configuration** : Maven favorise une structure de projet standardisée, ce qui réduit la nécessité de configurations explicites.

```xml
<!-- Exemple de pom.xml minimal -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>mon-application</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

### Introduction À Gradle

* **Gradle** est un outil de build plus moderne et flexible, qui utilise un DSL (Domain Specific Language) basé sur Groovy ou Kotlin pour définir les scripts de build (`build.gradle` ou `build.gradle.kts`).
* Il offre une meilleure performance pour les builds incrémentaux et une plus grande flexibilité grâce à son approche basée sur des tâches.

```groovy
// Exemple de build.gradle minimal (Groovy DSL)
plugins {
    id 'java'
}

group 'com.example'
version '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'junit:junit:4.13.2'
}

test {
    useJUnitPlatform()
}
```

### Gestion Des Dépendances Et Compilation

* Les deux outils gèrent automatiquement le téléchargement des bibliothèques externes (dépendances) à partir de dépôts (comme Maven Central).
* Ils compilent le code source, exécutent les tests et empaquettent l'application.

## 17. Logging

* Le logging est le processus d'enregistrement des événements qui se produisent dans une application. Il est crucial pour le débogage, la surveillance et l'analyse du comportement d'une application en production.

### Introduction Au Logging

* En Java, le package `java.util.logging` fournit une API de logging de base, mais des frameworks tiers sont généralement préférés pour leur flexibilité et leurs fonctionnalités avancées.

```java
import java.util.logging.Logger;

public class SimpleLoggingExample {
    private static final Logger logger = Logger.getLogger(SimpleLoggingExample.class.getName());

    public static void main(String[] args) {
        logger.info("Ceci est un message d'information.");
        logger.warning("Ceci est un message d'avertissement.");
        logger.severe("Ceci est un message d'erreur grave.");
    }
}
```

### Frameworks De Logging (Log4j, SLF4j, Logback)

* **Log4j** : Un des premiers et des plus populaires frameworks de logging. Bien que Log4j 1.x soit obsolète, Log4j 2 est une version améliorée.
* **SLF4j (Simple Logging Facade for Java)** : Une façade de logging qui permet aux développeurs d'utiliser n'importe quel framework de logging sous-jacent (Log4j, Logback, java.util.logging) sans changer le code de l'application. C'est une bonne pratique d'utiliser SLF4j.
* **Logback** : Successeur de Log4j, conçu par le créateur de Log4j. Il offre de meilleures performances et plus de fonctionnalités.

### Niveaux De Log

* Les niveaux de log permettent de catégoriser les messages en fonction de leur importance. Les niveaux courants (du plus détaillé au plus critique) sont :
    * `TRACE`
    * `DEBUG`
    * `INFO`
    * `WARN`
    * `ERROR`
    * `FATAL`

## 18. Ressources Et Communauté

### Documentation Officielle

* [Oracle Java Documentation](https://docs.oracle.com/en/java/)
* [Java SE API Documentation](https://docs.oracle.com/en/java/javase/17/docs/api/index.html) (pour la version 17, ajuster selon la version)

### Communautés En Ligne

* [Stack Overflow](https://stackoverflow.com/questions/tagged/java) : Excellente ressource pour les questions et réponses techniques.
* [Reddit (r/java)](https://www.reddit.com/r/java/) : Communauté active pour les discussions, les actualités et l'aide.
* [Baeldung](https://www.baeldung.com/java-tutorials) : Tutoriels Java très complets et pratiques.

### Livres Et Cours

* **"Effective Java" par Joshua Bloch** : Un livre incontournable pour les développeurs Java de tous niveaux, offrant des conseils et des meilleures pratiques.
* **"Head First Java" par Kathy Sierra et Bert Bates** : Excellent pour les débutants, avec une approche visuelle et engageante.
* **"Spring in Action" par Craig Walls** : Pour ceux qui veulent maîtriser le framework Spring.
* **Cours en ligne** : Coursera, Udemy, edX, OpenClassrooms proposent de nombreux cours sur Java, du niveau débutant à avancé.

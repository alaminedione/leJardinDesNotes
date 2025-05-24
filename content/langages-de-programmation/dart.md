---
title: Dart
draft: false
tags:
  - dart
  - programming
  - flutter
description: Langage de programmation optimisé pour le développement d'applications multiplateformes avec Flutter.
---

# Dart

## Sommaire

1.  Introduction à Dart
    *   Qu'est-ce que Dart ?
    *   Historique et principes (AOT, JIT)
    *   Environnement d'exécution (Dart VM, Flutter)
    *   Compilation et exécution
    *   Écosystème Dart et cas d'utilisation
2.  Bases du Langage
    *   Syntaxe de base
    *   Variables et types de données (built-in types, `var`, `dynamic`)
    *   Opérateurs
    *   Structures de contrôle (conditions, boucles)
    *   Fonctions
    *   Collections (List, Set, Map)
3.  Programmation Orientée Objet (POO) en Dart
    *   Classes et Objets
    *   Encapsulation, Héritage, Polymorphisme
    *   Interfaces (implicites) et Classes Abstraites
    *   Mixins
    *   Constructeurs et `this`
4.  Gestion des Erreurs et Exceptions
    *   Types d'exceptions
    *   Blocs `try-on-catch-finally`
    *   Déclaration et levée d'exceptions
5.  Asynchronisme en Dart
    *   Futures
    *   `async` et `await`
    *   Streams
6.  Null Safety
    *   Introduction au Null Safety
    *   Types nullables et non-nullables
    *   Opérateurs de null safety (`?`, `!`, `??`, `?.`)
7.  Développement d'Applications avec Flutter
    *   Introduction à Flutter
    *   Widgets (StatelessWidget, StatefulWidget)
    *   Layouts et UI
    *   Gestion d'état (State Management)
8.  Bonnes Pratiques et Patterns
    *   Conventions de codage (Dart Style Guide)
    *   Patterns de conception courants
    *   Principes SOLID
9.  Ressources et Communauté
    *   Documentation officielle
    *   Communautés en ligne
    *   Livres et cours

## 1. Introduction à Dart

### Qu'est-ce Que Dart ?

Dart est un langage de programmation client optimisé pour le développement rapide d'applications sur n'importe quelle plateforme, avec un accent particulier sur le développement mobile, web et desktop via le framework Flutter. Il est développé par Google.

### Historique Et Principes (AOT, JIT)

*   Développé par Google, première version en 2011.
*   Conçu pour le développement d'applications client.
*   Supporte la compilation **AOT (Ahead-Of-Time)** pour des performances natives sur mobile et desktop.
*   Supporte la compilation **JIT (Just-In-Time)** pour un développement rapide avec "Hot Reload" sur Flutter.

### Environnement D'exécution (Dart VM, Flutter)

*   **Dart VM** : Machine virtuelle Dart, utilisée pour le développement rapide (JIT) et l'exécution côté serveur (bien que moins courant).
*   **Flutter** : Framework UI multiplateforme qui utilise Dart comme langage de programmation. Il compile le code Dart en code machine natif pour iOS, Android, web, et desktop.

### Compilation Et Exécution

1.  Écrire le code source Dart (`.dart`).
2.  Exécuter directement avec la Dart VM (`dart mon_programme.dart`) pour le développement.
3.  Compiler en JavaScript pour le web (`dart compile js mon_programme.dart`).
4.  Compiler en code machine natif pour les applications mobiles/desktop avec Flutter.

```bash
# Exécution directe
dart main.dart

# Compilation pour le web
dart compile js main.dart

# Exécution d'une application Flutter
flutter run
```

### Écosystème Dart Et Cas D'utilisation

*   **Développement Mobile (Flutter)** : Cas d'utilisation principal, permettant de créer des applications natives pour iOS et Android à partir d'une seule base de code.
*   **Développement Web** : Peut être utilisé pour le frontend web (compilé en JS) ou le backend (avec des frameworks comme Aqueduct ou Shelf).
*   **Développement Desktop (Flutter)** : Création d'applications natives pour Windows, macOS, Linux.
*   **Scripts et Outils en ligne de commande** : Dart est excellent pour écrire des scripts système ou des outils de développement.

## 2. Bases Du Langage

### Syntaxe De Base

*   Orienté objet : Tout est objet en Dart.
*   Syntaxe inspirée de C, Java et JavaScript.
*   Utilisation de classes, fonctions et variables.
*   Point d'entrée : la fonction `main()`.

```dart
void main() {
  print('Hello, Dart!');
}
```

### Variables Et Types De Données (built-in types, `var`, `dynamic`)

*   **Types built-in** : `int`, `double`, `String`, `bool`, `List`, `Map`, `Set`, `Runes`, `Symbol`.
*   **`var`** : Déclaration de variable dont le type est inféré par le compilateur.
*   **`dynamic`** : Variable dont le type peut changer à l'exécution (moins sûr, à utiliser avec prudence).
*   **`final`** : Variable qui ne peut être assignée qu'une seule fois.
*   **`const`** : Variable qui est une constante de compilation.

```dart
int age = 30;
String name = 'Alice';
double price = 99.99;
bool isActive = true;

var quantity = 100; // int
var message = 'Hello'; // String

dynamic anything = 'Can be anything';
anything = 123;

final DateTime now = DateTime.now();
const double PI = 3.14159;
```

### Opérateurs

*   Arithmétiques : `+`, `-`, `*`, `/`, `~/` (division entière), `%`
*   Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
*   Logiques : `&&`, `||`, `!`
*   Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
*   Incrémentation/Décrémentation : `++`, `--`
*   Opérateurs de type : `is`, `is!`, `as`
*   Opérateurs de null safety : `??`, `?.`, `!` (expliqués plus loin)

```dart
int x = 10;
int y = 5;
print(x + y); // 15
print(x == y); // false

String? nullableString;
print(nullableString ?? 'Default Value'); // 'Default Value'
```

### Structures De Contrôle (conditions, boucles)

*   `if`, `else if`, `else` : Conditionnelles
*   `for`, `while`, `do-while` : Boucles
*   `switch` : Sélection multiple

```dart
int score = 85;
if (score > 90) {
  print('Excellent');
} else if (score > 80) {
  print('Très bien');
} else {
  print('Bien');
}

for (int i = 0; i < 3; i++) {
  print(i);
}

int count = 0;
while (count < 2) {
  print('Count: $count');
  count++;
}
```

### Fonctions

*   Déclaration : `type_retour nomFonction(paramètres) { // corps }`
*   Fonctions fléchées (`=>`) pour les corps de fonction d'une seule expression.
*   Paramètres nommés et optionnels.

```dart
// Fonction simple
int add(int a, int b) {
  return a + b;
}

// Fonction fléchée
int multiply(int a, int b) => a * b;

// Paramètres nommés
void greet({String? name, String? message}) {
  print('$message, $name!');
}

void main() {
  print(add(2, 3)); // 5
  print(multiply(4, 5)); // 20
  greet(name: 'Alice', message: 'Bonjour'); // Bonjour, Alice!
}
```

### Collections (List, Set, Map)

*   **List** : Collection ordonnée d'éléments (permet les doublons).
*   **Set** : Collection non ordonnée d'éléments uniques (ne permet pas les doublons).
*   **Map** : Collection de paires clé-valeur (chaque clé est unique).

```dart
// List
List<int> numbers = [1, 2, 3];
numbers.add(4);
print(numbers[0]); // 1

// Set
Set<String> uniqueNames = {'Alice', 'Bob'};
uniqueNames.add('Alice'); // N'ajoute pas de doublon
print(uniqueNames); // {Alice, Bob}

// Map
Map<String, String> capitals = {
  'France': 'Paris',
  'Germany': 'Berlin',
};
print(capitals['France']); // Paris
capitals['Italy'] = 'Rome';
```

## 3. Programmation Orientée Objet (POO) en Dart

### Classes Et Objets

*   Une classe est un modèle pour créer des objets.
*   Un objet est une instance d'une classe.

```dart
class Car {
  String brand;
  String model;

  Car(this.brand, this.model); // Constructeur concis

  void displayInfo() {
    print('Brand: $brand, Model: $model');
  }
}

void main() {
  Car myCar = Car('Toyota', 'Corolla');
  myCar.displayInfo(); // Brand: Toyota, Model: Corolla
}
```

### Encapsulation, Héritage, Polymorphisme

*   **Encapsulation** : Les membres privés sont préfixés par un underscore (`_`).
*   **Héritage** : Utilisation du mot-clé `extends`.
*   **Polymorphisme** : Les objets peuvent prendre plusieurs formes (surcharge d'opérateurs, méthodes d'instance).

```dart
// Encapsulation
class Account {
  double _balance; // Privé

  Account(this._balance);

  double get balance => _balance; // Getter
  set balance(double newBalance) { // Setter
    if (newBalance >= 0) {
      _balance = newBalance;
    }
  }
}

// Héritage
class Animal {
  void makeSound() {
    print('Animal makes a sound');
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print('Dog barks');
  }
}

// Polymorphisme
void main() {
  Animal myDog = Dog();
  myDog.makeSound(); // Dog barks
}
```

### Interfaces (implicites) et Classes Abstraites

*   **Interfaces implicites** : En Dart, toutes les classes définissent implicitement une interface. Une classe peut implémenter l'interface d'une autre classe en utilisant le mot-clé `implements`.
*   **Classes Abstraites** : Classes qui ne peuvent pas être instanciées directement et qui peuvent contenir des méthodes abstraites (sans implémentation).

```dart
// Interface implicite
class Flyable {
  void fly() {
    print('Flying...');
  }
}

class Bird implements Flyable {
  @override
  void fly() {
    print('Bird is flying');
  }
}

// Classe Abstraite
abstract class Shape {
  double getArea(); // Méthode abstraite
  void display() {
    print('This is a shape');
  }
}

class Circle extends Shape {
  double radius;
  Circle(this.radius);

  @override
  double getArea() {
    return 3.14 * radius * radius;
  }
}
```

### Mixins

*   Les mixins permettent de réutiliser le code d'une classe dans plusieurs hiérarchies de classes. Ils sont utilisés avec le mot-clé `with`.

```dart
mixin Logger {
  void log(String message) {
    print('[LOG]: $message');
  }
}

class UserService with Logger {
  void createUser(String name) {
    log('User $name created');
  }
}

void main() {
  UserService service = UserService();
  service.createUser('John Doe'); // [LOG]: User John Doe created
}
```

### Constructeurs Et `this`

*   **Constructeur** : Méthode spéciale pour initialiser les objets.
*   **Constructeurs nommés** : Permettent de définir plusieurs constructeurs pour une classe.
*   **`this`** : Fait référence à l'instance courante de la classe.

```dart
class Point {
  double x, y;

  // Constructeur par défaut
  Point(this.x, this.y);

  // Constructeur nommé
  Point.origin() : this(0, 0);

  // Constructeur nommé avec initialisation
  Point.fromJson(Map<String, double> json)
      : x = json['x']!,
        y = json['y']!;

  void display() {
    print('Point: ($x, $y)');
  }
}

void main() {
  Point p1 = Point(10, 20);
  p1.display(); // Point: (10.0, 20.0)

  Point p2 = Point.origin();
  p2.display(); // Point: (0.0, 0.0)

  Point p3 = Point.fromJson({'x': 5.0, 'y': 15.0});
  p3.display(); // Point: (5.0, 15.0)
}
```

## 4. Gestion des Erreurs et Exceptions

### Types D'exceptions

*   Dart a des exceptions `Error` (erreurs de programmation, non récupérables) et `Exception` (conditions anormales, récupérables).
*   Exemples : `FormatException`, `StateError`, `ArgumentError`.

### Blocs `try-on-catch-finally`

*   `try` : Contient le code qui peut potentiellement lever une exception.
*   `on` : Gère une exception d'un type spécifique.
*   `catch` : Capture l'objet exception et/ou la pile d'appels.
*   `finally` : Contient le code qui est exécuté que l'exception soit levée ou non.

```dart
void main() {
  try {
    int result = 10 ~/ 0; // Division par zéro
    print(result);
  } on IntegerDivisionByZeroException {
    print('Cannot divide by zero!');
  } catch (e, s) {
    print('An unknown error occurred: $e');
    print('Stack trace: $s');
  } finally {
    print('Execution finished.');
  }
}
```

### Déclaration Et Levée D'exceptions

*   Utilisation du mot-clé `throw` pour lever une exception.

```dart
void checkAge(int age) {
  if (age < 0) {
    throw ArgumentError('Age cannot be negative');
  }
  print('Age is valid: $age');
}

void main() {
  try {
    checkAge(-5);
  } catch (e) {
    print('Error: $e'); // Error: Invalid argument(s): Age cannot be negative
  }
}
```

## 5. Asynchronisme en Dart

Dart est un langage à thread unique, mais il gère l'asynchronisme via un "event loop" et des "isolates" (pour le parallélisme).

### Futures

*   Un `Future` représente le résultat d'une opération asynchrone qui n'est pas encore disponible. Il peut être complété avec une valeur ou une erreur.

```dart
Future<String> fetchUserData() {
  return Future.delayed(Duration(seconds: 2), () => 'User data fetched!');
}

void main() {
  print('Fetching data...');
  fetchUserData().then((data) {
    print(data); // S'exécute après 2 secondes
  }).catchError((error) {
    print('Error: $error');
  });
  print('Program continues...');
}
```

### `async` et `await`

*   Les mots-clés `async` et `await` simplifient l'écriture de code asynchrone, le rendant plus lisible et similaire au code synchrone.
*   Une fonction marquée `async` retourne implicitement un `Future`.
*   `await` peut être utilisé pour attendre la complétion d'un `Future` dans une fonction `async`.

```dart
Future<String> fetchOrder() async {
  print('Fetching order...');
  await Future.delayed(Duration(seconds: 3));
  return 'Order #123 fetched!';
}

void main() async {
  String order = await fetchOrder(); // Attend la complétion du Future
  print(order);
  print('Main function finished.');
}
```

### Streams

*   Un `Stream` est une séquence de données asynchrones. Il peut émettre zéro ou plusieurs événements (données ou erreurs) au fil du temps. Utile pour les événements UI, les données de base de données en temps réel, etc.

```dart
Stream<int> countStream(int max) async* {
  for (int i = 1; i <= max; i++) {
    await Future.delayed(Duration(milliseconds: 500));
    yield i; // Émet une valeur
  }
}

void main() {
  print('Starting stream...');
  countStream(3).listen((number) {
    print('Received: $number');
  }, onDone: () {
    print('Stream finished.');
  }, onError: (error) {
    print('Stream error: $error');
  });
  print('Main continues after stream setup.');
}
```

## 6. Null Safety

### Introduction Au Null Safety

*   Introduit en Dart 2.12, le null safety est une fonctionnalité qui aide à prévenir les erreurs de référence nulle à l'exécution. Le compilateur Dart analyse le code pour s'assurer que les variables ne peuvent pas être nulles à moins que cela ne soit explicitement autorisé.

### Types Nullables Et Non-nullables

*   Par défaut, les types sont non-nullables (ex: `String`, `int`).
*   Pour rendre un type nullable, ajoutez un `?` après le type (ex: `String?`, `int?`).

```dart
String name = 'Alice'; // Non-nullable
// name = null; // Erreur de compilation

String? nullableName = 'Bob'; // Nullable
nullableName = null; // OK
```

### Opérateurs De Null Safety (`?`, `!`, `??`, `?.`)

*   **`?` (Nullable type)** : Déclare un type comme pouvant être nul.
*   **`!` (Null assertion operator)** : Indique au compilateur que vous êtes sûr qu'une expression nullable n'est pas nulle à ce point. À utiliser avec prudence, car si l'expression est nulle, une erreur d'exécution sera levée.
*   **`??` (Null-aware operator)** : Fournit une valeur par défaut si l'expression de gauche est nulle.
*   **`?.` (Null-aware access operator)** : Accède à un membre d'un objet seulement si l'objet n'est pas nul.

```dart
String? firstName;
String lastName = 'Doe';

// Utilisation de !
String fullName = firstName! + ' ' + lastName; // Peut lever une erreur si firstName est null

// Utilisation de ??
String displayFirstName = firstName ?? 'Guest';
print(displayFirstName); // Affiche 'Guest'

// Utilisation de ?.
int? length = firstName?.length; // length sera null si firstName est null
print(length); // Affiche null

// Combinaison
String userStatus = firstName?.isEmpty ?? true ? 'New User' : 'Existing User';
print(userStatus); // Affiche 'New User'
```

## 7. Développement d'Applications avec Flutter

### Introduction à Flutter

*   Flutter est le framework UI de Google pour la création d'applications compilées de manière native pour mobile, web et desktop à partir d'une seule base de code.
*   Il utilise Dart et est connu pour ses performances élevées et son "Hot Reload" pour un développement rapide.

### Widgets (StatelessWidget, StatefulWidget)

*   Tout en Flutter est un widget. Les widgets sont les blocs de construction de l'interface utilisateur.
*   **`StatelessWidget`** : Widgets qui n'ont pas d'état mutable. Leur configuration est définie au moment de la création.
*   **`StatefulWidget`** : Widgets qui peuvent changer d'état au cours de leur vie. Ils ont un objet `State` associé qui gère l'état mutable.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget { // StatelessWidget
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: Scaffold(
        appBar: AppBar(title: Text('Hello Flutter')),
        body: Center(
          child: Text('Welcome to Flutter!'),
        ),
      ),
    );
  }
}

class CounterApp extends StatefulWidget { // StatefulWidget
  @override
  _CounterAppState createState() => _CounterAppState();
}

class _CounterAppState extends State<CounterApp> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() { // Rebuild le widget avec le nouvel état
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter App')),
      body: Center(
        child: Text('Counter: $_counter', style: TextStyle(fontSize: 24)),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### Layouts et UI

*   Flutter utilise un système de composition de widgets pour construire des layouts.
*   Widgets courants pour le layout : `Row`, `Column`, `Stack`, `Container`, `Padding`, `Center`.

```dart
import 'package:flutter/material.dart';

class LayoutExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Layout Example')),
      body: Column( // Widgets organisés verticalement
        children: [
          Container(
            color: Colors.blue,
            padding: EdgeInsets.all(16),
            child: Text('Header', style: TextStyle(color: Colors.white)),
          ),
          Row( // Widgets organisés horizontalement
            mainAxisAlignment: MainAxisAlignment.spaceAround,
            children: [
              Icon(Icons.star, size: 50),
              Icon(Icons.star, size: 50),
              Icon(Icons.star, size: 50),
            ],
          ),
          Expanded( // Prend l'espace restant
            child: Center(
              child: Text('Main Content'),
            ),
          ),
        ],
      ),
    );
  }
}
```

### Gestion D'état (State Management)

*   La gestion d'état est cruciale pour les applications complexes. Flutter offre plusieurs approches :
    *   **`setState`** : Pour les états locaux simples (dans un `StatefulWidget`).
    *   **Provider** : Un package populaire pour la gestion d'état simple à moyenne.
    *   **Bloc/Cubit** : Pour les applications plus complexes, basé sur des événements et des états.
    *   **Riverpod** : Alternative à Provider, offrant une sécurité de type améliorée.
    *   **GetX** : Solution complète pour la gestion d'état, les dépendances et les routes.

## 8. Bonnes Pratiques et Patterns

### Conventions De Codage (Dart Style Guide)

*   Suivre le [Dart Style Guide](https://dart.dev/guides/language/effective-dart/style) pour un code cohérent et lisible.
*   Utiliser des noms clairs et descriptifs (`camelCase` pour les variables/fonctions, `PascalCase` pour les classes).
*   Formater le code avec `dart format`.

### Patterns De Conception Courants

*   **Singleton** : Assure qu'une classe n'a qu'une seule instance.
*   **Factory** : Fournit une méthode pour créer des objets sans exposer la logique de création.
*   **Observer** : Définit une dépendance un-à-plusieurs (souvent utilisé avec les Streams).
*   **Builder** : Sépare la construction d'un objet complexe de sa représentation.
*   **Provider/Bloc/Cubit** : Patterns spécifiques à Flutter pour la gestion d'état.

### Principes SOLID

Les principes SOLID sont applicables en Dart et Flutter pour concevoir des applications maintenables et évolutives.

*   **S (Single Responsibility Principle)** : Une classe ou un widget ne devrait avoir qu'une seule raison de changer.
*   **O (Open/Closed Principle)** : Les entités logicielles doivent être ouvertes à l'extension, mais fermées à la modification.
*   **L (Liskov Substitution Principle)** : Les objets d'un programme doivent pouvoir être remplacés par des instances de leurs sous-types sans altérer la justesse du programme.
*   **I (Interface Segregation Principle)** : Les clients ne devraient pas être forcés de dépendre d'interfaces qu'ils n'utilisent pas.
*   **D (Dependency Inversion Principle)** : Les modules de haut niveau ne devraient pas dépendre des modules de bas niveau. Les deux devraient dépendre d'abstractions.

## 9. Ressources et Communauté

### Documentation Officielle

*   [Dart Official Documentation](https://dart.dev/guides)
*   [Flutter Official Documentation](https://flutter.dev/docs)

### Communautés En Ligne

*   [Stack Overflow (Dart)](https://stackoverflow.com/questions/tagged/dart)
*   [Stack Overflow (Flutter)](https://stackoverflow.com/questions/tagged/flutter)
*   [Reddit (r/dartlang)](https://www.reddit.com/r/dartlang/)
*   [Reddit (r/flutterdev)](https://www.reddit.com/r/flutterdev/)

### Livres Et Cours

*   **"Dart Apprentice" par Ray Wenderlich** : Excellent pour apprendre Dart.
*   **"Flutter Apprentice" par Ray Wenderlich** : Pour maîtriser Flutter.
*   **Cours en ligne** : Udemy, Coursera, edX, et la chaîne YouTube officielle de Flutter proposent de nombreux tutoriels et cours.
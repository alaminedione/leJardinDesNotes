---
title: Go
draft: false
tags:
  - golang
  - programming
description: Langage de programmation compilé, concurrent et typé statiquement, conçu par Google.
---

# Golang

## Sommaire

1. Introduction à Go
    * Qu'est-ce que Go ?
    * Historique et philosophie
    * Installation et configuration
    * Espace de travail Go (GOPATH, Modules)
2. Bases du Langage
    * Syntaxe de base
    * Variables et types de données
        * Types de base
        * Types de données complexes
        * Types de données définis par l'utilisateur
        * Conversions de types
    * Constantes
    * Opérateurs
    * Structures de contrôle (if, for, switch)
    * Fonctions
    * Pointeurs
3. Types Composés
    * Tableaux (Arrays)
    * Slices
    * Maps
    * Structs
4. Interfaces
    * Déclaration et implémentation
    * Interfaces vides
5. Gestion des Erreurs
    * Le type `error`
    * Gestion des erreurs avec `if err != nil`
    * Panic et Recover
6. Concurrence (Goroutines et Channels)
    * Goroutines
    * Channels (synchronisés et bufferisés)
    * Le mot-clé `select`
    * Mutexes et WaitGroups
7. Packages et Modules
    * Création et utilisation de packages
    * Gestion des dépendances avec Go Modules
8. Entrées/Sorties (I/O)
    * Le package `io`
    * Lecture et écriture de fichiers
    * Manipulation de chaînes de caractères
9. Tests en Go
    * Le package `testing`
    * Tests unitaires
    * Tests d'exemple
10. Développement Web avec Go
    * Le package `net/http`
    * Création de serveurs web
    * Gestion des requêtes et réponses
    * Frameworks populaires (Gin, Echo)
11. Déploiement d'Applications Go
    * Création d'Exécutables
    * Utilisation de Docker
12. Intégration Continue
    * Utilisation de GitHub Actions
    * Utilisation de Travis CI
13. Microservices avec Go
    * Avantages de Go pour les Microservices
    * Frameworks pour Microservices
    * Exemple de Microservice
14. Bonnes Pratiques
    * Conventions de nommage
    * Formatage du code (go fmt)
    * Documentation (go doc)
15. Ressources et Communauté
    * Documentation officielle
    * Communautés en ligne

## 1. Introduction à Go

### Qu'est-ce Que Go ?

Go (ou Golang) est un langage de programmation compilé, concurrent et typé statiquement, développé par Google. Il a été conçu pour être simple, efficace et fiable.

### Historique Et Philosophie

* Développé chez Google par Robert Griesemer, Rob Pike et Ken Thompson.
* Première version en 2009.
* Objectifs : simplicité, concurrence, performance.
* Inspiré par des langages comme C, Pascal et Newsqueak.

### Installation Et Configuration

1. Télécharger le paquetage d'installation depuis [le site officiel](https://golang.org/dl/).
2. Installer Go en suivant les instructions spécifiques à votre système d'exploitation.
3. Configurer les variables d'environnement (GOPATH, PATH).

### Espace De Travail Go (GOPATH, Modules)

* **GOPATH** (déprécié) : Ancien système de gestion des dépendances. Définit l'emplacement du code source Go.
* **Go Modules** (recommandé) : Nouveau système de gestion des dépendances. Permet de gérer les dépendances de manière plus flexible et isolée.

```bash
# Activer les modules Go
go env -w GO111MODULE=on

# Initialiser un module Go
go mod init nom_du_module
```

## 2. Bases Du Langage

### Syntaxe De Base

* Similaire à C, mais avec une syntaxe plus propre et plus simple.
* Utilisation de `:=` pour l'inférence de type lors de la déclaration et de l'initialisation.
* Pas de point-virgule obligatoire à la fin des instructions.

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

### Variables Et Types De Données

* Déclaration : `var nom_variable type` ou `nom_variable := valeur`
* Types de base :
    * `int`, `int8`, `int16`, `int32`, `int64` : Entiers signés
    * `uint`, `uint8`, `uint16`, `uint32`, `uint64` : Entiers non signés
    * `float32`, `float64` : Nombres à virgule flottante
    * `complex64`, `complex128` : Nombres complexes
    * `bool` : Booléens (true ou false)
    * `string` : Chaînes de caractères

```go
var age int = 30
name := "John"
var pi float64 = 3.14159
is_valid := true
```

Go est un langage à typage statique, ce qui signifie que le type de chaque variable doit être connu à la compilation. Go offre plusieurs types de données de base, ainsi que la possibilité de définir des types de données complexes.

#### Types de données complexes

Go offre plusieurs types de données complexes, tels que les tableaux, les slices, les maps et les structs.

*   **Tableaux :** Un tableau est une collection d'éléments du même type, de taille fixe.
*   **Slices :** Un slice est une abstraction au-dessus des tableaux, permettant une taille dynamique.
*   **Maps :** Une map est une table de hachage (dictionnaire) associant des clés à des valeurs.
*   **Structs :** Un struct est un type composite regroupant des champs de types différents.

#### Types de données définis par l'utilisateur

Go permet également de définir des types de données personnalisés en utilisant le mot-clé `type`.

```go
type Celsius float64
type Fahrenheit float64
```

#### Conversions de types

Go exige des conversions de types explicites. Vous ne pouvez pas mélanger des types différents dans une expression sans effectuer une conversion.

```go
var x int = 10
var y float64 = float64(x)
```

### Constantes

* Déclaration : `const nom_constante type = valeur`
* Les constantes doivent être connues à la compilation.

```go
const PI float64 = 3.14159
const MAX_SIZE int = 100
```

### Opérateurs

* Arithmétiques : `+`, `-`, `*`, `/`, `%`
* Relationnels : `==`, `!=`, `<`, `>`, `<=`, `>=`
* Logiques : `&&`, `||`, `!`
* Affectation : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
* Incrémentation/Décrémentation : `++`, `--`

```go
x := 10
y := 5
sum := x + y
is_equal := (x == y)
condition := (x > 0 && y < 10)
x++
```

### Structures De Contrôle (if, For, switch)

* `if` : Conditionnelle
* `for` : Boucle
* `switch` : Sélection multiple

```go
score := 85
if score > 90 {
    // ...
} else if score > 80 {
    // ...
} else {
    // ...
}

for i := 0; i < 5; i++ {
    // ...
}

switch score {
case 100:
    // ...
case 90:
    // ...
default:
    // ...
}
```

### Fonctions

* Déclaration : `func nom_fonction(paramètres) type_retour { // corps }`
* Possibilité de retourner plusieurs valeurs.

```go
func add(a int, b int) int {
    return a + b
}

func divide(a int, b int) (int, error) {
    if b == 0 {
        return 0, fmt.Errorf("division par zéro")
    }
    return a / b, nil
}

func main() {
    result := add(5, 3)
    fmt.Println(result)
}
```

### Pointeurs

* Similaires à C, mais avec une gestion de la mémoire plus sûre.
* Opérateur d'adresse : `&`
* Opérateur de déréférencement : `*`

```go
var x int = 10
var ptr *int = &x

fmt.Println("Adresse de x:", &x)
fmt.Println("Valeur de ptr:", ptr)
fmt.Println("Valeur pointée par ptr:", *ptr)

*ptr = 20
fmt.Println("Nouvelle valeur de x:", x)
```

## 3. Types Composés

### Tableaux (Arrays)

* Collection d'éléments du même type avec une taille fixe.
* Déclaration : `var nom_tableau [taille]type`

```go
var numbers [5]int
numbers[0] = 10
numbers[1] = 20

names := [3]string{"Alice", "Bob", "Charlie"}
```

### Slices

* Abstraction au-dessus des tableaux, permettant une taille dynamique.
* Déclaration : `var nom_slice []type`
* Utilisation de `make` pour créer un slice.
* Fonctions `append` et `len` pour manipuler les slices.

```go
var numbers []int
numbers = make([]int, 5) // Crée un slice de taille 5

numbers = append(numbers, 10) // Ajoute un élément

fmt.Println("Taille du slice:", len(numbers))
```

### Maps

* Table de hachage (dictionnaire) associant des clés à des valeurs.
* Déclaration : `var nom_map map[type_clé]type_valeur`
* Utilisation de `make` pour créer une map.

```go
var ages map[string]int
ages = make(map[string]int)

ages["Alice"] = 30
ages["Bob"] = 25

fmt.Println("Age de Alice:", ages["Alice"])
```

### Structs

* Type composite regroupant des champs de types différents.
* Déclaration :

```go
type Person struct {
    Name string
    Age  int
}

var person Person
person.Name = "John"
person.Age = 30

fmt.Println("Nom:", person.Name)
```

## 4. Interfaces

### Déclaration Et Implémentation

* Une interface définit un ensemble de méthodes qu'un type doit implémenter.
* Un type implémente une interface en définissant toutes les méthodes de l'interface.

```go
type Animal interface {
    Speak() string
}

type Dog struct {
    Name string
}

func (d Dog) Speak() string {
    return "Woof!"
}

var animal Animal = Dog{Name: "Fido"}
fmt.Println(animal.Speak())
```

### Interfaces Vides

* L'interface vide `interface{}` peut contenir n'importe quel type de valeur.
* Utile pour écrire du code générique.

```go
var i interface{}
i = 10
i = "Hello"

fmt.Println(i)
```

## 5. Gestion Des Erreurs

### Le Type `error`

* Go n'a pas d'exceptions. Les erreurs sont gérées en retournant une valeur de type `error`.
* Le type `error` est une interface avec une seule méthode : `Error() string`.

### Gestion Des Erreurs Avec `if err != nil`

* La manière la plus courante de gérer les erreurs en Go est de vérifier si la valeur de retour `error` est `nil`.

```go
result, err := divide(10, 2)
if err != nil {
    fmt.Println("Erreur:", err)
    return
}

fmt.Println("Résultat:", result)
```

### Panic Et Recover

* `panic` : Provoque l'arrêt brutal du programme. À utiliser en cas d'erreurs irrécupérables.
* `recover` : Permet de récupérer après un `panic`. Doit être utilisé dans une fonction `defer`.

```go
func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Récupération après panic:", r)
        }
    }()

    // ... code qui peut provoquer un panic ...
}
```

## 6. Concurrence (Goroutines Et Channels)

### Goroutines

* Fonctions légères exécutées de manière concurrente.
* Lancées avec le mot-clé `go`.

```go
go maFonction()
```

### Channels (synchronisés Et bufferisés)

* Permettent la communication et la synchronisation entre les goroutines.
* Déclaration : `make(chan type)`
* Synchronisés : Bloquent l'expéditeur jusqu'à ce que le récepteur reçoive la valeur.
* Bufferisés : Peuvent stocker un nombre limité de valeurs avant de bloquer l'expéditeur.

```go
ch := make(chan int) // Channel synchronisé

go func() {
    ch <- 10 // Envoie la valeur 10 dans le channel
}()

value := <-ch // Reçoit la valeur du channel
fmt.Println(value)
```

### Le Mot-clé `select`

* Permet d'attendre sur plusieurs opérations de channel.

```go
select {
case value := <-ch1:
    // ...
case value := <-ch2:
    // ...
default:
    // ...
}
```

### Mutexes Et WaitGroups

* `Mutex` : Permet de protéger l'accès concurrent à une ressource partagée.
* `WaitGroup` : Permet d'attendre la fin de plusieurs goroutines.

```go
var mutex sync.Mutex

mutex.Lock()
// ... accéder à la ressource partagée ...
mutex.Unlock()

var wg sync.WaitGroup
wg.Add(2) // Ajoute 2 goroutines à attendre

go func() {
    defer wg.Done() // Indique que la goroutine est terminée
    // ...
}()

go func() {
    defer wg.Done()
    // ...
}()

wg.Wait() // Attend que toutes les goroutines soient terminées
```

## 7. Packages Et Modules

### Création Et Utilisation De Packages

* Un package est un ensemble de fichiers Go regroupés dans un même répertoire.
* Le nom du package est spécifié en haut de chaque fichier avec le mot-clé `package`.
* Les fonctions et les variables exportées (commençant par une majuscule) peuvent être utilisées depuis d'autres packages.

```go
// mypackage/mypackage.go
package mypackage

func MyFunction() {
    // ...
}
```

```go
// main.go
package main

import "mypackage"

func main() {
    mypackage.MyFunction()
}
```

### Gestion Des Dépendances Avec Go Modules

* Go Modules est le système de gestion des dépendances intégré à Go.
* Permet de gérer les versions des dépendances et d'assurer la reproductibilité des builds.

```bash
go mod init nom_du_module
go get github.com/nom/du/paquet
```

## 8. Entrées/Sorties (I/O)

### Le Package `io`

* Le package `io` fournit des interfaces de base pour les opérations d'entrée/sortie.
* Interfaces principales : `Reader`, `Writer`.

### Lecture Et Écriture De Fichiers

* Utilisation des packages `os` et `io/ioutil` pour lire et écrire des fichiers.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "os"
)

func main() {
    // Écriture dans un fichier
    err := ioutil.WriteFile("myfile.txt", []byte("Hello, file!"), 0644)
    if err != nil {
        fmt.Println("Erreur lors de l'écriture:", err)
        return
    }

    // Lecture depuis un fichier
    data, err := ioutil.ReadFile("myfile.txt")
    if err != nil {
        fmt.Println("Erreur lors de la lecture:", err)
        return
    }

    fmt.Println("Contenu du fichier:", string(data))

    os.Remove("myfile.txt") // Supprime le fichier
}
```

### Manipulation De Chaînes De Caractères

* Le package `strings` fournit des fonctions pour manipuler les chaînes de caractères.

```go
import "strings"

str := "Hello, World!"
fmt.Println(strings.ToUpper(str)) // HELLO, WORLD!
```

## 9. Tests En Go

### Le Package `testing`

* Le package `testing` fournit les outils nécessaires pour écrire des tests en Go.
* Les fichiers de test doivent avoir le suffixe `_test.go`.
* Les fonctions de test doivent commencer par `Test`.

### Tests Unitaires

* Vérifient le comportement d'une fonction ou d'une méthode.

```go
// mypackage/mypackage.go
package mypackage

func Add(a, b int) int {
    return a + b
}
```

```go
// mypackage/mypackage_test.go
package mypackage

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    if result != 5 {
        t.Errorf("Add(2, 3) = %d; want 5", result)
    }
}
```

### Tests D'exemple

* Fournissent des exemples d'utilisation du code.
* Sont compilés et exécutés lors des tests.

```go
func ExampleAdd() {
    result := Add(2, 3)
    fmt.Println(result)
    // Output: 5
}
```

## 10. Développement Web Avec Go

### Le Package `net/http`

* Le package `net/http` fournit les outils nécessaires pour créer des serveurs web en Go.

### Création De Serveurs Web

* Utilisation de la fonction `HandleFunc` pour enregistrer des gestionnaires de requêtes.
* Utilisation de la fonction `ListenAndServe` pour démarrer le serveur.

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

### Gestion Des Requêtes Et Réponses

* L'objet `http.Request` contient des informations sur la requête HTTP.
* L'objet `http.ResponseWriter` permet d'écrire la réponse HTTP.

### Frameworks Populaires (Gin, Echo)

* `Gin` : Framework web léger et performant.
* `Echo` : Autre framework web populaire, mettant l'accent sur la simplicité et la performance.

## 13. Microservices avec Go

Go est un excellent choix pour la construction de microservices en raison de sa performance, de sa simplicité et de sa concurrence.

### Avantages de Go pour les Microservices

*   **Performance :** Go est un langage compilé qui offre d'excellentes performances.
*   **Simplicité :** La syntaxe de Go est simple et facile à apprendre.
*   **Concurrence :** Go offre d'excellentes fonctionnalités de concurrence grâce aux goroutines et aux channels.
*   **Déploiement facile :** Go produit des exécutables autonomes qui sont faciles à déployer.

### Frameworks pour Microservices

*   **Go Micro :** Un framework pour la construction de microservices en Go.
*   **Kratos :** Un autre framework populaire pour les microservices en Go.

### Exemple de Microservice

Voici un exemple simple de microservice en Go qui expose une API REST pour récupérer des informations sur un utilisateur.

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"

	"github.com/gorilla/mux"
)

type User struct {
	ID    string `json:"id"`
	Name  string `json:"name"`
	Email string `json:"email"`
}

func GetUser(w http.ResponseWriter, r *http.Request) {
	params := mux.Vars(r)
	userID := params["id"]

	user := User{
		ID:    userID,
		Name:  "John Doe",
		Email: "john.doe@example.com",
	}

	json.NewEncoder(w).Encode(user)
}

func main() {
	r := mux.NewRouter()

	r.HandleFunc("/users/{id}", GetUser).Methods("GET")

	fmt.Println("Serveur démarré sur le port 8000")
	http.ListenAndServe(":8000", r)
}
```

Ce code utilise le framework `gorilla/mux` pour gérer les routes HTTP. La fonction `GetUser` récupère l'ID de l'utilisateur à partir des paramètres de la requête et renvoie un objet `User` au format JSON.
## 12. Intégration Continue

L'intégration continue (CI) est une pratique de développement logiciel qui consiste à automatiser les tests et le déploiement de votre application à chaque modification du code. Cela permet de détecter rapidement les erreurs et de s'assurer que votre application est toujours dans un état stable.

### Utilisation de GitHub Actions

GitHub Actions est une plateforme d'automatisation CI/CD intégrée à GitHub. Vous pouvez créer un fichier de workflow dans le répertoire `.github/workflows` de votre dépôt pour définir les étapes de votre pipeline CI/CD.

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Go
      uses: actions/setup-go@v2
      with:
        go-version: '1.17'
    - name: Build
      run: go build -v ./...
    - name: Test
      run: go test -v ./...
```

Ce workflow effectue les étapes suivantes :

*   Déclenche le workflow à chaque push ou pull request sur la branche `main`.
*   Utilise l'image `ubuntu-latest` comme environnement de build.
*   Configure Go avec la version 1.17.
*   Construit l'application en utilisant la commande `go build`.
*   Exécute les tests en utilisant la commande `go test`.

### Utilisation de Travis CI

Travis CI est une autre plateforme d'automatisation CI/CD populaire. Vous pouvez créer un fichier `.travis.yml` à la racine de votre dépôt pour définir les étapes de votre pipeline CI/CD.

```yaml
language: go
go:
  - "1.17"

before_install:
  - go get -u golang.org/x/lint/golint

script:
  - go build -v ./...
  - go test -v ./...
  - golint ./...
```

Ce fichier effectue les étapes suivantes :

*   Spécifie que le langage est Go et que la version est 1.17.
*   Installe `golint` avant d'exécuter les tests.
*   Construit l'application en utilisant la commande `go build`.
*   Exécute les tests en utilisant la commande `go test`.
*   Exécute `golint` pour vérifier le style du code.
## 11. Déploiement d'Applications Go

### Création d'Exécutables

Pour déployer une application Go, vous devez d'abord créer un exécutable. Vous pouvez le faire en utilisant la commande `go build`.

```bash
go build -o myapp main.go
```

Cela créera un exécutable nommé `myapp` dans le répertoire courant.

### Utilisation de Docker

Docker est un outil populaire pour le déploiement d'applications. Vous pouvez créer une image Docker pour votre application Go en utilisant un fichier Dockerfile.

```dockerfile
FROM golang:latest

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download && go mod verify

COPY . .

RUN go build -o myapp main.go

EXPOSE 8080

CMD ["./myapp"]
```

Ce Dockerfile utilise l'image `golang:latest` comme base, copie le code source de l'application dans le conteneur, télécharge les dépendances, construit l'exécutable et expose le port 8080.

Vous pouvez ensuite construire l'image Docker en utilisant la commande `docker build`.

```bash
docker build -t myapp .
```

Et exécuter le conteneur en utilisant la commande `docker run`.

```bash
docker run -p 8080:8080 myapp
```

### Frameworks Populaires (Gin, Echo, Fiber)

* `Gin` : Framework web léger et performant, idéal pour les API.
* `Echo` : Framework web mettant l'accent sur la simplicité et la performance.
* `Fiber` : Framework web inspiré par Express.js, offrant une expérience de développement familière aux développeurs Node.js.

### Outils Utiles

* `GoLand` : IDE populaire pour le développement Go, offrant des fonctionnalités avancées telles que l'autocomplétion, le débogage et le refactoring.
* `Delve` : Débogueur pour Go.
* `Staticcheck` : Linter pour Go.
## 11. Bonnes Pratiques

### Conventions De Nommage

* Utiliser des noms clairs et descriptifs.
* Utiliser le camelCase pour les noms de variables et de fonctions.
* Utiliser des noms courts pour les variables locales.
* Utiliser des noms longs pour les variables globales.

### Formatage Du Code (go fmt)

* Utiliser l'outil `go fmt` pour formater automatiquement le code.
* Assure une cohérence du style de code dans tout le projet.

```bash
go fmt ./...
```

### Documentation (go doc)

* Écrire des commentaires pour documenter le code.
* Utiliser l'outil `go doc` pour générer la documentation.

```bash
go doc nom_du_package
```

## 12. Ressources Et Communauté

### Documentation Officielle

* [The Go Programming Language](https://golang.org/)

### Communautés En Ligne

* [Stack Overflow](https://stackoverflow.com/)
* [Reddit (r/golang)](https://www.reddit.com/r/golang/)

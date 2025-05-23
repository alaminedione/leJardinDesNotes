# Créer une API REST simple avec Spring Boot

## Introduction

Dans le monde moderne du développement logiciel, les API REST sont devenues un standard de facto pour permettre la communication entre différentes applications. Elles offrent une approche flexible et stateless pour interagir avec des ressources. Spring Boot, grâce à sa configuration simplifiée et son riche écosystème, est particulièrement bien adapté pour construire rapidement des API REST robustes et performantes en Java.

Cet article vous guidera pas à pas pour créer une API REST simple en utilisant Spring Boot. Nous allons développer une petite application de gestion de tâches (Todo List) pour illustrer les concepts clés.

## Contenu principal

### Conception de l'API

Notre API de gestion de tâches permettra d'effectuer les opérations CRUD (Create, Read, Update, Delete) sur des objets `Todo`.

**Endpoints prévus :**

*   `GET /api/todos` : Lister toutes les tâches.
*   `POST /api/todos` : Créer une nouvelle tâche. Le corps de la requête contiendra les données de la tâche.
*   `GET /api/todos/{id}` : Récupérer une tâche spécifique par son identifiant.
*   `PUT /api/todos/{id}` : Mettre à jour une tâche spécifique par son identifiant. Le corps de la requête contiendra les nouvelles données.
*   `DELETE /api/todos/{id}` : Supprimer une tâche spécifique par son identifiant.

**Structure des données (Modèle Todo) :**

Une tâche simple pourrait avoir les attributs suivants :

*   `id` : Un identifiant unique (pourra être généré automatiquement).
*   `title` : Le titre de la tâche (une chaîne de caractères).
*   `completed` : Un booléen indiquant si la tâche est terminée.

### Mise en place du modèle

Créons une classe Java pour représenter notre modèle `Todo`. Pour cet exemple simple sans base de données persistante pour l'instant (nous verrons la persistance plus tard), nous allons juste utiliser une classe POJO (Plain Old Java Object).

```articles/spring-boot/src/main/java/com/example/demo/model/Todo.java
package com.example.demo.model;

public class Todo {
    private Long id;
    private String title;
    private boolean completed;

    // Constructeur par défaut (nécessaire pour la désérialisation JSON)
    public Todo() {
    }

    // Constructeur avec arguments
    public Todo(Long id, String title, boolean completed) {
        this.id = id;
        this.title = title;
        this.completed = completed;
    }

    // Getters et Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public boolean isCompleted() {
        return completed;
    }

    public void setCompleted(boolean completed) {
        this.completed = completed;
    }
}
```
*Note : Dans une application réelle utilisant JPA, cette classe serait annotée avec `@Entity` et d'autres annotations JPA.*

### Création du contrôleur REST

Nous allons maintenant créer une classe contrôleur qui gérera les requêtes HTTP entrantes et renverra les réponses appropriées. Nous utiliserons l'annotation `@RestController`, qui est une combinaison de `@Controller` et `@ResponseBody`. `@Controller` indique à Spring que cette classe est un contrôleur web, et `@ResponseBody` indique que les valeurs de retour des méthodes doivent être sérialisées directement dans le corps de la réponse HTTP (généralement en JSON par défaut avec Spring Boot).

Pour cet exemple simple, nous allons stocker les tâches dans une simple liste en mémoire. Dans une application réelle, vous interagiriez avec une couche Service qui elle-même utiliserait une couche Repository pour accéder à une base de données.

```articles/spring-boot/src/main/java/com/example/demo/controller/TodoController.java
package com.example.demo.controller;

import com.example.demo.model.Todo;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.concurrent.atomic.AtomicLong;

@RestController
@RequestMapping("/api/todos") // Chemin de base pour toutes les routes de ce contrôleur
public class TodoController {

    private List<Todo> todos = new ArrayList<>();
    private AtomicLong nextId = new AtomicLong(1);

    // Initialisation simple avec quelques tâches
    public TodoController() {
        todos.add(new Todo(nextId.getAndIncrement(), "Apprendre Spring Boot", false));
        todos.add(new Todo(nextId.getAndIncrement(), "Créer une API REST", false));
    }

    // GET /api/todos
    @GetMapping
    public List<Todo> getAllTodos() {
        return todos;
    }

    // GET /api/todos/{id}
    @GetMapping("/{id}")
    public ResponseEntity<Todo> getTodoById(@PathVariable Long id) {
        Optional<Todo> todo = todos.stream()
                                  .filter(t -> t.getId().equals(id))
                                  .findFirst();
        return todo.map(ResponseEntity::ok) // Si la tâche est trouvée, renvoyer 200 OK avec le corps
                   .orElse(ResponseEntity.notFound().build()); // Sinon, renvoyer 404 Not Found
    }

    // POST /api/todos
    @PostMapping
    public Todo createTodo(@RequestBody Todo todo) {
        todo.setId(nextId.getAndIncrement()); // Assigner un nouvel ID
        todos.add(todo);
        return todo;
    }

    // PUT /api/todos/{id}
    @PutMapping("/{id}")
    public ResponseEntity<Todo> updateTodo(@PathVariable Long id, @RequestBody Todo updatedTodo) {
        Optional<Todo> todoOptional = todos.stream()
                                          .filter(t -> t.getId().equals(id))
                                          .findFirst();

        if (todoOptional.isPresent()) {
            Todo todo = todoOptional.get();
            todo.setTitle(updatedTodo.getTitle());
            todo.setCompleted(updatedTodo.isCompleted());
            return ResponseEntity.ok(todo); // Renvoyer 200 OK avec la tâche mise à jour
        } else {
            return ResponseEntity.notFound().build(); // Sinon, renvoyer 404 Not Found
        }
    }

    // DELETE /api/todos/{id}
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteTodo(@PathVariable Long id) {
        boolean removed = todos.removeIf(todo -> todo.getId().equals(id));

        if (removed) {
            return ResponseEntity.noContent().build(); // Renvoyer 204 No Content si supprimé avec succès
        } else {
            return ResponseEntity.notFound().build(); // Sinon, renvoyer 404 Not Found
        }
    }
}
```

**Explication des annotations utilisées :**

*   `@RestController` : Marque la classe comme un contrôleur où les méthodes renvoient directement des données sérialisées (JSON/XML).
*   `@RequestMapping("/api/todos")` : Définit le chemin de base pour toutes les requêtes gérées par ce contrôleur.
*   `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping` : Annotations spécifiques pour mapper les méthodes HTTP GET, POST, PUT, DELETE à des méthodes de contrôleur. Ce sont des raccourcis pour `@RequestMapping(method = RequestMethod.GET, value = "...")`.
*   `@PathVariable Long id` : Permet d'extraire la valeur de l'identifiant (`{id}`) depuis le chemin de l'URL et de l'injecter comme argument de la méthode.
*   `@RequestBody Todo updatedTodo` : Indique que le corps de la requête HTTP doit être désérialisé (converti) en un objet `Todo` et injecté comme argument. Spring utilise Jackson par défaut pour la conversion JSON.
*   `ResponseEntity<T>` : Une classe utilitaire de Spring pour représenter la réponse HTTP complète (corps, en-têtes et statut HTTP). `ResponseEntity.ok()` renvoie un statut 200 OK, `ResponseEntity.notFound().build()` renvoie un statut 404 Not Found, et `ResponseEntity.noContent().build()` renvoie un statut 204 No Content.

### Test de l'API

Pour tester votre API, vous pouvez utiliser des outils comme Postman, Insomnia, ou la ligne de commande avec `curl`.

1.  **Démarrez l'application Spring Boot.** Si vous utilisez un IDE, exécutez simplement la classe principale (celle annotée avec `@SpringBootApplication`). Si vous utilisez Maven, exécutez `mvn spring-boot:run`. Si vous utilisez Gradle, exécutez `gradle bootRun`. L'application démarrera par défaut sur `http://localhost:8080`.

2.  **Exemples de requêtes (avec `curl`) :**

    *   **Lister toutes les tâches (GET)**
        ```bash
        curl http://localhost:8080/api/todos
        ```
        Vous devriez obtenir une réponse similaire à :
        ```json
        [
          {
            "id": 1,
            "title": "Apprendre Spring Boot",
            "completed": false
          },
          {
            "id": 2,
            "title": "Créer une API REST",
            "completed": false
          }
        ]
        ```

    *   **Créer une nouvelle tâche (POST)**
        ```bash
        curl -X POST -H "Content-Type: application/json" -d '{"title":"Ajouter la persistance","completed":false}' http://localhost:8080/api/todos
        ```
        La réponse contiendra la nouvelle tâche créée avec son ID :
        ```json
        {
          "id": 3,
          "title": "Ajouter la persistance",
          "completed": false
        }
        ```

    *   **Récupérer une tâche par ID (GET)**
        ```bash
        curl http://localhost:8080/api/todos/1
        ```
        Réponse :
        ```json
        {
          "id": 1,
          "title": "Apprendre Spring Boot",
          "completed": false
        }
        ```
        Si vous demandez un ID qui n'existe pas (`/api/todos/99`), vous devriez obtenir une réponse 404 Not Found.

    *   **Mettre à jour une tâche (PUT)**
        ```bash
        curl -X PUT -H "Content-Type: application/json" -d '{"title":"Créer une API REST (Terminé)","completed":true}' http://localhost:8080/api/todos/2
        ```
        Réponse avec la tâche mise à jour :
        ```json
        {
          "id": 2,
          "title": "Créer une API REST (Terminé)",
          "completed": true
        }
        ```

    *   **Supprimer une tâche (DELETE)**
        ```bash
        curl -X DELETE http://localhost:8080/api/todos/3 -v
        ```
        La réponse aura un statut 204 No Content si la suppression réussit (le `-v` permet de voir les en-têtes incluant le statut). Si l'ID n'existe pas, vous obtiendrez 404 Not Found.

## Conclusion

Vous avez maintenant créé une API REST simple avec Spring Boot capable de gérer des opérations CRUD de base sur une ressource `Todo`. Vous avez vu comment utiliser les annotations `@RestController`, `@RequestMapping` et les annotations spécifiques aux méthodes HTTP (`@GetMapping`, etc.), ainsi que `@PathVariable` et `@RequestBody` pour gérer les données des requêtes et des réponses. L'utilisation de `ResponseEntity` vous a permis de contrôler le statut HTTP des réponses.

**Extensions possibles :**

*   **Validation :** Ajouter des contraintes de validation sur le modèle `Todo` (par exemple, le titre ne peut pas être vide) en utilisant l'API Validation de Java (Bean Validation / JSR 380) et l'intégration de Spring.
*   **Persistance :** Connecter l'API à une base de données réelle en utilisant Spring Data JPA, comme nous le verrons dans le prochain article.
*   **Gestion d'erreurs avancée :** Mettre en place un mécanisme global pour gérer les exceptions et renvoyer des messages d'erreur cohérents.
*   **Pagination et Filtrage :** Ajouter des paramètres de requête pour permettre de paginer ou de filtrer la liste des tâches.

**Bonnes pratiques REST à retenir :**

*   Utiliser les verbes HTTP appropriés (GET pour la lecture, POST pour la création, PUT pour la mise à jour complète, PATCH pour la mise à jour partielle, DELETE pour la suppression).
*   Utiliser les codes de statut HTTP corrects pour indiquer le résultat de l'opération (200 OK, 201 Created, 204 No Content, 400 Bad Request, 404 Not Found, 500 Internal Server Error, etc.).
*   Utiliser des noms de ressources (chemins d'URL) clairs et cohérents (ex: `/api/todos` plutôt que `/getAllTodos`).
*   Utiliser le format de données approprié (JSON est le plus courant).

Ce n'est qu'un début ! Spring Boot offre beaucoup plus de fonctionnalités pour construire des API REST sophistiquées. Continuez votre apprentissage avec les articles suivants pour découvrir comment intégrer une base de données, sécuriser votre API, et bien plus encore.
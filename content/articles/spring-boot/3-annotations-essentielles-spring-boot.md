# 3. Les Annotations Essentielles Dans Spring Boot : Un Guide Débutant

## Introduction

Dans l'univers de Spring et, plus particulièrement, de Spring Boot, les annotations jouent un rôle absolument central. Elles remplacent une grande partie de la configuration XML ou Java que l'on trouvait dans les applications Spring traditionnelles, rendant le code plus concis, lisible et "magique" (dans le bon sens du terme !).

### Le Rôle Central Des Annotations Dans Spring Boot

Les annotations sont des métadonnées ajoutées au code Java qui fournissent des informations au framework Spring lors de l'exécution ou de la compilation. Elles permettent de déclarer des beans, de configurer l'injection de dépendances, de mapper des requêtes web, de gérer les transactions, et bien plus encore, souvent sans nécessiter de code supplémentaire ou de configuration externe lourde.

### Pourquoi Comprendre Les Annotations Est Crucial

Pour un développeur débutant avec Spring Boot, comprendre les annotations est la clé pour décoder comment l'application fonctionne sous le capot. Elles expliquent comment les composants sont découverts, comment les dépendances sont résolues, comment les requêtes web sont traitées, etc. Sans cette compréhension, Spring Boot peut sembler être une boîte noire.

Cet article vous présentera les annotations les plus courantes et essentielles que vous rencontrerez en débutant avec Spring Boot.

## Contenu Principal

Explorons les annotations regroupées par catégorie pour mieux comprendre leur rôle.

### Annotations De Configuration

Ces annotations aident Spring Boot à configurer l'application et à gérer le contexte de l'application.

- `@SpringBootApplication`: C'est l'annotation principale que l'on trouve sur la classe de démarrage de l'application. C'est une annotation de commodité qui regroupe trois annotations courantes :
    - `@Configuration`: Indique que la classe contient des méthodes annotées `@Bean` qui créent des beans gérés par le conteneur Spring.
    - `@EnableAutoConfiguration`: Déclenche l'auto-configuration de Spring Boot. Elle examine les JARs présents dans le classpath et configure automatiquement les beans basés sur ces dépendances et les paramètres de configuration.
    - `@ComponentScan`: Active le scan des composants. Elle indique à Spring de rechercher d'autres composants (classes annotées `@Component`, `@Service`, `@Repository`, `@Controller`, etc.) dans le package de la classe actuelle (et ses sous-packages) et de les enregistrer comme des beans.

    ```java
    package com.example.demo;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication // Équivaut à @Configuration + @EnableAutoConfiguration + @ComponentScan
    public class MyApplication {

        public static void main(String[] args) {
            SpringApplication.run(MyApplication.class, args);
        }

    }
    ```

- `@Bean`: Utilisée dans une classe `@Configuration`, cette annotation indique que la méthode produit un bean qui doit être géré par le conteneur Spring. Le nom de la méthode est utilisé comme nom du bean par défaut.

    ```java
    package com.example.demo.config;

    import com.example.demo.service.MyService;
    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;

    @Configuration
    public class AppConfig {

        @Bean // Déclare un bean de type MyService
        public MyService myService() {
            return new MyService(); // Instanciation du bean
        }
    }
    ```

- `@ConfigurationProperties`: Permet de lier des propriétés externes (depuis `application.properties` ou `application.yml`) à un bean Java fortement typé.

    ```java
    package com.example.demo.config;

    import org.springframework.boot.context.properties.ConfigurationProperties;
    import org.springframework.stereotype.Component;

    @Component
    @ConfigurationProperties(prefix = "app") // Lie les propriétés commençant par "app."
    public class AppProperties {
        private String name;
        private String version;

        // Getters and setters (nécessaires pour l'injection par Spring)

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getVersion() {
            return version;
        }

        public void setVersion(String version) {
            this.version = version;
        }
    }
    ```

    Avec `application.properties`:

    ```yaml
    app.name=My Awesome App
    app.version=1.0.0
    ```

- `@Value`: Permet d'injecter des valeurs individuelles depuis les fichiers de propriétés ou les variables d'environnement dans les champs ou les paramètres des beans.

    ```java
    package com.example.demo.service;

    import org.springframework.beans.factory.annotation.Value;
    import org.springframework.stereotype.Service;

    @Service
    public class MyService {

        @Value("${app.name}") // Injecte la valeur de la propriété 'app.name'
        private String appName;

        public void displayAppName() {
            System.out.println("Application Name: " + appName);
        }
    }
    ```

### Annotations Pour Les Composants

Ces annotations sont des spécialisations de `@Component` et indiquent à Spring qu'une classe est un bean et son rôle dans l'architecture de l'application. `@ComponentScan` recherche ces annotations par défaut.

- `@Component`: Annotation générique pour n'importe quel composant géré par Spring. C'est l'annotation de base pour les stéréotypes.

    ```java
    package com.example.demo.utils;

    import org.springframework.stereotype.Component;

    @Component // Déclare cette classe comme un bean Spring
    public class MyUtility {
        // ... utility methods
    }
    ```

- `@Service`: Spécifie qu'une classe est un service de la couche métier. Bien qu'elle soit techniquement similaire à `@Component`, elle ajoute une sémantique qui peut être utile pour la lisibilité et potentiellement pour d'autres outils ou aspects orientés.

    ```java
    package com.example.demo.service;

    import org.springframework.stereotype.Service;

    @Service // Indique que c'est un bean de service
    public class MyService {
        // ... business logic
    }
    ```

- `@Repository`: Indique qu'une classe est un dépôt de données (DAO - Data Access Object). Elle est typiquement utilisée pour les classes qui interagissent directement avec une base de données ou une autre source de données. Spring peut appliquer une traduction d'exceptions spécifiques à la base de données aux classes annotées `@Repository`.

    ```java
    package com.example.demo.repository;

    import org.springframework.stereotype.Repository;

    @Repository // Indique que c'est un bean de dépôt de données
    public class MyRepository {
        // ... data access methods
    }
    ```

- `@Controller`: Indique qu'une classe est un contrôleur de la couche présentation, gérant les requêtes web entrantes et renvoyant des vues. Utilisée typiquement dans les applications basées sur MVC (Model-View-Controller).

    ```java
    package com.example.demo.controller;

    import org.springframework.stereotype.Controller;
    import org.springframework.web.bind.annotation.GetMapping;

    @Controller // Indique que c'est un contrôleur (pour les vues)
    public class MyViewController {

        @GetMapping("/home")
        public String home() {
            return "index"; // Retourne le nom d'une vue
        }
    }
    ```

- `@RestController`: C'est une annotation de commodité qui combine `@Controller` et `@ResponseBody`. Elle est utilisée pour créer des services web RESTful, où les méthodes retournent directement des données qui seront sérialisées (par exemple en JSON) dans le corps de la réponse HTTP, plutôt que de retourner des noms de vues.

    ```java
    package com.example.demo.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController // Indique que c'est un contrôleur REST (@Controller + @ResponseBody)
    public class MyRestController {

        @GetMapping("/api/hello")
        public String hello() {
            return "Hello REST!"; // Retourne des données directement
        }
    }
    ```

### Annotations Pour L'injection De Dépendances

Ces annotations sont utilisées pour demander à Spring d'injecter automatiquement des dépendances (d'autres beans) dans les beans.

- `@Autowired`: C'est l'annotation la plus courante pour l'injection de dépendances. Elle peut être appliquée sur un constructeur, une méthode setter ou un champ. Spring résout la dépendance par type par défaut.

    ```java
    package com.example.demo.service;

    import com.example.demo.repository.MyRepository;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;

    @Service
    public class MyService {

        private final MyRepository myRepository;

        // Injection par constructeur (recommandé)
        @Autowired
        public MyService(MyRepository myRepository) {
            this.myRepository = myRepository;
        }

        // // Injection par champ (moins recommandé)
        // @Autowired
        // private MyRepository myRepository;

        // // Injection par setter (utile pour les dépendances optionnelles)
        // private MyRepository myRepository;
        // @Autowired
        // public void setMyRepository(MyRepository myRepository) {
        //     this.myRepository = myRepository;
        // }

        // ... methods using myRepository
    }
    ```

    Depuis Spring 4.3, si une classe n'a qu'un seul constructeur, `@Autowired` est optionnel sur celui-ci.

- `@Qualifier`: Utilisée avec `@Autowired`, elle permet de spécifier le nom du bean exact à injecter lorsque plusieurs beans du même type sont disponibles.

    ```java
    package com.example.demo.service;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.beans.factory.annotation.Qualifier;
    import org.springframework.stereotype.Service;

    @Service
    public class MyService {

        private final MyDataSource dataSource; // Assume MyDataSource is an interface

        @Autowired
        public MyService(@Qualifier("jdbcDataSource") MyDataSource dataSource) { // Injecte le bean nommé "jdbcDataSource"
            this.dataSource = dataSource;
        }
        // ...
    }
    ```

- `@Primary`: Utilisée sur un bean, elle indique que ce bean doit être préféré lorsqu'il y a plusieurs beans du même type et qu'aucun `@Qualifier` n'est spécifié.

    ```java
    package com.example.demo.config;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.context.annotation.Primary;

    @Configuration
    public class DataSourceConfig {

        @Bean
        @Primary // Ce bean sera injecté par défaut s'il y a plusieurs MyDataSource
        public MyDataSource jdbcDataSource() {
            return new JdbcDataSourceImpl();
        }

        @Bean
        public MyDataSource jmsDataSource() {
            return new JmsDataSourceImpl();
        }
    }
    ```

### Annotations Pour Le Web

Ces annotations sont spécifiquement utilisées dans la couche web pour mapper les requêtes HTTP aux méthodes de contrôleur et extraire les données des requêtes.

- `@RequestMapping`: Annotation polyvalente pour mapper les requêtes web à des méthodes de contrôleur. Elle peut être utilisée au niveau de la classe pour définir un chemin de base, et au niveau de la méthode pour un chemin spécifique. Elle permet de spécifier la méthode HTTP (`GET`, `POST`, etc.) et d'autres détails (paramètres, en-têtes, etc.).

    ```java
    package com.example.demo.controller;

    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    @RequestMapping("/api/articles") // Chemin de base pour toutes les méthodes dans ce contrôleur
    public class ArticleController {

        @RequestMapping(method = RequestMethod.GET, value = "/{id}") // Mappe les requêtes GET à /api/articles/{id}
        public String getArticle(@PathVariable Long id) {
            return "Article " + id;
        }
    }
    ```

    **Variantes de `@RequestMapping`** : Pour simplifier, Spring 4.3 a introduit des annotations composées spécifiques pour les méthodes HTTP :
    - `@GetMapping`
    - `@PostMapping`
    - `@PutMapping`
    - `@DeleteMapping`
    - `@PatchMapping`
    Ces annotations sont préférables car plus lisibles. L'exemple ci-dessus devient :

    ```java
    package com.example.demo.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    @RequestMapping("/api/articles")
    public class ArticleController {

        @GetMapping("/{id}") // Plus simple que @RequestMapping(method = RequestMethod.GET, value = "/{id}")
        public String getArticle(@PathVariable Long id) {
            return "Article " + id;
        }
    }
    ```

- `@RequestParam`: Permet d'extraire des paramètres de la chaîne de requête (query parameters) de l'URL.

    ```java
    package com.example.demo.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class SearchController {

        @GetMapping("/search")
        public String search(@RequestParam String query) { // Extraire le paramètre 'query' de l'URL ex: /search?query=spring
            return "Searching for: " + query;
        }

        @GetMapping("/list")
        public String list(@RequestParam(required = false, defaultValue = "1") int page) { // Paramètre optionnel avec valeur par défaut
             return "Listing page " + page;
        }
    }
    ```

- `@PathVariable`: Permet d'extraire des valeurs des variables de chemin (path variables) dans l'URL.

    ```java
    package com.example.demo.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class UserController {

        @GetMapping("/users/{userId}/orders/{orderId}") // Extrait userId et orderId du chemin
        public String getUserOrder(@PathVariable Long userId, @PathVariable Long orderId) {
            return "Fetching order " + orderId + " for user " + userId;
        }
    }
    ```

- `@RequestBody`: Indique qu'une méthode de contrôleur ou un argument de méthode doit être lié au corps de la requête HTTP. Spring utilise des convertisseurs de messages (comme Jackson pour JSON) pour désérialiser le corps de la requête en un objet Java.

    ```java
    package com.example.demo.controller;

    import com.example.demo.model.Product;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.RequestBody;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class ProductController {

        @PostMapping("/products")
        public String createProduct(@RequestBody Product product) { // Désérialise le corps JSON en objet Product
            // Save the product...
            return "Product created: " + product.getName();
        }
    }
    ```

- `@ResponseBody`: Indique que la valeur de retour d'une méthode doit être sérialisée directement dans le corps de la réponse HTTP. C'est l'annotation qui transforme `@Controller` en `@RestController`. Utilisée seule sur une méthode dans un `@Controller` (non `@RestController`), elle a le même effet que si la classe était annotée `@RestController`.

    ```java
    package com.example.demo.controller;

    import org.springframework.stereotype.Controller;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.ResponseBody;

    @Controller // Note: This is a regular @Controller
    public class DataController {

        @GetMapping("/data")
        @ResponseBody // Indicates the return value should be written directly to the body
        public String getData() {
            return "Some raw data";
        }
    }
    ```

## Bonnes Pratiques

- **Quand utiliser quelle annotation**:
    - Utilisez `@RestController` pour les API REST qui retournent des données (JSON/XML).
    - Utilisez `@Controller` pour les applications MVC qui retournent des noms de vues.
    - Utilisez les stéréotypes spécialisés (`@Service`, `@Repository`) plutôt que `@Component` lorsque c'est approprié pour ajouter de la sémantique et permettre des post-processing spécifiques à Spring (comme la traduction d'exceptions pour `@Repository`).
    - Privilégiez l'injection par constructeur (`@Autowired` sur le constructeur) pour les dépendances obligatoires.
- **Les erreurs courantes avec les annotations**:
    - Oublier d'inclure `@ComponentScan` ou s'assurer que les packages sont scannés (automatique avec `@SpringBootApplication` si les classes sont dans le bon package).
    - Avoir plusieurs beans du même type sans utiliser `@Qualifier` ou `@Primary` lors de l'injection.
    - Utiliser `@ResponseBody` sur une classe `@RestController` (redondant).
    - Confondre `@RequestParam` et `@PathVariable`.
    - Oublier `@RequestBody` pour les requêtes qui envoient des données dans le corps (POST, PUT).
- **Annotations personnalisées : concept et utilité**:
    Spring permet de créer vos propres annotations composites. Par exemple, vous pourriez créer une annotation `@MyRestController` qui combine `@RestController` et d'autres annotations spécifiques à votre projet. C'est une technique avancée pour réduire la répétition et créer des abstractions.

## Conclusion

Les annotations sont l'épine dorsale de la configuration dans Spring Boot. Elles vous permettent de déclarer des composants, de gérer les dépendances et de configurer le comportement de l'application de manière déclarative et concise.

Voici un tableau récapitulatif des annotations essentielles abordées :

| Annotation              | Catégorie                 | Rôle principal                                                              |
| :---------------------- | :------------------------ | :-------------------------------------------------------------------------- |
| `@SpringBootApplication` | Configuration             | Démarrage de l'application, active auto-configuration, scan de composants   |
| `@Configuration`        | Configuration             | Indique une classe de configuration Spring (contient des méthodes `@Bean`) |
| `@Bean`                 | Configuration             | Déclare une méthode productrice d'un bean géré par Spring                   |
| `@ConfigurationProperties`| Configuration             | Lie les propriétés externes à un bean                                       |
| `@Value`                | Configuration             | Injecte des valeurs individuelles depuis les propriétés                   |
| `@Component`            | Composants                | Annotation générique pour un bean Spring                                    |
| `@Service`              | Composants                | Stéréotype pour la couche métier                                          |
| `@Repository`           | Composants                | Stéréotype pour la couche d'accès aux données                               |
| `@Controller`           | Composants                | Stéréotype pour la couche présentation (MVC, retourne des vues)             |
| `@RestController`       | Composants                | Stéréotype pour les services web RESTful (retourne des données)           |
| `@Autowired`            | Injection de Dépendances  | Demande à Spring d'injecter une dépendance par type                         |
| `@Qualifier`            | Injection de Dépendances  | Spécifie le nom du bean à injecter (avec `@Autowired`)                     |
| `@Primary`              | Injection de Dépendances  | Indique le bean par défaut à injecter lorsqu'il y a plusieurs choix         |
| `@RequestMapping`       | Web                       | Mappe les requêtes web aux méthodes                                         |
| `@GetMapping`, etc.     | Web                       | Raccourcis pour `@RequestMapping` selon la méthode HTTP                     |
| `@RequestParam`         | Web                       | Extrait les paramètres de la chaîne de requête                              |
| `@PathVariable`         | Web                       | Extrait les variables du chemin de l'URL                                    |
| `@RequestBody`          | Web                       | Lie le corps de la requête HTTP à un objet Java                             |
| `@ResponseBody`         | Web                       | Lie la valeur de retour à un objet Java (sérialisé dans le corps de réponse) |

### Ressources Pour Approfondir

- La documentation officielle de Spring Framework et Spring Boot sur les annotations.
- Expérimentez en modifiant les annotations dans les exemples de projets.

La maîtrise de ces annotations vous donnera une base solide pour construire des applications Spring Boot. Les articles suivants les mettront en pratique dans des scénarios plus complexes, comme la création d'une API REST et l'interaction avec une base de données.

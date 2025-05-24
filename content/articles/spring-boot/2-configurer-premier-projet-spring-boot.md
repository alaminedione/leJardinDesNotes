---
title: Comment Configurer Votre Premier Projet Spring Boot En 15 Minutes
tags: spring-boot configuration projet demarrage rapide
draft: false
---

# Comment Configurer Votre Premier Projet Spring Boot En 15 Minutes

## Introduction

Bienvenue dans ce guide rapide où nous allons configurer ensemble votre tout premier projet Spring Boot et le faire fonctionner en moins de 15 minutes. Spring Boot est conçu pour rendre le développement d'applications basées sur Spring aussi simple et rapide que possible, et la création d'un nouveau projet ne fait pas exception.

**Objectif de l'article :** À la fin de ce guide, vous aurez une application Spring Boot simple mais fonctionnelle, prête à être développée davantage.

**Prérequis :** Avant de commencer, assurez-vous d'avoir les éléments suivants installés :
* **JDK (Java Development Kit) :** Version 8 ou supérieure.
* **IDE (Environnement de Développement Intégré) :** Un IDE moderne comme IntelliJ IDEA (Community ou Ultimate), Eclipse (avec Spring Tools 4), ou VS Code (avec extensions Java) est fortement recommandé.
* **Maven ou Gradle :** Bien que Spring Initializr puisse générer les fichiers de build, il est utile d'avoir l'un de ces outils installé si vous prévoyez d'exécuter l'application depuis la ligne de commande.

Prêt ? Allons-y !

## Contenu Principal

Spring Boot simplifie la création de projets grâce à un outil appelé **Spring Initializr**. C'est la méthode la plus courante et la plus rapide pour démarrer.

### Utilisation De Spring Initializr

Vous avez deux options principales pour utiliser Spring Initializr :

#### Via Le Site Web (start.spring.io)

1. Ouvrez votre navigateur et allez sur [https://start.spring.io/](https://start.spring.io/).
2. Vous verrez une interface web pour configurer votre projet. Remplissez les informations suivantes :
    * **Project :** Choisissez `Maven Project` ou `Gradle Project`. Maven est souvent un bon choix pour les débutants.
    * **Language :** Sélectionnez `Java`.
    * **Spring Boot :** Choisissez la version stable la plus récente.
    * **Project Metadata :**
        * **Group :** Un nom de package inversé comme `com.example`.
        * **Artifact :** Le nom de votre projet, par exemple `myfirstapp`.
        * **Name :** Le nom de l'application (peut être identique à Artifact).
        * **Description :** Une courte description.
        * **Package name :** Sera généré automatiquement (Group + Artifact).
        * **Packaging :** `Jar` (pour une application exécutable standalone).
        * **Java :** Choisissez la version de Java que vous utilisez (par exemple, 17 ou 21).
    * **Dependencies :** C'est ici que vous ajoutez les fonctionnalités dont votre application aura besoin. Cliquez sur le bouton "Add Dependencies…" et ajoutez :
        * `Spring Web` : Pour créer des applications web et RESTful.
        * `Spring Boot DevTools` : Utile pour le développement rapide (rechargement à chaud).
        * `Configuration Processor` : Aide à la configuration (optionnel mais recommandé).
3. Cliquez sur le bouton "Generate" (ou "Explore" pour voir la structure avant de télécharger). Un fichier `.zip` contenant votre projet sera téléchargé.
4. Extrayez le contenu du fichier `.zip` dans un répertoire de votre choix.

#### Via Votre IDE (plugin Spring)

La plupart des IDE modernes ont une intégration directe avec Spring Initializr, ce qui rend la création de projet encore plus rapide.
* **IntelliJ IDEA :** Allez dans `File -> New -> Project…`, sélectionnez `Spring Initializr` dans le menu de gauche. Configurez les mêmes options que sur le site web.
* **Eclipse :** Allez dans `File -> New -> Other…`, recherchez `Spring Boot`, et sélectionnez `Spring Starter Project`. Configurez les options nécessaires.
* **VS Code :** Installez l'extension "Spring Boot Extension Pack". Utilisez la palette de commandes (`Ctrl+Shift+P` ou `Cmd+Shift+P`) et tapez "Spring Initializr". Suivez les invites pour configurer le projet.

Une fois le projet créé via l'IDE, il sera automatiquement importé dans votre espace de travail.

### Structure Du Projet Généré

Que vous ayez téléchargé et extrait le projet ou l'ayez créé via l'IDE, la structure de base sera similaire (en utilisant Maven comme exemple) :

```
myfirstapp/
├── .mvn/        (fichiers Wrapper Maven)
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/myfirstapp/
│   │   │       └── MyfirstappApplication.java  (Classe principale)
│   │   └── resources/
│   │       ├── application.properties         (Fichier de configuration)
│   │       ├── static/                        (Pour les fichiers statiques comme JS, CSS)
│   │       └── templates/                     (Pour les templates de vue si vous utilisez un moteur)
│   └── test/
│       └── java/
│           └── com/example/myfirstapp/
│               └── MyfirstappApplicationTests.java (Classe de test)
├── .gitignore
├── mvnw                      (Script Wrapper Maven pour Linux/macOS)
├── mvnw.cmd                  (Script Wrapper Maven pour Windows)
└── pom.xml                   (Fichier de configuration Maven)
```

* `pom.xml` (ou `build.gradle` pour Gradle) : Ce fichier définit les dépendances de votre projet et comment il doit être construit.
* `src/main/java/…/MyfirstappApplication.java` : C'est la classe principale de votre application. Elle contient la méthode `main` et l'annotation `@SpringBootApplication`.

    ```articles/spring-boot/myfirstapp/src/main/java/com/example/myfirstapp/MyfirstappApplication.java
    package com.example.myfirstapp;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication
    public class MyfirstappApplication {

        public static void main(String[] args) {
            SpringApplication.run(MyfirstappApplication.class, args);
        }

    }
    ```

    L'annotation `@SpringBootApplication` est essentielle. Nous en parlerons plus en détail dans un prochain article, mais sachez qu'elle combine plusieurs annotations pour simplifier la configuration. `SpringApplication.run()` est la méthode qui lance l'application Spring Boot.
* `src/main/resources/application.properties` : C'est le fichier de configuration par défaut où vous pouvez définir des paramètres comme le port du serveur, la configuration de la base de données, etc.
* `src/test/java/…/MyfirstappApplicationTests.java` : Un exemple de classe de test fournie par défaut.

### Créer Un Premier Contrôleur Simple

Maintenant, ajoutons un peu de code pour que notre application fasse quelque chose d'utile : répondre à une requête HTTP. Nous allons créer un simple contrôleur REST.

1. Dans le dossier `src/main/java/com/example/myfirstapp/`, créez un nouveau package (dossier) appelé `controller`.
2. Dans ce nouveau package `controller`, créez une nouvelle classe Java appelée `HelloWorldController.java`.
3. Ajoutez le code suivant à cette classe :

```articles/spring-boot/myfirstapp/src/main/java/com/example/myfirstapp/controller/HelloWorldController.java
package com.example.myfirstapp.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Bonjour, Monde de Spring Boot!";
    }
}
```

* L'annotation `@RestController` indique à Spring que cette classe est un contrôleur et que ses méthodes doivent retourner directement des données (et non le nom d'une vue).
* L'annotation `@GetMapping("/hello")` mappe la méthode `sayHello()` aux requêtes HTTP GET sur le chemin `/hello`.

Félicitations ! Vous avez écrit votre premier contrôleur Spring Boot.

## Test Et Exécution

Il est temps de voir notre application en action.

### Exécuter L'application Depuis l'IDE

C'est la méthode la plus simple pendant le développement. Dans votre IDE, localisez la classe principale `MyfirstappApplication.java`. Faites un clic droit dessus et sélectionnez "Run 'MyfirstappApplication.main()'" (ou une option similaire). L'IDE lancera l'application. Vous devriez voir les logs de démarrage dans la console, indiquant que Spring Boot démarre et que le serveur Tomcat intégré écoute sur le port 8080 par défaut.

### Exécuter Avec Maven/Gradle

Vous pouvez également exécuter l'application depuis la ligne de commande en utilisant le wrapper Maven ou Gradle qui a été généré avec le projet :

* **Avec Maven :** Ouvrez un terminal dans le répertoire racine de votre projet (`myfirstapp`) et exécutez :

    ```bash
    ./mvnw spring-boot:run
    ```

    (Utilisez `mvnw.cmd spring-boot:run` sous Windows)

* **Avec Gradle :** Ouvrez un terminal dans le répertoire racine de votre projet et exécutez :

    ```bash
    ./gradlew bootRun
    ```

    (Utilisez `gradlew.bat bootRun` sous Windows)

Ces commandes compileront (si nécessaire) et exécuteront votre application Spring Boot.

### Accéder à l'API via Le Navigateur

Une fois que l'application est lancée (peu importe la méthode), ouvrez votre navigateur et allez à l'adresse `http://localhost:8080/hello`.

Vous devriez voir le texte "Bonjour, Monde de Spring Boot!" affiché dans votre navigateur. Votre application Spring Boot répond !

### Hot-reload Avec DevTools

Si vous avez inclus la dépendance `Spring Boot DevTools`, essayez de modifier le message retourné par la méthode `sayHello()` dans `HelloWorldController.java` et sauvegardez le fichier. Vous devriez voir dans les logs de l'application qu'un rechargement a été déclenché. Actualisez la page `http://localhost:8080/hello` dans votre navigateur, et vous devriez voir votre message mis à jour sans avoir eu besoin de redémarrer l'application manuellement. C'est très pratique pendant le développement !

## Conclusion

Félicitations ! Vous venez de configurer et d'exécuter votre premier projet Spring Boot en partant de zéro. En utilisant Spring Initializr et en ajoutant juste quelques lignes de code, nous avons créé une application web fonctionnelle.

**Récapitulatif des étapes clés :**
1. Utilisation de Spring Initializr pour générer la structure de base avec les dépendances nécessaires.
2. Compréhension rapide de la structure du projet généré.
3. Création d'un simple contrôleur REST pour traiter une requête HTTP.
4. Exécution de l'application et test via le navigateur.

Vous êtes maintenant prêt à explorer plus en profondeur les capacités de Spring Boot.

**Ressources pour aller plus loin :**
* Explorez le fichier `application.properties` pour voir les options de configuration disponibles.
* Modifiez le chemin `/hello` dans l'annotation `@GetMapping` pour voir l'effet.
* Essayez d'ajouter une autre méthode avec une annotation `@GetMapping` différente dans le même contrôleur.

Dans les prochains articles, nous plongerons dans les annotations essentielles, la création d'API REST plus complexes, l'interaction avec les bases de données, et bien plus encore. Restez à l'écoute !

# Spring Boot Actuator : Surveillez votre application en production

## Introduction

Lorsque vous déployez une application en production, il est crucial de pouvoir la surveiller activement. Cela implique de connaître son état de santé, de suivre ses performances, de comprendre son comportement et d'identifier rapidement les problèmes. C'est là que les métriques applicatives et les outils de monitoring entrent en jeu.

Spring Boot Actuator est un sous-projet du framework Spring Boot qui fournit des fonctionnalités de production pour vos applications. Il vous permet de surveiller et de gérer votre application en production sans avoir à écrire beaucoup de code. Il offre un ensemble d'endpoints prêts à l'emploi pour obtenir des informations précieuses sur l'état de votre application.

Dans cet article, nous allons explorer ce qu'est Spring Boot Actuator, comment l'ajouter à votre projet et comment utiliser ses principaux endpoints pour surveiller votre application.

## Contenu principal

### Configuration de base

Pour ajouter Spring Boot Actuator à votre projet, il vous suffit d'ajouter la dépendance `spring-boot-starter-actuator` à votre fichier de build Maven ou Gradle.

Avec Maven, ajoutez ceci à votre `pom.xml` :

```/dev/null/pom.xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Avec Gradle, ajoutez ceci à votre `build.gradle` :

```/dev/null/build.gradle
implementation 'org.springframework.boot:spring-boot-starter-actuator'
```

Une fois la dépendance ajoutée, Actuator est automatiquement configuré. Par défaut, Actuator expose un certain nombre d'endpoints (comme `/health` et `/info`) sur un port HTTP séparé (le port 8080 par défaut, le même que l'application, sauf si configuré autrement) sous le chemin `/actuator`.

Vous pouvez configurer Actuator dans votre fichier `application.properties` ou `application.yml`. Par exemple, pour exposer tous les endpoints via l'interface web (car certains ne sont pas exposés par défaut pour des raisons de sécurité), vous pouvez ajouter :

```/dev/null/application.properties
management.endpoints.web.exposure.include=*
```

Il est crucial de sécuriser ces endpoints en production, car ils peuvent exposer des informations sensibles. Spring Security s'intègre très bien avec Actuator pour cela (voir article 7).

### Endpoints disponibles

Actuator fournit de nombreux endpoints prêts à l'emploi. Voici quelques-uns des plus couramment utilisés :

-   `/actuator/health` : Fournit des informations de base sur l'état de santé de l'application (UP, DOWN, etc.). Il peut être étendu pour vérifier l'état de la base de données, des services externes, etc.
-   `/actuator/info` : Affiche des informations arbitraires sur l'application. Vous pouvez configurer ces informations dans `application.properties` (par exemple, version de l'application, nom).
-   `/actuator/metrics` : Fournit des informations sur les métriques de l'application (mémoire utilisée, threads actifs, temps de réponse HTTP, etc.). Vous pouvez voir toutes les métriques disponibles en accédant à `/actuator/metrics`, puis une métrique spécifique via `/actuator/metrics/{nom_metrique}`.
-   `/actuator/env` : Affiche les variables d'environnement, les propriétés de configuration, etc. **Cet endpoint doit être sécurisé en production.**
-   `/actuator/loggers` : Permet de visualiser et de configurer le niveau de log des loggers de l'application à la volée. **Cet endpoint doit être sécurisé en production.**
-   `/actuator/beans` : Liste tous les beans Spring créés dans votre `ApplicationContext`. **Cet endpoint doit être sécurisé en production.**
-   `/actuator/mappings` : Affiche une liste de tous les mappings `@RequestMapping`.

### Personnalisation

Vous pouvez personnaliser le comportement d'Actuator :

-   **Activation/désactivation d'endpoints** : Utilisez `management.endpoints.web.exposure.include` et `management.endpoints.web.exposure.exclude` dans `application.properties` pour spécifier quels endpoints exposer via le web.
-   **Sécurisation des endpoints** : Si vous utilisez Spring Security, Actuator sécurise automatiquement les endpoints par défaut. Vous pouvez configurer des règles d'accès spécifiques.
-   **Création d'indicateurs personnalisés** : Vous pouvez créer vos propres indicateurs de santé en implémentant l'interface `HealthIndicator` et les enregistrer en tant que beans Spring. Vous pouvez également créer des métriques personnalisées en utilisant l'API `MeterRegistry` de Micrometer.

### Intégration avec des outils de monitoring

Bien qu'Actuator expose des métriques, il n'est pas un système de monitoring complet en soi. Il est conçu pour s'intégrer avec des systèmes de monitoring externes. Micrometer, qui est inclus par défaut dans Spring Boot Actuator depuis la version 2.0, fournit une façade de mesure pour vos métriques. Actuator expose ces métriques dans des formats compréhensibles par divers systèmes de monitoring.

Quelques intégrations courantes incluent :

-   **Prometheus** : Un système de monitoring et d'alerte populaire. Actuator expose un endpoint `/actuator/prometheus` que Prometheus peut scrapper.
-   **Grafana** : Une plateforme d'analyse et de visualisation. Grafana peut se connecter à Prometheus (ou d'autres sources de données) pour créer des dashboards basés sur les métriques fournies par Actuator.
-   **Autres** : Micrometer supporte de nombreux autres systèmes comme Datadog, New Relic, etc.

## En pratique

Pour voir Actuator en action, ajoutez la dépendance à un projet Spring Boot simple. Démarrez l'application et accédez à `http://localhost:8080/actuator`. Vous devriez voir la liste des endpoints exposés (si vous avez inclus tous les endpoints via la configuration).

Naviguez vers `http://localhost:8080/actuator/health` pour voir l'état de santé.
Naviguez vers `http://localhost:8080/actuator/info` (si vous avez configuré des informations dans `application.properties`, sinon ce sera vide par défaut).
Naviguez vers `http://localhost:8080/actuator/metrics` pour voir les métriques disponibles, puis `http://localhost:8080/actuator/metrics/jvm.memory.used` par exemple, pour voir la métrique spécifique d'utilisation mémoire.

La configuration d'un dashboard simple avec Prometheus et Grafana impliquerait :
1.  Configurer Actuator pour exposer l'endpoint Prometheus (`management.endpoints.web.exposure.include=health,info,prometheus`).
2.  Installer et configurer Prometheus pour qu'il scrape l'endpoint `/actuator/prometheus` de votre application.
3.  Installer et configurer Grafana, en ajoutant Prometheus comme source de données.
4.  Créer des dashboards dans Grafana en utilisant les métriques de votre application disponibles dans Prometheus.

Les alertes peuvent être configurées dans Prometheus ou Grafana, basées sur des seuils définis pour vos métriques (par exemple, alerter si l'utilisation du CPU dépasse 80% pendant 5 minutes).

## Conclusion

Spring Boot Actuator est un outil indispensable pour gérer et surveiller vos applications Spring Boot en production. Il vous fournit un accès rapide à des informations essentielles sur l'état, les métriques, l'environnement et bien plus encore.

En l'intégrant avec des systèmes de monitoring comme Prometheus et Grafana via Micrometer, vous pouvez mettre en place une solution de surveillance robuste pour vos applications, vous permettant d'identifier les problèmes avant qu'ils n'affectent vos utilisateurs et d'assurer le bon fonctionnement de votre système.

Il est essentiel de se rappeler l'importance de sécuriser les endpoints Actuator, surtout en production, car ils exposent des informations potentiellement sensibles.

Au-delà d'Actuator, l'écosystème de monitoring Spring Boot est riche, avec des intégrations pour le tracing distribué (Spring Cloud Sleuth/Micrometer Tracing) et d'autres outils d'observabilité. La compréhension d'Actuator est la première étape clé pour une bonne gestion de vos applications en production.
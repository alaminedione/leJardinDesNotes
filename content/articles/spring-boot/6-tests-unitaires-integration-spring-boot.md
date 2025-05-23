# Les tests unitaires et d'intégration avec Spring Boot

## Introduction

Les tests automatisés sont une pierre angulaire du développement logiciel moderne. Ils permettent de garantir la qualité du code, de faciliter les refactorings et de s'assurer que les nouvelles fonctionnalités n'introduisent pas de régressions. Pour les applications Spring Boot, l'écriture de tests est particulièrement aisée grâce à l'écosystème riche et aux outils dédiés fournis par le framework. Cet article vous guidera à travers les concepts fondamentaux des tests unitaires et d'intégration dans Spring Boot.

- **Importance des tests automatisés**
  Les tests automatisés fournissent une assurance continue que votre application fonctionne comme prévu. Ils détectent rapidement les erreurs, réduisent les coûts de maintenance et augmentent la confiance dans le code que vous écrivez.

- **Comment Spring Boot facilite l'écriture de tests**
  Spring Boot offre une excellente intégration avec des frameworks de test comme JUnit et Mockito. Il fournit également des annotations et des utilitaires spécifiques pour configurer facilement des contextes de test pour les tests d'intégration, rendant le test de diverses couches de votre application simple et efficace.

## Contenu principal

### Configuration de l'environnement de test

Pour commencer à tester votre application Spring Boot, vous aurez besoin d'ajouter les dépendances de test appropriées à votre projet.

- **Dépendances nécessaires (JUnit, Mockito, etc.)**
  Lorsque vous créez un projet Spring Boot via Spring Initializr, la dépendance `spring-boot-starter-test` est généralement incluse par défaut. Cette dépendance apporte JUnit 5, Mockito, AssertJ, Hamcrest, et d'autres bibliothèques de test courantes.

  ```/dev/null/pom.xml#L1-5
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
  </dependency>
  ```

- **@SpringBootTest vs tests slice**
  - `@SpringBootTest`: Charge le contexte d'application Spring Boot complet. Utile pour les tests d'intégration où vous testez plusieurs couches ensemble. Cela peut être plus lent car cela démarre une grande partie de l'application.
  - Tests slice (ex: `@WebMvcTest`, `@DataJpaTest`): Chargent une partie spécifique du contexte Spring (par exemple, uniquement la couche web ou la couche JPA). Ils sont plus rapides et adaptés aux tests d'intégration ciblant une seule couche.

### Tests unitaires

Les tests unitaires visent à tester de petites unités de code isolément, généralement une méthode ou une classe, en mockant leurs dépendances.

- **Principes et organisation**
  Les tests unitaires doivent être rapides, isolés et se concentrer sur la logique métier d'une seule unité. Ils se placent généralement dans le répertoire `src/test/java`.

- **Mockito pour les mocks**
  Mockito est un framework de mocking populaire utilisé pour créer des objets fictifs (mocks) pour les dépendances. Cela permet de tester l'unité de code en isolation sans dépendre de ses collaborateurs réels.

  ```/dev/null/SomeServiceTest.java#L1-10
  import org.junit.jupiter.api.Test;
  import org.mockito.Mockito;

  // ... imports for the class being tested ...

  class SomeServiceTest {

      @Test
      void testMethod() {
          // Create a mock dependency
          Dependency mockDependency = Mockito.mock(Dependency.class);
          // ... rest of the test ...
      }
  }
  ```

- **Tester des services et composants**
  Vous pouvez tester des services ou d'autres composants Spring en instanciant la classe directement et en injectant des mocks pour ses dépendances.

### Tests d'intégration

Les tests d'intégration vérifient que différentes parties de votre application fonctionnent correctement ensemble. Spring Boot fournit des outils pour simplifier la configuration de ces tests.

- **@SpringBootTest pour les tests complets**
  Cette annotation charge le contexte complet de l'application et est utilisée pour tester des scénarios de bout en bout ou des interactions complexes entre composants.

  ```/dev/null/FullIntegrationTest.java#L1-5
  import org.springframework.boot.test.context.SpringBootTest;
  import org.junit.jupiter.api.Test;

  @SpringBootTest
  class FullIntegrationTest {
      // ... test methods ...
  }
  ```

- **TestRestTemplate pour tester les API REST**
  `TestRestTemplate` est un utilitaire fourni par Spring Boot pour effectuer facilement des appels HTTP dans vos tests d'intégration, simulant un client REST.

  ```/dev/null/ApiTest.java#L1-10
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.boot.test.context.SpringBootTest;
  import org.springframework.boot.test.web.client.TestRestTemplate;
  import org.junit.jupiter.api.Test;

  @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
  class ApiTest {

      @Autowired
      private TestRestTemplate restTemplate;

      @Test
      void testEndpoint() {
          // Use restTemplate to make HTTP calls
      }
  }
  ```

- **Tests avec base de données (TestContainers)**
  Pour tester l'interaction avec une base de données réelle, vous pouvez utiliser TestContainers, qui permet de démarrer des conteneurs Docker pour des bases de données dans vos tests.

### Tests spécifiques

Spring Boot offre des annotations spécialisées pour tester des couches spécifiques de votre application de manière isolée (tests slice).

- **Tests des contrôleurs avec MockMvc**
  `@WebMvcTest` permet de tester la couche web Spring MVC sans démarrer le serveur HTTP complet. `MockMvc` est utilisé pour simuler des requêtes HTTP.

  ```/dev/null/WebLayerTest.java#L1-10
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
  import org.springframework.test.web.servlet.MockMvc;
  import org.junit.jupiter.api.Test;

  @WebMvcTest(MyController.class)
  class WebLayerTest {

      @Autowired
      private MockMvc mockMvc;

      @Test
      void testControllerEndpoint() throws Exception {
          // Use mockMvc to perform requests
      }
  }
  ```

- **Tests des repositories avec @DataJpaTest**
  `@DataJpaTest` configure un environnement de test pour tester la couche Spring Data JPA. Il configure une base de données embarquée par défaut et est transactionnel par test.

  ```/dev/null/JpaLayerTest.java#L1-10
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
  import org.junit.jupiter.api.Test;

  @DataJpaTest
  class JpaLayerTest {

      @Autowired
      private MyRepository repository;

      @Test
      void testRepository() {
          // Use repository to interact with the database
      }
  }
  ```

- **Tests des services avec @MockBean**
  Dans les tests slice ou `@SpringBootTest`, `@MockBean` permet de remplacer un bean existant dans le contexte Spring par un mock Mockito. Utile pour isoler la couche testée des dépendances externes.

  ```/dev/null/ServiceTest.java#L1-10
  import org.springframework.boot.test.context.SpringBootTest; // or @WebMvcTest, etc.
  import org.springframework.boot.test.mock.mockito.MockBean;
  import org.junit.jupiter.api.Test;
  import org.mockito.Mockito;

  // Assume MyService depends on ExternalService
  class MyServiceTest {

      @MockBean
      private ExternalService externalService;

      // Assume MyService is injected or tested directly
      // ... test methods using MyService and verify externalService calls ...
  }
  ```

## Bonnes pratiques

- **Isolation des tests**
  Assurez-vous que chaque test est indépendant des autres. Les tests d'intégration avec base de données devraient être transactionnels pour revenir à un état propre après chaque test.

- **Données de test (TestConfiguration, @SQL)**
  Utilisez `@TestConfiguration` pour définir des beans spécifiques aux tests ou `@SQL` pour exécuter des scripts SQL avant ou après les méthodes de test afin de configurer l'état initial de la base de données.

- **Profils de test**
  Utilisez les profils Spring (`@ActiveProfiles`) pour activer des configurations spécifiques aux tests (par exemple, utiliser une base de données en mémoire pour les tests d'intégration).

## Conclusion

Spring Boot fournit un environnement robuste et convivial pour écrire des tests unitaires et d'intégration. En utilisant `@SpringBootTest` pour les tests d'intégration complets, les tests slice pour les couches spécifiques, et des outils comme Mockito et TestRestTemplate, vous pouvez couvrir efficacement différentes parties de votre application.

- **Indicateurs de qualité des tests**
  La couverture de code (code coverage) est un indicateur important, mais assurez-vous de tester les scénarios critiques et les cas limites, pas seulement d'atteindre un pourcentage élevé.

- **Automatisation des tests dans un pipeline CI/CD**
  Intégrez l'exécution de vos tests automatisés dans votre pipeline d'intégration continue/déploiement continu (CI/CD) pour garantir que chaque changement de code est validé avant le déploiement.
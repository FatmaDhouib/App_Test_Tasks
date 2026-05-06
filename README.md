# Exercices pratiques — Tests d'applications Java Spring Boot

Ce dépôt regroupe une série d'exercices pratiques pour apprendre à tester une application Spring Boot à différents niveaux : tests unitaires, mocks, repository, contrôleur REST, intégration, performance et sécurité.

## Objectifs pédagogiques

- Écrire des tests unitaires avec JUnit 5 et AssertJ.
- Isoler les dépendances avec Mockito.
- Tester la couche persistance avec `@DataJpaTest`.
- Tester les contrôleurs REST avec `@WebMvcTest` et `MockMvc`.
- Réaliser des tests E2E avec Testcontainers et PostgreSQL.
- Concevoir un scénario de charge avec Gatling.
- Lancer des analyses de sécurité SAST et DAST avec OWASP Dependency-Check, SpotBugs et ZAP.

## Contenu

### Exercice 1 — Tests unitaires avec JUnit 5 et TDD
- Tester `ReservationService`.
- Appliquer le cycle TDD : Red → Green → Refactor.
- Vérifier :
  - le calcul du prix total,
  - la disponibilité d’une chambre,
  - le format d’un code de confirmation.

### Exercice 2 — Isolation avec Mockito
- Tester `FacturationService`.
- Utiliser `@Mock`, `@InjectMocks`, `when().thenReturn()` et `verify()`.
- Gérer un cas nominal et un cas d’erreur.

### Exercice 3 — Tests de repository avec `@DataJpaTest`
- Tester `EmployeRepository`.
- Utiliser H2 en mémoire.
- Vérifier les requêtes :
  - `findByDepartement`
  - `findBySalaireSuperieurA`

### Exercice 4 — Tests de contrôleur REST avec MockMvc
- Tester `EmployeController`.
- Utiliser `@WebMvcTest`.
- Vérifier :
  - le statut HTTP,
  - le JSON retourné,
  - la validation Bean avec `@Valid`.

### Exercice 5 — Tests E2E et Testcontainers
- Tester le flux complet HTTP → service → base de données.
- Utiliser PostgreSQL via Testcontainers.
- Vérifier :
  - création et récupération d’un employé,
  - suppression et contrôle du 404.

### Exercice 6 — Tests de performance avec Gatling
- Écrire une simulation de charge.
- Définir des SLOs avant exécution.
- Analyser les métriques :
  - temps de réponse moyen,
  - 95e percentile,
  - débit,
  - taux d’erreur.

### Exercice 7 — Sécurité : SAST et DAST
- Lancer OWASP Dependency-Check.
- Lancer SpotBugs avec Find Security Bugs.
- Scanner l’application avec OWASP ZAP.
- Comparer SAST et DAST.

## Technologies utilisées

- Java
- Spring Boot
- JUnit 5
- AssertJ
- Mockito
- Spring Data JPA
- H2
- MockMvc
- Testcontainers
- PostgreSQL
- Gatling
- OWASP Dependency-Check
- SpotBugs
- OWASP ZAP

## Prérequis

- Java 17 ou supérieur.
- Maven.
- Docker pour les tests avec Testcontainers et ZAP.
- IntelliJ IDEA recommandé pour exécuter les tests avec couverture.

## Lancement des tests

```bash
./mvnw test
```

## Tests avec couverture

Dans IntelliJ IDEA :
- Ouvrir la classe de test.
- Cliquer sur **Run with Coverage**.
- Vérifier que `ReservationService` atteint au moins 80 % de couverture.

## Exécution des tests E2E

```bash
./mvnw test
```

Vérifier que Docker est démarré avant de lancer les tests Testcontainers.

## Exécution Gatling

Démarrer l’application :

```bash
./mvnw spring-boot:run
```

Puis lancer le test de charge :

```bash
./mvnw gatling:test
```

## Analyse de sécurité

### Dependency-Check
```bash
./mvnw dependency-check:check
```

### SpotBugs
```bash
./mvnw spotbugs:check
```

### OWASP ZAP
```bash
docker run --rm \
  --network host \
  -v $(pwd):/zap/wrk \
  ghcr.io/zaproxy/zaproxy:stable \
  zap-baseline.py \
  -t http://localhost:8080 \
  -r zap-report.html
```

## Structure attendue du projet

```text
src/
├── main/
│   └── java/
│       └── ...
└── test/
    └── java/
        ├── ReservationServiceTest.java
        ├── FacturationServiceTest.java
        ├── EmployeRepositoryTest.java
        ├── EmployeControllerTest.java
        ├── EmployeApiE2ETest.java
        └── EmployeSimulation.java
```

## Consignes générales

- Chaque test doit couvrir un seul cas.
- Les noms de méthode doivent être explicites.
- Les assertions doivent être lisibles et expressives.
- Les tests doivent être isolés les uns des autres.
- Les dépendances externes doivent être simulées quand cela est nécessaire.

## Formateur

Wahid Hamdi
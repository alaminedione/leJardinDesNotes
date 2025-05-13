---
title: SQL
draft: false
tags:
  - sql
  - database
description: Langage standard pour la gestion et la manipulation des bases de données relationnelles.
---

## Sommaire

1.  Introduction à SQL
    *   Qu'est-ce que SQL ?
    *   Systèmes de gestion de bases de données relationnelles (SGBDR)
    *   Types de commandes SQL (DDL, DML, DCL, TCL)
2.  Bases de Données Relationnelles
    *   Concepts (Tables, Colonnes, Lignes, Clés primaires, Clés étrangères)
    *   Relations entre tables
    *   Normalisation
3.  Requêtes de Sélection (SELECT)
    *   Sélectionner des colonnes et toutes les colonnes
    *   Filtrage (WHERE)
    *   Tri (ORDER BY)
    *   Limitation des résultats (LIMIT, TOP)
4.  Jointures (JOIN)
    *   INNER JOIN
    *   LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN
    *   Self Join
5.  Agrégation et Groupement
    *   Fonctions d'agrégation (COUNT, SUM, AVG, MIN, MAX)
    *   Groupement (GROUP BY)
    *   Filtrage des groupes (HAVING)
6.  Modification des Données (INSERT, UPDATE, DELETE)
    *   Insertion de nouvelles lignes
    *   Mise à jour de lignes existantes
    *   Suppression de lignes
7.  Création et Modification de Structures (DDL)
    *   Création de tables (CREATE TABLE)
    *   Modification de tables (ALTER TABLE)
    *   Suppression de tables (DROP TABLE)
    *   Création d'index (CREATE INDEX)
8.  Contraintes
    *   NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT
9.  Transactions
    *   ACID properties
    *   BEGIN, COMMIT, ROLLBACK
10. Vues
    *   Création et utilisation des vues
11. Sous-requêtes
    *   Sous-requêtes dans WHERE, FROM, SELECT
12. Fonctions et Procédures Stockées
    *   Création et exécution
13. Bonnes Pratiques
    *   Optimisation des requêtes
    *   Sécurité
14. Ressources et Communauté
    *   Documentation spécifique au SGBDR
    *   Communautés en ligne
## 1. Introduction à SQL

### Qu'est-ce que SQL ?

SQL (Structured Query Language) est un langage standard pour la gestion et la manipulation des bases de données relationnelles. Il permet de créer, de modifier, de supprimer et d'interroger des données stockées dans des tables.

### Systèmes de gestion de bases de données relationnelles (SGBDR)

*   MySQL
*   PostgreSQL
*   Oracle
*   Microsoft SQL Server
*   SQLite

### Types de commandes SQL (DDL, DML, DCL, TCL)

*   **DDL (Data Definition Language)** : Commandes pour définir la structure de la base de données (ex: `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`).
*   **DML (Data Manipulation Language)** : Commandes pour manipuler les données (ex: `SELECT`, `INSERT`, `UPDATE`, `DELETE`).
*   **DCL (Data Control Language)** : Commandes pour contrôler l'accès aux données (ex: `GRANT`, `REVOKE`).
*   **TCL (Transaction Control Language)** : Commandes pour gérer les transactions (ex: `BEGIN`, `COMMIT`, `ROLLBACK`).

## 2. Bases de Données Relationnelles

### Concepts (Tables, Colonnes, Lignes, Clés primaires, Clés étrangères)

*   **Table** : Ensemble de données organisées en lignes et en colonnes.
*   **Colonne** : Attribut d'une table (ex: nom, âge, adresse).
*   **Ligne** : Enregistrement d'une table (ensemble de valeurs pour chaque colonne).
*   **Clé primaire** : Colonne (ou ensemble de colonnes) identifiant de manière unique chaque ligne d'une table.
*   **Clé étrangère** : Colonne d'une table qui référence la clé primaire d'une autre table (permet d'établir des relations entre les tables).

### Relations entre tables

*   **Un-à-un (1:1)** : Chaque ligne d'une table est associée à une seule ligne d'une autre table.
*   **Un-à-plusieurs (1:N)** : Chaque ligne d'une table est associée à plusieurs lignes d'une autre table.
*   **Plusieurs-à-plusieurs (N:N)** : Plusieurs lignes d'une table sont associées à plusieurs lignes d'une autre table (nécessite une table de jointure).

### Normalisation

*   Processus de conception d'une base de données pour réduire la redondance des données et améliorer l'intégrité.
*   Formes normales (1NF, 2NF, 3NF, BCNF, etc.).
## 3. Requêtes de Sélection (SELECT)

### Sélectionner des colonnes et toutes les colonnes

*   `SELECT colonne1, colonne2 FROM table` : Sélectionne les colonnes spécifiées.
*   `SELECT * FROM table` : Sélectionne toutes les colonnes.

```sql
SELECT nom, age FROM personnes;
SELECT * FROM personnes;
```

### Filtrage (WHERE)

*   `WHERE condition` : Filtre les lignes en fonction d'une condition.

```sql
SELECT * FROM personnes WHERE age > 30;
SELECT nom FROM produits WHERE prix < 100 AND categorie = 'Electronique';
```

### Tri (ORDER BY)

*   `ORDER BY colonne ASC|DESC` : Trie les résultats par la colonne spécifiée (ASC pour croissant, DESC pour décroissant).

```sql
SELECT * FROM personnes ORDER BY nom ASC;
SELECT * FROM produits ORDER BY prix DESC;
```

### Limitation des résultats (LIMIT, TOP)

*   `LIMIT nombre` (MySQL, PostgreSQL) : Limite le nombre de résultats.
*   `TOP nombre` (SQL Server) : Limite le nombre de résultats.

```sql
SELECT * FROM personnes LIMIT 10;
SELECT TOP 10 * FROM personnes;
```
## 4. Jointures (JOIN)

### INNER JOIN

*   Retourne les lignes qui ont une correspondance dans les deux tables.

```sql
SELECT * FROM commandes
INNER JOIN clients ON commandes.client_id = clients.id;
```

### LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN

*   `LEFT JOIN` : Retourne toutes les lignes de la table de gauche et les lignes correspondantes de la table de droite (si elles existent).
*   `RIGHT JOIN` : Retourne toutes les lignes de la table de droite et les lignes correspondantes de la table de gauche (si elles existent).
*   `FULL OUTER JOIN` : Retourne toutes les lignes des deux tables (pas supporté par tous les SGBDR).

```sql
SELECT * FROM commandes
LEFT JOIN clients ON commandes.client_id = clients.id;

SELECT * FROM commandes
RIGHT JOIN clients ON commandes.client_id = clients.id;

-- FULL OUTER JOIN (peut nécessiter une syntaxe spécifique selon le SGBDR)
```

### Self Join

*   Jointure d'une table avec elle-même (utile pour comparer des lignes de la même table).

```sql
SELECT e1.nom, e2.nom AS responsable
FROM employes e1
INNER JOIN employes e2 ON e1.responsable_id = e2.id;
```
## 5. Agrégation et Groupement

### Fonctions d'agrégation (COUNT, SUM, AVG, MIN, MAX)

*   `COUNT()` : Retourne le nombre de lignes.
*   `SUM()` : Retourne la somme des valeurs.
*   `AVG()` : Retourne la moyenne des valeurs.
*   `MIN()` : Retourne la valeur minimale.
*   `MAX()` : Retourne la valeur maximale.

```sql
SELECT COUNT(*) FROM personnes;
SELECT SUM(prix) FROM produits;
SELECT AVG(age) FROM personnes;
SELECT MIN(prix) FROM produits;
SELECT MAX(prix) FROM produits;
```

### Groupement (GROUP BY)

*   `GROUP BY colonne` : Regroupe les lignes ayant la même valeur dans la colonne spécifiée.

```sql
SELECT categorie, COUNT(*) FROM produits GROUP BY categorie;
```

### Filtrage des groupes (HAVING)

*   `HAVING condition` : Filtre les groupes en fonction d'une condition (utilisé après `GROUP BY`).

```sql
SELECT categorie, COUNT(*) FROM produits GROUP BY categorie HAVING COUNT(*) > 10;
```
## 6. Modification des Données (INSERT, UPDATE, DELETE)

### Insertion de nouvelles lignes

*   `INSERT INTO table (colonne1, colonne2, ...) VALUES (valeur1, valeur2, ...)` : Insère une nouvelle ligne dans la table.

```sql
INSERT INTO personnes (nom, age) VALUES ('John', 30);
```

### Mise à jour de lignes existantes

*   `UPDATE table SET colonne1 = valeur1, colonne2 = valeur2, ... WHERE condition` : Met à jour les lignes qui correspondent à la condition.

```sql
UPDATE personnes SET age = 31 WHERE nom = 'John';
```

### Suppression de lignes

*   `DELETE FROM table WHERE condition` : Supprime les lignes qui correspondent à la condition.

```sql
DELETE FROM personnes WHERE nom = 'John';
```
## 7. Création et Modification de Structures (DDL)

### Création de tables (CREATE TABLE)

*   `CREATE TABLE table (colonne1 type contraintes, colonne2 type contraintes, ...)` : Crée une nouvelle table.

```sql
CREATE TABLE personnes (
    id INT PRIMARY KEY,
    nom VARCHAR(255) NOT NULL,
    age INT
);
```

### Modification de tables (ALTER TABLE)

*   `ALTER TABLE table ADD colonne type contraintes` : Ajoute une colonne à une table.
*   `ALTER TABLE table DROP COLUMN colonne` : Supprime une colonne d'une table.
*   `ALTER TABLE table MODIFY COLUMN colonne type contraintes` : Modifie le type ou les contraintes d'une colonne.

```sql
ALTER TABLE personnes ADD email VARCHAR(255);
ALTER TABLE personnes DROP COLUMN age;
ALTER TABLE personnes MODIFY COLUMN nom VARCHAR(100) NOT NULL;
```

### Suppression de tables (DROP TABLE)

*   `DROP TABLE table` : Supprime une table.

```sql
DROP TABLE personnes;
```

### Création d'index (CREATE INDEX)

*   `CREATE INDEX index_nom ON table (colonne)` : Crée un index sur une colonne pour accélérer les requêtes.

```sql
CREATE INDEX nom_index ON personnes (nom);
```
## 8. Contraintes

### NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT

*   `NOT NULL` : Empêche l'insertion de valeurs NULL dans une colonne.
*   `UNIQUE` : Empêche l'insertion de valeurs dupliquées dans une colonne.
*   `PRIMARY KEY` : Identifie de manière unique chaque ligne d'une table.
*   `FOREIGN KEY` : Établit une relation entre deux tables.
*   `CHECK` : Vérifie qu'une valeur respecte une condition.
*   `DEFAULT` : Définit une valeur par défaut pour une colonne.

```sql
CREATE TABLE personnes (
    id INT PRIMARY KEY,
    nom VARCHAR(255) NOT NULL,
    age INT CHECK (age > 0),
    ville VARCHAR(255) DEFAULT 'Inconnu'
);

CREATE TABLE commandes (
    id INT PRIMARY KEY,
    client_id INT,
    FOREIGN KEY (client_id) REFERENCES clients(id)
);
```
## 9. Transactions

### ACID properties

*   **Atomicity** : La transaction est traitée comme une seule unité de travail (tout ou rien).
*   **Consistency** : La transaction doit maintenir l'intégrité de la base de données (passage d'un état valide à un autre).
*   **Isolation** : Les transactions concurrentes doivent être isolées les unes des autres (pas d'interférence).
*   **Durability** : Une fois la transaction validée, les modifications sont permanentes.

### BEGIN, COMMIT, ROLLBACK

*   `BEGIN` : Démarre une transaction.
*   `COMMIT` : Valide les modifications de la transaction.
*   `ROLLBACK` : Annule les modifications de la transaction.

```sql
BEGIN;

UPDATE comptes SET solde = solde - 100 WHERE id = 1;
UPDATE comptes SET solde = solde + 100 WHERE id = 2;

COMMIT; -- ou ROLLBACK;
```
## 10. Vues

### Création et utilisation des vues

*   Une vue est une requête SELECT stockée comme un objet de base de données.
*   Elle permet de simplifier les requêtes complexes et de masquer la complexité de la structure de la base de données.

```sql
CREATE VIEW clients_actifs AS
SELECT id, nom, email FROM clients WHERE actif = 1;

SELECT * FROM clients_actifs;
```
## 11. Sous-requêtes

### Sous-requêtes dans WHERE, FROM, SELECT

*   Une sous-requête est une requête SELECT imbriquée dans une autre requête.
*   Elle peut être utilisée dans les clauses `WHERE`, `FROM` et `SELECT`.

```sql
-- Dans WHERE
SELECT * FROM produits WHERE prix > (SELECT AVG(prix) FROM produits);

-- Dans FROM
SELECT * FROM (SELECT id, nom FROM clients WHERE actif = 1) AS clients_actifs;

-- Dans SELECT
SELECT nom, (SELECT COUNT(*) FROM commandes WHERE client_id = clients.id) AS nombre_commandes FROM clients;
```
## 12. Fonctions et Procédures Stockées

### Création et exécution

*   Les fonctions et procédures stockées sont des blocs de code SQL stockés dans la base de données.
*   Elles permettent de réutiliser le code et d'améliorer les performances.
*   La syntaxe de création et d'exécution dépend du SGBDR.

```sql
-- Exemple (MySQL)
DELIMITER //
CREATE FUNCTION calculer_age(date_naissance DATE)
RETURNS INT
BEGIN
    RETURN YEAR(CURDATE()) - YEAR(date_naissance);
END //
DELIMITER ;

SELECT calculer_age('1990-01-01');
```
## 13. Bonnes Pratiques

### Optimisation des requêtes

*   Utiliser des index pour accélérer les requêtes.
*   Éviter les `SELECT *` inutiles.
*   Utiliser des jointures appropriées.
*   Analyser le plan d'exécution des requêtes.

### Sécurité

*   Éviter les injections SQL (utiliser des requêtes préparées).
*   Limiter les privilèges des utilisateurs.
*   Chiffrer les données sensibles.
## 14. Ressources et Communauté

### Documentation spécifique au SGBDR

*   [MySQL Documentation](https://dev.mysql.com/doc/)
*   [PostgreSQL Documentation](https://www.postgresql.org/docs/)
*   [Microsoft SQL Server Documentation](https://docs.microsoft.com/sql/)

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Database Administrators Stack Exchange](https://dba.stackexchange.com/)

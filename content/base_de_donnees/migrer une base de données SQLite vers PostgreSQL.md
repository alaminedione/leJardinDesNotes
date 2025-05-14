# Migrer Une Base De Données SQLite Vers PostgreSQL

Pour migrer une base de données SQLite vers PostgreSQL, voici une approche structurée avec différentes options selon vos besoins :

## Méthode Simple Avec Pgloader

La méthode la plus directe utilise pgloader 26:2 :

```bash
# Installation
sudo apt-get install pgloader

# Commande de migration
pgloader sqlite:///chemin/vers/ma_base.sqlite postgresql://utilisateur:motdepasse@hote:port/nom_base
```

## Méthode Par Étapes Avec Dump SQL

Pour plus de contrôle, utilisez cette approche en plusieurs étapes :

Créer un dump SQLite

```bash

sqlite3 ma_base.db .dump > dump.sql

```

Modifier le dump pour PostgreSQL

```bash
sed -e 's/AUTOINCREMENT/SERIAL PRIMARY KEY/g' \
    -e 's/DATETIME/TIMESTAMP/g' \
    -e 's/BOOLEAN/SMALLINT/g' \
    dump.sql > dump_pg.sql
```

Importer dans PostgreSQL

```bash

psql -d nom_base -U utilisateur -f dump_pg.sql

```

###  Adaptations Nécessaires

1. **Types de Données** 26:1 :
  - INTEGER PRIMARY KEY → SERIAL PRIMARY KEY
  - DATETIME → TIMESTAMP
  - BOOLEAN → SMALLINT
  - BLOB → bytea


2. **Clés Étrangères** :

```sql
-- Désactiver temporairement les contraintes
SET CONSTRAINTS ALL DEFERRED;

-- Réactiver après l'import
SET CONSTRAINTS ALL IMMEDIATE;
```

## Recommandations

1. **Pour les Petites Bases** :
  - Utiliser pgloader directement
  - Vérifier la cohérence des données après migration

2. **Pour les Grandes Bases** :
  - Utiliser la méthode par étapes
  - Migrer les tables importantes en premier
  - Tester la migration sur un environnement de développement

3. **Points d'Attention** :
  - Sauvegarder la base SQLite avant la migration
  - Vérifier les permissions PostgreSQL
  - Tester les requêtes complexes après migration

Cette approche structurée vous permettra de migrer votre base de données SQLite vers PostgreSQL de manière sécurisée et efficace.

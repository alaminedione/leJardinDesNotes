---
title: Bash
draft: false
tags:
  - bash
  - shell
description: Interpréteur de commandes Unix, largement utilisé pour l'automatisation de tâches et la gestion du système.
---

## Sommaire

1.  Introduction à Bash
    *   Qu'est-ce que Bash ?
    *   Historique et rôle dans les systèmes Unix/Linux
    *   Exécution de commandes
2.  Bases du Scripting Bash
    *   Syntaxe de base
    *   Variables (déclaration, affectation, accès)
    *   Types de données (chaînes, nombres)
    *   Opérateurs (arithmétiques, de comparaison, logiques)
3.  Structures de Contrôle
    *   Conditions (if, elif, else)
    *   Boucles (for, while, until)
    *   Case statements
4.  Entrées/Sorties et Redirections
    *   Entrée standard (stdin), sortie standard (stdout), sortie d'erreur standard (stderr)
    *   Redirection (>, >>, <, 2>, &>)
    *   Pipes (|)
5.  Fonctions
    *   Déclaration et appel de fonctions
    *   Arguments de fonction
    *   Valeurs de retour
6.  Gestion des Fichiers et Répertoires
    *   Commandes courantes (ls, cd, pwd, mkdir, rm, cp, mv)
    *   Permissions de fichiers (chmod, chown)
7.  Traitement de Texte
    *   Commandes (grep, sed, awk)
    *   Expressions régulières
8.  Gestion des Processus
    *   Exécution de commandes en arrière-plan (&)
    *   Jobs (jobs, fg, bg)
    *   Signaux (kill)
9.  Variables d'Environnement
    *   Variables globales et locales
    *   Exportation de variables
10. Débogage de Scripts Bash
    *   Options de débogage (set -x, set -e)
    *   Affichage des variables
11. Bonnes Pratiques
    *   Commentaires
    *   Gestion des erreurs
    *   Utilisation de guillemets
12. Ressources et Communauté
    *   Documentation (man pages)
    *   Communautés en ligne
## 1. Introduction à Bash

### Qu'est-ce que Bash ?

Bash (Bourne Again Shell) est un interpréteur de commandes Unix, largement utilisé pour l'automatisation de tâches et la gestion du système. Il permet d'exécuter des commandes, de manipuler des fichiers et des répertoires, de gérer les processus et de configurer l'environnement.

### Historique et rôle dans les systèmes Unix/Linux

*   Créé par Brian Fox en 1989.
*   Remplace le Bourne shell (sh) comme interpréteur de commandes par défaut dans de nombreux systèmes Unix/Linux.
*   Fournit des fonctionnalités améliorées par rapport au Bourne shell, telles que l'historique des commandes, l'autocomplétion et le scripting.

### Exécution de commandes

*   Taper une commande dans le terminal et appuyer sur Entrée.
*   Exemples : `ls`, `cd`, `pwd`, `mkdir`, `rm`.

## 2. Bases du Scripting Bash

### Syntaxe de base

*   Un script Bash est un fichier texte contenant une série de commandes Bash.
*   La première ligne d'un script Bash doit être `#!/bin/bash` (shebang) pour indiquer l'interpréteur à utiliser.
*   Les commentaires commencent par `#`.

```bash
#!/bin/bash

# Ceci est un commentaire
echo "Hello, World!"
```

### Variables (déclaration, affectation, accès)

*   Déclaration : `nom_variable=valeur` (pas d'espace avant ou après le signe égal).
*   Accès : `$nom_variable` ou `${nom_variable}`.

```bash
nom="John"
echo "Hello, $nom!"
echo "Hello, ${nom}!"
```

### Types de données (chaînes, nombres)

*   Bash ne distingue pas les types de données. Toutes les variables sont traitées comme des chaînes de caractères.
*   Les opérations arithmétiques sont effectuées avec des commandes spéciales (ex: `expr`, `$(())`).

```bash
age=30
echo "Age: $age"

resultat=$((age + 10))
echo "Age dans 10 ans: $resultat"
```

### Opérateurs (arithmétiques, de comparaison, logiques)

*   Arithmétiques : `+`, `-`, `*`, `/`, `%` (utilisés avec `expr` ou `$(( ))`).
*   Comparaison : `-eq` (égal), `-ne` (différent), `-lt` (inférieur), `-gt` (supérieur), `-le` (inférieur ou égal), `-ge` (supérieur ou égal).
*   Logiques : `&&`, `||`, `!`

```bash
x=10
y=5

if [ $x -gt $y ]; then
    echo "$x est supérieur à $y"
fi

if [[ $x > 0 && $y < 10 ]]; then
    echo "Condition remplie"
fi
```

## 3. Structures de Contrôle

### Conditions (if, elif, else)

*   Permettent d'exécuter des blocs de code en fonction de conditions.

```bash
if [ condition ]; then
    # ...
elif [ condition ]; then
    # ...
else
    # ...
fi
```

### Boucles (for, while, until)

*   `for` : Boucle for (pour parcourir les séquences).
*   `while` : Boucle while (tant que la condition est vraie).
*   `until` : Boucle until (jusqu'à ce que la condition soit vraie).

```bash
for i in 1 2 3 4 5; do
    echo $i
done

i=0
while [ $i -lt 5 ]; do
    echo $i
    i=$((i + 1))
done

i=0
until [ $i -ge 5 ]; do
    echo $i
    i=$((i + 1))
done
```

### Case statements

*   Permettent de simplifier les conditions multiples.

```bash
case "$variable" in
    "valeur1")
        # ...
        ;;
    "valeur2")
        # ...
        ;;
    *)
        # ...
        ;;
esac
```
## 4. Entrées/Sorties et Redirections

### Entrée standard (stdin), sortie standard (stdout), sortie d'erreur standard (stderr)

*   `stdin` : Entrée standard (par défaut, le clavier).
*   `stdout` : Sortie standard (par défaut, l'écran).
*   `stderr` : Sortie d'erreur standard (par défaut, l'écran).

### Redirection (>, >>, <, 2>, &>)

*   `>` : Redirige la sortie standard vers un fichier (écrase le contenu existant).
*   `>>` : Redirige la sortie standard vers un fichier (ajoute à la fin du fichier).
*   `<` : Redirige l'entrée standard depuis un fichier.
*   `2>` : Redirige la sortie d'erreur standard vers un fichier.
*   `&>` : Redirige la sortie standard et la sortie d'erreur standard vers un fichier.

```bash
ls > liste_fichiers.txt
echo "Erreur" 2> erreurs.txt
commande_bidon &> sortie.txt
```

### Pipes (|)

*   Permettent de connecter la sortie d'une commande à l'entrée d'une autre commande.

```bash
ls -l | grep "mon_fichier"
```
## 5. Fonctions

### Déclaration et appel de fonctions

*   Déclaration : `nom_fonction() { // corps }`
*   Appel : `nom_fonction`

### Arguments de fonction

*   Accès aux arguments : `$1`, `$2`, `$3`, ...
*   Nombre d'arguments : `$#`
*   Tous les arguments : `$@`

### Valeurs de retour

*   Utilisation de la commande `return` pour retourner une valeur (entre 0 et 255).
*   La valeur de retour est accessible via la variable `$?`.

```bash
ma_fonction() {
    echo "Argument 1: $1"
    echo "Nombre d'arguments: $#"
    return 0
}

ma_fonction "Hello" "World"
echo "Valeur de retour: $?"
```
## 6. Gestion des Fichiers et Répertoires

### Commandes courantes (ls, cd, pwd, mkdir, rm, cp, mv)

*   `ls` : Liste les fichiers et répertoires.
*   `cd` : Change de répertoire.
*   `pwd` : Affiche le répertoire courant.
*   `mkdir` : Crée un répertoire.
*   `rm` : Supprime des fichiers et des répertoires.
*   `cp` : Copie des fichiers et des répertoires.
*   `mv` : Déplace ou renomme des fichiers et des répertoires.

### Permissions de fichiers (chmod, chown)

*   `chmod` : Modifie les permissions d'un fichier ou d'un répertoire.
*   `chown` : Modifie le propriétaire d'un fichier ou d'un répertoire.

```bash
chmod +x mon_script.sh # Ajoute le droit d'exécution
chown user:group mon_fichier.txt # Change le propriétaire et le groupe
```
## 7. Traitement de Texte

### Commandes (grep, sed, awk)

*   `grep` : Recherche des motifs dans des fichiers.
*   `sed` : Éditeur de flux (permet de modifier du texte).
*   `awk` : Langage de programmation pour le traitement de texte.

### Expressions régulières

*   Utilisées avec `grep`, `sed` et `awk` pour rechercher et manipuler du texte.

```bash
grep "motif" mon_fichier.txt # Recherche les lignes contenant "motif"
sed 's/ancien/nouveau/g' mon_fichier.txt # Remplace "ancien" par "nouveau"
awk '{print $1}' mon_fichier.txt # Affiche la première colonne
```
## 8. Gestion des Processus

### Exécution de commandes en arrière-plan (&)

*   Ajouter `&` à la fin d'une commande pour l'exécuter en arrière-plan.

```bash
commande_longue &
```

### Jobs (jobs, fg, bg)

*   `jobs` : Liste les processus en arrière-plan.
*   `fg` : Amène un processus en avant-plan.
*   `bg` : Envoie un processus en arrière-plan.

### Signaux (kill)

*   `kill` : Envoie un signal à un processus (ex: `SIGTERM` pour terminer, `SIGKILL` pour forcer la terminaison).

```bash
kill -9 PID # Force la terminaison du processus avec l'ID PID
```
## 9. Variables d'Environnement

### Variables globales et locales

*   Variables globales : Accessibles depuis n'importe quel script ou commande.
*   Variables locales : Accessibles uniquement dans la fonction ou le script où elles sont définies.

### Exportation de variables

*   Utilisation de la commande `export` pour rendre une variable locale accessible aux processus enfants.

```bash
export MA_VARIABLE="valeur"
```
## 10. Débogage de Scripts Bash

### Options de débogage (set -x, set -e)

*   `set -x` : Affiche chaque commande avant son exécution.
*   `set -e` : Arrête l'exécution du script si une commande échoue.

### Affichage des variables

*   Utilisation de la commande `echo` pour afficher la valeur des variables.

```bash
set -x # Active le débogage

nom="John"
echo "Nom: $nom"

set +x # Désactive le débogage
```
## 11. Bonnes Pratiques

### Commentaires

*   Écrire des commentaires pour expliquer le code.
*   Utiliser des commentaires pour décrire le but du script, les fonctions et les variables.

### Gestion des erreurs

*   Vérifier le code de retour des commandes.
*   Utiliser `set -e` pour arrêter l'exécution du script en cas d'erreur.
*   Utiliser des blocs `try...catch` (avec des fonctions) pour gérer les exceptions.

### Utilisation de guillemets

*   Utiliser des guillemets doubles (`"`) pour permettre l'expansion des variables.
*   Utiliser des guillemets simples (`'`) pour empêcher l'expansion des variables.
## 12. Ressources et Communauté

### Documentation (man pages)

*   Utiliser la commande `man` pour accéder à la documentation des commandes Bash.

```bash
man ls
```

### Communautés en ligne

*   [Stack Overflow](https://stackoverflow.com/)
*   [Reddit (r/bash)](https://www.reddit.com/r/bash/)

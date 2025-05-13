# Guide Complet de Statistique Descriptive pour l'Analyse de Données

## Table des Matières

1.  [Introduction à la Statistique Descriptive](#introduction)
2.  [Indicateurs de Position (tendance centrale)](#tendance-centrale)
3.  [Indicateurs de Dispersion](#dispersion)
4.  [Indicateurs de Forme](#distribution)
5.  [Analyse Bivariée](#relations)
6.  [Visualisation des Données](#visualisation)
7.  [Implémentation avec Python](#python-implementation)
8.  [Interprétation des Résultats](#interpretation)
9.  [Cas Pratiques](#cas-pratiques)

## introduction

## 1. Introduction à la Statistique Descriptive

### Qu'est-ce que la Statistique Descriptive ?

La statistique descriptive est une branche des mathématiques qui s'occupe de la collecte, de l'organisation, de l'analyse et de la présentation des données. Elle permet de résumer et de visualiser des ensembles de données de manière à faire ressortir les caractéristiques essentielles.

### À quoi sert la Statistique Descriptive ?

*   **Synthétiser l'information** : Condenser de grands volumes de données en quelques indicateurs pertinents.
*   **Décrire les données** : Caractériser les propriétés d'un ensemble de données.
*   **Détecter des tendances** : Identifier des motifs ou des anomalies.
*   **Communiquer des résultats** : Présenter les caractéristiques principales des données.
*   **Faciliter la prise de décision** : Fournir une base objective pour l'action.

### Types de Données

*   **Données quantitatives** : Valeurs numériques mesurables.

    *   Continues (poids, taille, température).
    *   Discrètes (nombre d'enfants, de voitures).
*   **Données qualitatives** : Caractéristiques non numériques.

    *   Nominales (couleurs, genres).
    *   Ordinales (niveaux d'éducation, satisfaction).

<a name="tendance-centrale">

## 2. Indicateurs de Position (tendance centrale)

### Moyenne Arithmétique

La moyenne est la somme de toutes les valeurs divisée par le nombre de valeurs.

**Formule mathématique :**

$\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i = \frac{x_1 + x_2 + ... + x_n}{n}$

**Avec Python :**

```python
import numpy as np

data = [12, 15, 18, 22, 25, 30]
mean = np.mean(data)
# ou
mean = sum(data) / len(data)
print(f"Moyenne: {mean}")
```

**Avec R :**

```R
# Exemple de données
data <- c(12, 15, 18, 22, 25, 30)

# Moyenne
mean_r <- mean(data)
print(paste("Moyenne:", mean_r))
```

**Interprétation :** La moyenne représente la valeur typique ou centrale d'un ensemble de données. Elle est sensible aux valeurs extrêmes.

### Médiane

La médiane est la valeur qui divise l'ensemble de données en deux parties égales lorsque les données sont triées.

**Formule mathématique :** Si n est impair :

$\text{médiane} = x_{\frac{n+1}{2}}$

Si n est pair :

$\text{médiane} = \frac{x_{\frac{n}{2}} + x_{\frac{n}{2}+1}}{2}$

**Avec Python :**

```python
 median = np.median(data)
 print(f"Médiane: {median}")
 ```

 **Avec R :**

 ```R
 # Médiane
 median_r <- median(data)
 print(paste("Médiane:", median_r))
 ```

 **Interprétation :** La médiane représente la valeur centrale d'un ensemble de données et est moins sensible aux valeurs extrêmes que la moyenne.

### Mode

Le mode est la valeur qui apparaît le plus fréquemment dans un ensemble de données.

**Avec Python :**

```python
from scipy import stats

mode_result = stats.mode(data)
mode = mode_result.mode[0]
count = mode_result.count[0]
print(f"Mode: {mode} (apparaît {count} fois)")
```

**Avec R :**

```R
# Mode (nécessite souvent une fonction personnalisée ou un package)
# Exemple simple pour trouver le mode
get_mode <- function(v) {
   uniqv <- unique(v)
   uniqv[which.max(tabulate(match(v, uniqv)))]
}
mode_r <- get_mode(data)
print(paste("Mode:", mode_r))
```

**Interprétation :** Le mode indique la valeur la plus commune ou typique dans un ensemble de données.

<a name="dispersion">

## 3. Indicateurs de Dispersion

### Étendue

L'étendue est la différence entre la valeur maximale et la valeur minimale.

**Formule mathématique :**

$\text{étendue} = \max(x) - \min(x)$

**Avec Python :**

```python
data_range = max(data) - min(data)
print(f"Étendue: {data_range}")
```

**Avec R :**

```R
# Étendue
range_r <- max(data) - min(data)
print(paste("Étendue:", range_r))
```

**Interprétation :** L'étendue donne une idée simple de la dispersion des données, mais elle est très sensible aux valeurs extrêmes.

### Variance

La variance mesure la dispersion des valeurs autour de la moyenne.

**Formule mathématique (population) :**

$\sigma^2 = \frac{1}{N}\sum_{i=1}^{N}(x_i - \mu)^2$

**Formule mathématique (échantillon) :**

$s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2$

**Avec Python :**

```python
# Variance d'échantillon
variance = np.var(data, ddof=1)
print(f"Variance: {variance}")

# Variance de population
pop_variance = np.var(data, ddof=0)
print(f"Variance de population: {pop_variance}")
```

**Avec R :**

```R
# Exemple de données (assurez-vous que 'data' est défini)
# data <- c(12, 15, 18, 22, 25, 30)

# Variance d'échantillon
variance_r <- var(data)
print(paste("Variance (échantillon):", variance_r))
```

**Interprétation :** La variance quantifie la dispersion des données autour de la moyenne. Une variance élevée indique des données très dispersées.

### Écart-type

L'écart-type est la racine carrée de la variance.

**Formule mathématique (population) :**

$\sigma = \sqrt{\sigma^2} = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(x_i - \mu)^2}$

**Formule mathématique (échantillon) :**

$s = \sqrt{s^2} = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2}$

**Avec Python :**

```python
# Écart-type d'échantillon
std_dev = np.std(data, ddof=1)
print(f"Écart-type: {std_dev}")

# Écart-type de population
pop_std_dev = np.std(data, ddof=0)
print(f"Écart-type de population: {pop_std_dev}")
```

**Avec R :**

```R
# Écart-type d'échantillon
std_dev_r <- sd(data)
print(paste("Écart-type (échantillon):", std_dev_r))
```

**Interprétation :** L'écart-type mesure la dispersion des données autour de la moyenne dans les mêmes unités que les données originales.

### Écart Interquartile (IQR)

L'IQR est la différence entre le troisième quartile (Q3) et le premier quartile (Q1).

**Formule mathématique :**

$\text{IQR} = Q_3 - Q_1$

**Avec Python :**

```python
q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)
iqr = q3 - q1
print(f"Q1: {q1}, Q3: {q3}, IQR: {iqr}")
```

**Avec R :**

```R
# Écart Interquartile (IQR)
iqr_r <- IQR(data)
print(paste("IQR:", iqr_r))

# Ou calcul manuel
quartiles_r <- quantile(data, probs = c(0.25, 0.75))
iqr_manuel <- quartiles_r[2] - quartiles_r[1]
print(paste("IQR (manuel):", iqr_manuel))
```

**Interprétation :** L'IQR représente la plage du milieu 50% des données et est robuste aux valeurs extrêmes.

### Coefficient de Variation

Le coefficient de variation est le rapport entre l'écart-type et la moyenne.

**Formule mathématique :**

$CV = \frac{s}{\bar{x}} \times 100%$

**Avec Python :**

```python
cv = (std_dev / mean) * 100
print(f"Coefficient de variation: {cv}%")
```

**Avec R :**

```R
# Coefficient de Variation
# Assurez-vous que 'data' est défini et que la moyenne n'est pas nulle
if (mean(data) != 0) {
  cv_r <- (sd(data) / mean(data)) * 100
  print(paste("Coefficient de variation:", cv_r, "%"))
} else {
  print("Impossible de calculer le coefficient de variation car la moyenne est nulle.")
}
```

**Interprétation :** Le CV exprime la dispersion relative, permettant de comparer la variabilité entre différents ensembles de données.

<a name="distribution">

## 4. Indicateurs de Forme

### Percentiles et Quantiles

Les percentiles divisent les données en 100 parties égales, tandis que les quantiles divisent les données en parties égales.

**Avec Python :**

```python
# Calcul des quartiles (25%, 50%, 75%)
q1 = np.percentile(data, 25)
q2 = np.percentile(data, 50)  # médiane
q3 = np.percentile(data, 75)
print(f"Q1: {q1}, Q2 (médiane): {q2}, Q3: {q3}")

# Calcul des déciles (10%, 20%, ..., 90%)
deciles = [np.percentile(data, i*10) for i in range(1, 10)]
print(f"Déciles: {deciles}")
```

**Avec R :**

```R
# Exemple de données (assurez-vous que 'data' est défini)
# data <- c(10, 12, 12, 15, 18, 20, 22, 22, 22, 25)

# Calcul des quartiles (25%, 50%, 75%)
quartiles_r <- quantile(data, probs = c(0.25, 0.5, 0.75))
print("Quartiles:")
print(quartiles_r)

# Calcul des déciles (10%, 20%, ..., 90%)
deciles_r <- quantile(data, probs = seq(0.1, 0.9, by = 0.1))
print("Déciles:")
print(deciles_r)
```

### Asymétrie (Skewness)

L'asymétrie mesure le degré et la direction de l'asymétrie.

**Formule mathématique :**

$\text{skewness} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^3$

**Avec Python :**

```python
from scipy import stats

skewness = stats.skew(data)
print(f"Coefficient d'asymétrie: {skewness}")
```

**Avec R :**

```R
# Asymétrie (Skewness)
# Nécessite le package 'e1071'
# install.packages("e1071")
# library(e1071)

# skewness_r <- skewness(data)
# print(paste("Coefficient d'asymétrie:", skewness_r))
```

**Interprétation :**

*   Asymétrie positive (> 0) : Queue à droite (valeurs extrêmes élevées).
*   Asymétrie négative (< 0) : Queue à gauche (valeurs extrêmes basses).
*   Proche de 0 : Distribution approximativement symétrique.

### Aplatissement (Kurtosis)

Le kurtosis mesure l'aplatissement ou la pointicité d'une distribution.

**Formule mathématique :**

$\text{kurtosis} = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{x_i - \bar{x}}{s}\right)^4 - 3$

**Avec Python :**

```python
kurtosis = stats.kurtosis(data)
print(f"Coefficient d'aplatissement: {kurtosis}")
```

**Avec R :**

```R
# Aplatissement (Kurtosis)
# Nécessite le package 'e1071'
# install.packages("e1071")
# library(e1071)

# kurtosis_r <- kurtosis(data)
# print(paste("Coefficient d'aplatissement:", kurtosis_r))
```

**Interprétation :**

*   Kurtosis positif : Distribution leptokurtique (plus pointue qu'une normale).
*   Kurtosis négatif : Distribution platykurtique (plus aplatie qu'une normale).
*   Proche de 0 : Distribution mésokurtique (similaire à une normale).

<a name="relations">

## 5. Analyse Bivariée

### Covariance

La covariance mesure la relation linéaire entre deux variables.

**Formule mathématique :**

$\text{cov}(X,Y) = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})$

**Avec Python :**

```python
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

covariance = np.cov(x, y)[0, 1]
print(f"Covariance: {covariance}")
```

**Interprétation :** La covariance indique la direction de la relation (positive ou négative), mais son ampleur dépend des unités des variables.

### Coefficient de Corrélation de Pearson

Le coefficient de corrélation mesure la force et la direction de la relation linéaire entre deux variables.

**Formule mathématique :**

$r = \frac{\text{cov}(X,Y)}{s_X \times s_Y} = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n}(x_i - \bar{x})^2 \sum_{i=1}^{n}(y_i - \bar{y})^2}}$

**Avec Python :**

```python
correlation, p_value = stats.pearsonr(x, y)
print(f"Coefficient de corrélation: {correlation}, p-value: {p_value}")
```

**Interprétation :**

*   r = 1 : Corrélation positive parfaite.
*   r = -1 : Corrélation négative parfaite.
*   r = 0 : Pas de corrélation linéaire.
*   0 < |r| < 0.3 : Corrélation faible.
*   0.3 < |r| < 0.7 : Corrélation modérée.
*   0.7 < |r| < 1 : Corrélation forte.

### Coefficient de Corrélation de Spearman

Le coefficient de corrélation de Spearman mesure la force et la direction de la relation monotone entre deux variables.

**Avec Python :**

```python
spearman_corr, p_value = stats.spearmanr(x, y)
print(f"Corrélation de Spearman: {spearman_corr}, p-value: {p_value}")
```

**Interprétation :** Similaire au coefficient de Pearson, mais basé sur les rangs des valeurs plutôt que sur les valeurs elles-mêmes.

<a name="visualisation">

## 6. Visualisation des Données

### Histogramme

L'histogramme représente la distribution des données en comptant le nombre d'observations dans des intervalles adjacents.

**Avec Python :**

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.histplot(data, bins=10, kde=True)
plt.title("Histogramme des Données")
plt.xlabel("Valeur")
plt.ylabel("Fréquence")
plt.show()
```

### Boîte à Moustaches (Box Plot)

Le box plot affiche les quartiles, la médiane et les valeurs extrêmes.

**Avec Python :**

```python
plt.figure(figsize=(10, 6))
sns.boxplot(x=data)
plt.title("Boîte à Moustaches")
plt.xlabel("Valeur")
plt.show()
```

### Diagramme de Dispersion (Scatter Plot)

Le scatter plot montre la relation entre deux variables.

**Avec Python :**

```python
plt.figure(figsize=(10, 6))
sns.scatterplot(x=x, y=y)
plt.title("Diagramme de Dispersion")
plt.xlabel("Variable X")
plt.ylabel("Variable Y")
plt.show()
```

### Heatmap de Corrélation

La heatmap visualise la matrice de corrélation entre plusieurs variables.

**Avec Python :**

```python
import pandas as pd

# Créer un DataFrame avec plusieurs variables
df = pd.DataFrame({'X': x, 'Y': y, 'Z': [5, 8, 11, 14, 17]})

# Calculer la matrice de corrélation
corr_matrix = df.corr()

# Visualiser la matrice de corrélation
plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', vmin=-1, vmax=1)
plt.title("Matrice de Corrélation")
plt.show()
```

<a name="python-implementation">

## 7. Implémentation avec Python

<a name="data-visualization">

## 8. Visualisation des Données

### Histogramme

L'histogramme représente la distribution des données en comptant le nombre d'observations dans des intervalles adjacents.

**Avec Python :**

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.histplot(data, bins=10, kde=True)
plt.title("Histogramme des Données")
plt.xlabel("Valeur")
plt.ylabel("Fréquence")
plt.show()
```

### Boîte à Moustaches (Box Plot)

Le box plot affiche les quartiles, la médiane et les valeurs extrêmes.

**Avec Python :**

```python
plt.figure(figsize=(10, 6))
sns.boxplot(x=data)
plt.title("Boîte à Moustaches")
plt.xlabel("Valeur")
plt.show()
```

### Diagramme de Dispersion (Scatter Plot)

Le scatter plot montre la relation entre deux variables.

**Avec Python :**

```python
plt.figure(figsize=(10, 6))
sns.scatterplot(x=x, y=y)
plt.title("Diagramme de Dispersion")
plt.xlabel("Variable X")
plt.ylabel("Variable Y")
plt.show()
```

### Heatmap de Corrélation

La heatmap visualise la matrice de corrélation entre plusieurs variables.

**Avec Python :**

```python
import pandas as pd

# Créer un DataFrame avec plusieurs variables
df = pd.DataFrame({'X': x, 'Y': y, 'Z': [5, 8, 11, 14, 17]})

# Calculer la matrice de corrélation
corr_matrix = df.corr()

# Visualiser la matrice de corrélation
plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', vmin=-1, vmax=1)
plt.title("Matrice de Corrélation")
plt.show()
```

<a name="probability-distributions">

## 9. Distributions de Probabilité

### Distribution Normale

La distribution normale est une distribution de probabilité continue très courante.

**Avec Python :**

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Générer des données pour la distribution normale
data = np.arange(-3, 3, 0.01)
pdf = norm.pdf(data, loc=0, scale=1)

# Tracer la distribution normale
plt.plot(data, pdf)
plt.title('Distribution Normale')
plt.xlabel('Données')
plt.ylabel('Densité de Probabilité')
plt.show()
```

### Distribution Binomiale

La distribution binomiale est une distribution de probabilité discrète qui décrit la probabilité de succès dans une séquence d'expériences indépendantes.

**Avec Python :**

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import binom

# Définir les valeurs de n et p
n = 10
p = 0.5
# Définir la liste des valeurs x
x = list(range(n + 1))
# Liste des valeurs pmf
y = [binom.pmf(i, n, p) for i in x]
# Tracer le graphique
plt.plot(x, y, 'o-')
plt.xlabel('Nombre de Succès')
plt.ylabel('Probabilité')
plt.title('Distribution Binomiale')
plt.show()
```

### Bibliothèques Essentielles

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
```

### Exemple Complet d'Analyse Descriptive

```python
# Chargement des données
# Exemple avec DataFrame pandas
df = pd.DataFrame({
    'Age': [25, 30, 35, 40, 45, 28, 32, 38, 42, 47],
    'Salaire': [45000, 55000, 60000, 70000, 80000, 48000, 57000, 63000, 72000, 85000],
    'Experience': [1, 3, 5, 8, 12, 2, 4, 6, 9, 15],
    'Satisfaction': [3, 4, 3, 5, 4, 2, 3, 4, 5, 4]
})

# Résumé statistique complet
print("Résumé statistique:")
print(df.describe())

# Mesures de tendance centrale
print("\nMoyennes:")
print(df.mean())
print("\nMédianes:")
print(df.median())
print("\nModes:")
print(df.mode().iloc[0])

# Mesures de dispersion
print("\nÉcarts-types:")
print(df.std())
print("\nVariances:")
print(df.var())
print("\nÉtendues:")
print(df.max() - df.min())

# Calcul des quartiles
Q1 = df.quantile(0.25)
Q3 = df.quantile(0.75)
IQR = Q3 - Q1
print("\nQ1 (25%):")
print(Q1)
print("\nQ3 (75%):")
print(Q3)
print("\nIQR:")
print(IQR)

# Asymétrie et aplatissement
print("\nAsymétrie (Skewness):")
print(df.skew())
print("\nAplatissement (Kurtosis):")
print(df.kurtosis())

# Matrice de corrélation
correlation_matrix = df.corr()
print("\nMatrice de corrélation:")
print(correlation_matrix)

# Visualisations
plt.figure(figsize=(12, 10))

# Histogrammes
plt.subplot(2, 2, 1)
sns.histplot(df['Age'], kde=True)
plt.title('Distribution des Ages')

plt.subplot(2, 2, 2)
sns.histplot(df['Salaire'], kde=True)
plt.title('Distribution des Salaires')

# Diagramme de dispersion
plt.subplot(2, 2, 3)
sns.scatterplot(x='Experience', y='Salaire', data=df)
plt.title('Salaire vs Expérience')

# Boîte à moustaches
plt.subplot(2, 2, 4)
sns.boxplot(data=df)
plt.title('Boîtes à Moustaches')

plt.tight_layout()
plt.show()

# Heatmap de corrélation
plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Matrice de Corrélation')
plt.show()

<a name="interpretation">

## 8. Interprétation des Résultats

### Interprétation des Mesures de Tendance Centrale

1. **Moyenne vs Médiane :**

    *   Si la moyenne > médiane : Distribution asymétrique positive (queue à droite).
    *   Si la moyenne < médiane : Distribution asymétrique négative (queue à gauche).
    *   Si la moyenne ≈ médiane : Distribution approximativement symétrique.
2. **Choix de la Mesure Appropriée :**

    *   Pour les distributions symétriques : Moyenne.
    *   Pour les distributions asymétriques : Médiane.
    *   Pour les données catégorielles nominales : Mode.

### Interprétation des Mesures de Dispersion

1.  **Écart-type :**

    *   Règle empirique (pour les distributions normales) :
        *   Environ 68 % des données se situent à ±1 écart-type de la moyenne.
        *   Environ 95 % des données se situent à ±2 écarts-types de la moyenne.
        *   Environ 99,7 % des données se situent à ±3 écarts-types de la moyenne.
2.  **Coefficient de Variation :**

    *   CV < 15 % : Faible dispersion.
    *   15 % < CV < 30 % : Dispersion modérée.
    *   CV > 30 % : Forte dispersion.

### Interprétation des Corrélations

1.  **Force de la Corrélation :**

    *   |r| < 0.3 : Faible corrélation.
    *   0.3 < |r| < 0.7 : Corrélation modérée.
    *   |r| > 0.7 : Forte corrélation.
2.  **Signification Statistique :**

    *   P-value < 0.05 : Corrélation statistiquement significative.
    *   P-value > 0.05 : Pas de preuve suffisante pour conclure à une corrélation significative.

### Interprétation des Visualisations

1.  **Histogramme :**

    *   Distribution normale : Forme de cloche.
    *   Distribution asymétrique : Queue prolongée d'un côté.
    *   Distribution bimodale : Deux pics distincts.
2.  **Boîte à Moustaches :**

    *   Médiane : Ligne centrale.
    *   Boîte : IQR (Q3-Q1).
    *   Moustaches : Généralement 1.5 × IQR.
    *   Points individuels : Valeurs aberrantes potentielles.
3.  **Diagramme de Dispersion :**

    *   Tendance positive : Les points montent de gauche à droite.
    *   Tendance négative : Les points descendent de gauche à droite.
    *   Forme linéaire : Relation linéaire.
    *   Forme curviligne : Relation non linéaire.

<a name="cas-pratiques">

## 9. Cas Pratiques

### Exemple 1 : Analyse des Revenus

Supposons que nous ayons un ensemble de données sur les revenus mensuels (en euros) de 100 employés d'une entreprise.

```python
# Génération de données fictives
np.random.seed(42)
revenus = np.random.lognormal(mean=8.5, sigma=0.4, size=100)

# Statistiques descriptives
print(f"Moyenne: {np.mean(revenus):.2f} €")
print(f"Médiane: {np.median(revenus):.2f} €")
print(f"Écart-type: {np.std(revenus, ddof=1):.2f} €")
print(f"Minimum: {np.min(revenus):.2f} €")
print(f"Maximum: {np.max(revenus):.2f} €")
print(f"Asymétrie: {stats.skew(revenus):.2f}")

# Visualisations
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
sns.histplot(revenus, kde=True)
plt.axvline(np.mean(revenus), color='r', linestyle='--', label=f'Moyenne: {np.mean(revenus):.0f} €')
plt.axvline(np.median(revenus), color='g', linestyle='-', label=f'Médiane: {np.median(revenus):.0f} €')
plt.title('Distribution des Revenus')
plt.xlabel('Revenu Mensuel (€)')
plt.ylabel('Fréquence')
plt.legend()

plt.subplot(1, 2, 2)
sns.boxplot(y=revenus)
plt.title('Boîte à Moustaches des Revenus')
plt.ylabel('Revenu Mensuel (€)')

plt.tight_layout()
plt.show()
```

**Interprétation :**

*   La moyenne est supérieure à la médiane, ce qui indique une distribution asymétrique positive.
*   L'écart significatif entre la moyenne et la médiane suggère la présence de quelques revenus très élevés qui tirent la moyenne vers le haut.
*   L'asymétrie positive est confirmée par le coefficient d'asymétrie et visible sur l'histogramme.
*   Pour rapporter le "revenu typique" de cette population, la médiane serait plus appropriée que la moyenne.

### Exemple 2 : Relation entre Expérience et Salaire

Examinons la relation entre l'expérience professionnelle (en années) et le salaire annuel.

```python
# Génération de données fictives
np.random.seed(42)
experience = np.random.uniform(1, 20, 50)
salaire = 30000 + 2500 * experience + np.random.normal(0, 5000, 50)

# Calcul de la corrélation
correlation, p_value = stats.pearsonr(experience, salaire)
print(f"Coefficient de corrélation: {correlation:.2f}")
print(f"P-value: {p_value:.6f}")

# Régression linéaire
slope, intercept, r_value, p_value, std_err = stats.linregress(experience, salaire)
print(f"Équation de régression: Salaire = {intercept:.2f} + {slope:.2f} * Expérience")
print(f"R²: {r_value**2:.2f}")

# Visualisation
plt.figure(figsize=(10, 6))
sns.scatterplot(x=experience, y=salaire)
plt.plot(experience, intercept + slope * experience, 'r')
plt.title('Relation entre Expérience et Salaire')
plt.xlabel('Expérience (années)')
plt.ylabel('Salaire Annuel (€)')
plt.text(15, 40000, f'r = {correlation:.2f}\nR² = {r_value**2:.2f}', fontsize=12)
plt.show()
```

**Interprétation :**

*   La corrélation forte et positive indique que le salaire tend à augmenter avec l'expérience.
*   La p-value très faible suggère que cette corrélation est statistiquement significative.
*   Le coefficient de détermination (R²) indique que X % de la variation des salaires peut être expliquée par l'expérience.
*   La pente de la droite de régression suggère qu'en moyenne, chaque année d'expérience supplémentaire est associée à une augmentation de X € du salaire annuel.

## Conclusion

La statistique descriptive est un outil fondamental pour tout analyste de données. Elle permet de comprendre la structure et les caractéristiques des données, d'identifier des tendances et des relations, et de communiquer efficacement les résultats. En combinant les différentes mesures et visualisations présentées dans ce guide, vous serez en mesure d'extraire des insights précieux de vos données et de les présenter de manière claire et convaincante.

Les compétences en statistique descriptive constituent la base sur laquelle s'appuient des techniques plus avancées comme l'inférence statistique, l'apprentissage automatique et l'analyse prédictive. Maîtriser ces concepts vous permettra d'aborder avec confiance des problèmes d'analyse de données plus complexes.

# Pandas — Documentation Résumée

# Table of Contents

- [Pandas — Documentation Résumée](#pandas--documentation-résumée)
- [Table of Contents](#table-of-contents)
  - [Introduction / Description ](#introduction--description-)
    - [Présentation de Pandas ](#présentation-de-pandas-)
    - [Objectif ](#objectif-)
    - [Fonctionnalités principales ](#fonctionnalités-principales-)
  - [Installation / Import ](#installation--import-)
    - [Installation de Pandas ](#installation-de-pandas-)
    - [Importer Pandas ](#importer-pandas-)
  - [PANDAS SERIES ](#pandas-series-)
    - [Présentation des Series ](#présentation-des-series-)
      - [Objectif ](#objectif--1)
      - [Fonctionnalités principales ](#fonctionnalités-principales--1)
    - [`pd.Series()` ](#pdseries-)
    - [Accès aux éléments d’une Series ](#accès-aux-éléments-dune-series-)
      - [`s[index]` — Accès par position ou label ](#sindex--accès-par-position-ou-label-)
      - [`s.loc[label]` — Accès par label explicite ](#sloclabel--accès-par-label-explicite-)
      - [`s.iloc[position]` — Accès par position entière ](#silocposition--accès-par-position-entière-)
      - [`s.at[label]` — Accès rapide par label ](#satlabel--accès-rapide-par-label-)
      - [`s.iat[position]` — Accès rapide par position ](#siatposition--accès-rapide-par-position-)
      - [Sélection conditionnelle (filtrage) ](#sélection-conditionnelle-filtrage-)
      - [Résumé des méthodes d’accès ](#résumé-des-méthodes-daccès-)
    - [Opérations mathématiques sur une Series ](#opérations-mathématiques-sur-une-series-)
      - [Opérations arithmétiques de base ](#opérations-arithmétiques-de-base-)
      - [Opérations entre Series ](#opérations-entre-series-)
      - [Points importants ](#points-importants-)
    - [Opérations statistiques sur Series ](#opérations-statistiques-sur-series-)
      - [`s.sum()` ](#ssum-)
      - [`s.mean()` ](#smean-)
      - [`s.median()` ](#smedian-)
      - [`s.max()` ](#smax-)
      - [`s.min()` ](#smin-)
      - [`s.idxmax()` ](#sidxmax-)
    - [`s.idxmin()` ](#sidxmin-)
      - [`s.std()` ](#sstd-)
      - [`s.describe()` ](#sdescribe-)
    - [Conversion Series ↔ DataFrame ](#conversion-series--dataframe-)

---
---

## Introduction / Description <a id="introduction--description-"></a>

### Présentation de Pandas <a id="présentation-de-pandas-"></a>

Pandas est une **bibliothèque Python open-source** dédiée à la **manipulation et à l'analyse de données tabulaires**.
Elle fournit les structures **Series** et **DataFrame**, puissantes et optimisées pour le traitement, la transformation, l’analyse et la préparation de données.

---

### Objectif <a id="objectif-"></a>

Pandas vise à :

* Simplifier la manipulation de données sous forme de tableaux
* Fournir des outils rapides pour filtrage, tri, nettoyage, fusion, statistiques
* Permettre l'import/export depuis de nombreux formats (CSV, Excel, SQL…)
* Faciliter les analyses exploratoires et transformations avancées

---

### Fonctionnalités principales <a id="fonctionnalités-principales-"></a>

* Structure **DataFrame** performante
* Lecture/écriture : CSV, JSON, Excel, SQL, Parquet
* Filtrage, tri, indexation, slicing
* Gestion des valeurs manquantes (`NaN`, `None`)
* GroupBy, merge, join, pivot tables
* Intégration avec NumPy, Matplotlib, Jupyter, Scikit-Learn
* Calcul vectorisé rapide

---
---

## Installation / Import <a id="installation--import-"></a>

### Installation de Pandas <a id="installation-de-pandas-"></a>

Installation avec pip :

```bash
pip install pandas
```

Avec conda :

```bash
conda install pandas
```

---

### Importer Pandas <a id="importer-pandas-"></a>

Dans votre script Python :

```python
import pandas as pd
```

---
---

## PANDAS SERIES <a id="pandas-series-"></a>

### Présentation des Series <a id="présentation-des-series-"></a>

Une **Series** est une structure de données unidimensionnelle dans Pandas, capable de contenir **des valeurs de n’importe quel type** (entiers, flottants, chaînes, objets Python, etc.) et associée à **un index**.
Elle peut être vue comme un **tableau étiqueté** ou comme une **colonne d’un DataFrame**.

---

#### Objectif <a id="objectif-"></a>

Les Series Pandas servent à :

* Représenter et manipuler des données unidimensionnelles
* Permettre un accès rapide via un **index** personnalisé
* Intégrer facilement dans les DataFrame
* Effectuer des opérations vectorisées et statistiques rapidement
* Manipuler et transformer des données pour analyses et visualisations

---

#### Fonctionnalités principales <a id="fonctionnalités-principales-"></a>

* Indexation et sélection par labels ou positions
* Opérations vectorisées (arithmétiques et logiques)
* Gestion des valeurs manquantes (`NaN`)
* Méthodes statistiques rapides (`sum`, `mean`, `median`, `std`, etc.)
* Support pour les chaînes de caractères (`.str`) et les dates (`.dt`)
* Conversion facile en DataFrame ou tableau NumPy
* Compatibilité avec Matplotlib pour visualisations simples

---

### `pd.Series()` <a id="pdseries-"></a>

`pd.Series()` est une **structure de données unidimensionnelle** de Pandas. Elle permet de stocker des **valeurs étiquetées** (index) et de réaliser des opérations vectorisées, statistiques ou de manipulation de données. Une Series peut contenir des **types de données hétérogènes**, mais le type est généralement uniforme pour des performances optimales.

```python
import pandas as pd

# Création d'une Series simple à partir d'une liste
s = pd.Series([10, 20, 30, 40])
print(s)

# Création d'une Series avec un index personnalisé
s2 = pd.Series([10, 20, 30], index=["a", "b", "c"])
print(s2)
```

**Paramètres principaux :**

* `data` (array-like, scalar, dict, Series)
  Les données à stocker dans la Series. Peut être une **liste**, un **tableau NumPy**, un **dictionnaire** ou même un **scalaire**.
* `index` (array-like, optionnel)
  Les **étiquettes** des éléments de la Series. Si non fourni, un index par défaut `[0, 1, 2, …]` est créé.
* `dtype` (type, optionnel)
  Le type de données de la Series. Si non fourni, Pandas infère automatiquement le type.
* `name` (str, optionnel)
  Nom de la Series, utile lorsqu’elle est intégrée dans un DataFrame ou pour les opérations statistiques.
* `copy` (bool, optionnel, défaut `False`)
  Si `True`, les données sont copiées ; sinon, la Series peut partager la même mémoire que `data`.

**Retour :** Une **Series Pandas**, un tableau étiqueté pouvant être manipulé comme un **array** mais avec des fonctionnalités avancées (indexation, filtrage, opérations vectorisées, méthodes statistiques).

**Notes importantes :**

* `pd.Series()` est **souvent la base** d’un DataFrame (une colonne est une Series).
* Permet des opérations rapides **vectorisées**, contrairement aux listes Python classiques.
* Les Series peuvent contenir des **valeurs manquantes (`NaN`)** et les gérer facilement avec les méthodes `.isna()`, `.fillna()`, `.dropna()`.
* L’**index** peut être **numérique ou étiqueté**, et peut être utilisé pour sélectionner ou filtrer des données.

---

Voici une présentation détaillée des **méthodes d’accès aux éléments d’une `pd.Series()`** dans le **même format que ton exemple SQLAlchemy** :

---

### Accès aux éléments d’une Series <a id="accès-aux-éléments-dune-series-"></a>

Les Series Pandas permettent de **sélectionner, filtrer et accéder** facilement aux éléments via **labels** ou **positions**. Ces méthodes sont essentielles pour manipuler les données unidimensionnelles.

---

#### `s[index]` — Accès par position ou label <a id="sindex--accès-par-position-ou-label-"></a>

```python
import pandas as pd

s = pd.Series([10, 20, 30], index=["a", "b", "c"])

# Accès par position (index par défaut si numérique)
print(s[0])  # 10

# Accès par label
print(s["b"])  # 20

# Accès multiple
print(s[["a", "c"]])  # Series contenant les éléments a et c
```

**Notes :**

* Si l’index est **numérique**, `s[0]` peut être ambigu : c’est soit l’étiquette 0, soit la première position.
* Pour lever l’ambiguïté, privilégier `iloc` et `loc`.

---

#### `s.loc[label]` — Accès par label explicite <a id="sloclabel--accès-par-label-explicite-"></a>

```python
# Accès à un élément par son label
print(s.loc["b"])  # 20

# Accès à plusieurs labels
print(s.loc[["a", "c"]])
```

**Notes :**
* `loc` sélectionne **toujours par étiquette**.
* Peut être utilisé avec **slicing inclusif** :

```python
print(s.loc["a":"b"])  # inclut "b"
```

---

#### `s.iloc[position]` — Accès par position entière <a id="silocposition--accès-par-position-entière-"></a>

```python
# Accès au premier élément
print(s.iloc[0])  # 10

# Accès multiple par positions
print(s.iloc[[0, 2]])  # 10 et 30

# Slicing par positions (exclusif à droite)
print(s.iloc[0:2])  # 10 et 20
```

**Notes :**
* `iloc` est **basé sur les positions**, similaire à l’indexation des listes Python.
* Très utile quand les labels sont numériques et qu’on veut éviter l’ambiguïté.

---

#### `s.at[label]` — Accès rapide par label <a id="satlabel--accès-rapide-par-label-"></a>

```python
print(s.at["b"])  # 20
```

**Notes :**
* `at` est **plus rapide que `loc`** pour accéder à un **seul élément**.
* Ne fonctionne que pour **un seul label à la fois**, pas pour des slices ou des listes.

---

#### `s.iat[position]` — Accès rapide par position <a id="siatposition--accès-rapide-par-position-"></a>

```python
print(s.iat[2])  # 30
```

**Notes :**
* `iat` est **plus rapide que `iloc`** pour un **élément unique**.
* Ne supporte pas la sélection multiple ou le slicing.

---

#### Sélection conditionnelle (filtrage) <a id="sélection-conditionnelle-filtrage-"></a>

```python
# Tous les éléments > 15
print(s[s > 15])

# Avec loc
print(s.loc[s > 15])
```

**Notes :**
* Le filtrage retourne une **nouvelle Series**.
* Permet des opérations vectorisées sur des sous-ensembles de données.

---

#### Résumé des méthodes d’accès <a id="résumé-des-méthodes-daccès-"></a>

| Méthode            | Accès par                         | Slicing multiple | Performance |
| ------------------ | --------------------------------- | ---------------- | ----------- |
| `s[index]`         | label ou position (selon l’index) | Oui              | standard    |
| `s.loc[label]`     | label                             | Inclusif         | standard    |
| `s.iloc[position]` | position                          | Exclusif         | standard    |
| `s.at[label]`      | label                             | Non              | très rapide |
| `s.iat[position]`  | position                          | Non              | très rapide |

---

### Opérations mathématiques sur une Series <a id="opérations-mathématiques-sur-une-series-"></a>

Les Series Pandas permettent d’effectuer facilement des **opérations mathématiques élément par élément** grâce à leur nature vectorisée. Ces opérations sont rapides et optimisées pour traiter de grandes quantités de données.

---

#### Opérations arithmétiques de base <a id="opérations-arithmétiques-de-base-"></a>

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

# Addition
print(s + 5)   # [15, 25, 35, 45]

# Soustraction
print(s - 2)   # [8, 18, 28, 38]

# Multiplication
print(s * 2)   # [20, 40, 60, 80]

# Division
print(s / 10)  # [1.0, 2.0, 3.0, 4.0]

# Division entière
print(s // 3)  # [3, 6, 10, 13]

# Modulo
print(s % 3)   # [1, 2, 0, 1]

# Puissance
print(s ** 2)  # [100, 400, 900, 1600]
```

**Notes :**
* Toutes les opérations sont **appliquées élément par élément**.
* La Series conserve son **index** original après l’opération.

---

#### Opérations entre Series <a id="opérations-entre-series-"></a>

Les opérations peuvent être faites entre deux Series alignées sur l’**index** :

```python

s = pd.Series([10, 20, 30, 40])
s2 = pd.Series([1, 2, 3, 4])

# Addition
print(s + s2)  # [11, 22, 33, 44]

# Multiplication
print(s * s2)  # [10, 40, 90, 160]

# Soustraction
print(s - s2)  # [9, 18, 27, 36]
```

**Notes :**
* Si les **index ne correspondent pas**, Pandas insère des **NaN** pour les valeurs manquantes.

---

#### Points importants <a id="points-importants-"></a>

* Les opérations mathématiques sur les Series sont **vectorisées**, donc beaucoup plus rapides que les boucles Python.
* L’index est **toujours conservé** après chaque opération.
* Ces méthodes peuvent être combinées avec des **opérations logiques** pour effectuer des calculs conditionnels.

---

### Opérations statistiques sur Series <a id="opérations-statistiques-sur-series-"></a>

#### `s.sum()` <a id="ssum-"></a>

La méthode `sum()` permet de **calculer la somme de tous les éléments d’une Series**. Elle est **vectorisée**, ce qui la rend très rapide, même sur de grandes séries de données.

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

# Calcul de la somme
total = s.sum()
print(total)  # 100
```

**Paramètres principaux :**
* `axis` (0 ou 'index', optionnel, défaut `0`)
  Détermine l’axe le long duquel la somme est calculée. Pour une Series, il n’a pas vraiment d’effet, mais il est utile dans les DataFrame.
* `skipna` (bool, optionnel, défaut `True`)
  Si `True`, les valeurs manquantes (`NaN`) sont **ignorées** lors du calcul.
  Si `False`, la somme renverra `NaN` si la Series contient au moins une valeur manquante.
* `level` (int ou nom, optionnel)
  Pour les Series avec **MultiIndex**, permet de calculer la somme le long d’un **niveau spécifique de l’index**.
* `min_count` (int, optionnel, défaut 0)
  Nombre minimum de valeurs non-NA requises pour effectuer le calcul.
  Si ce nombre n’est pas atteint, le résultat est `NaN`.

**Retour :**
* Retourne un **scalaire** représentant la **somme des valeurs de la Series** si level n’est pas utilisé.
* Si `level` est utilisé sur une Series avec **MultiIndex**, retourne une **Series** contenant les sommes par niveau d’index.
* Si `skipna=False` et qu’il y a au moins une valeur `NaN`, le retour sera `NaN`

**Notes importantes :**
* `s.sum()` est **vectorisé** et donc beaucoup plus rapide que `sum(list(s))`.
* Les valeurs `NaN` sont **ignorées par défaut**.
* Peut être utilisé pour les **Series numériques**, et parfois sur les Series de type `timedelta` ou booléen (`True`=1, `False`=0).

---

#### `s.mean()` <a id="smean-"></a>

La méthode `mean()` permet de **calculer la moyenne arithmétique des éléments d’une Series**.
Comme les autres opérations pandas, elle est **vectorisée**, ce qui la rend très performante même sur de grands ensembles de données.

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

# Calcul de la moyenne
m = s.mean()
print(m)  # 25.0
```

**Paramètres principaux :**
* `axis` (0 ou `'index'`, optionnel, défaut `0`)
  Identique à `sum()`, ce paramètre n’a **pas vraiment d’effet pour une Series**, mais reste présent pour compatibilité avec les DataFrame.
* `skipna` (bool, optionnel, défaut `True`)
  Contrôle la gestion des valeurs manquantes (`NaN`).
  * Si `True`, les `NaN` sont **ignorés** dans le calcul de la moyenne.
  * Si `False`, la présence d’un seul `NaN` rendra le résultat **`NaN`**.
* `level` (int ou nom, optionnel)
  Pour une Series avec **MultiIndex**, calcule la moyenne **par niveau d’index**, ce qui renvoie une nouvelle Series.
* `numeric_only` (bool, optionnel, défaut `False`)
  Ne concerne que les structures mixtes (typiquement les DataFrames).
  Pour une Series, ce paramètre est généralement inutile : elle ne contient qu’un seul type de données.

**Retour :**
* Retourne un **float** représentant la **moyenne des valeurs** de la Series.
* Si `level` est spécifié et que la Series possède un MultiIndex, retourne une **Series regroupée par niveau**.
* Si `skipna=False` et qu’un `NaN` est présent, le résultat sera **`NaN`**.
* Si la Series ne contient **aucune valeur numérique** ou uniquement des `NaN`, le résultat est **`NaN`**.

**Notes importantes :**
* `s.mean()` est **vectorisé et optimisé en C**, donc très rapide comparé à `sum(s)/len(s)` en Python pur.
* Les `NaN` sont **ignorés par défaut**, ce qui peut éviter des erreurs en analyse statistique.
* Fonctionne sur les Series :
  * **numériques**
  * **booléennes** (`True` = 1, `False` = 0)
  * **timedelta** (renvoie une moyenne temporelle)

---

#### `s.median()` <a id="smedian-"></a>

La méthode `median()` permet de **calculer la médiane** d’une Series, c’est-à-dire la **valeur centrale** lorsque les données sont triées.
Comme les autres opérations statistiques de pandas, elle est **vectorisée** et utilise des algorithmes optimisés, ce qui garantit rapidité et précision.

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

# Calcul de la médiane
m = s.median()
print(m)  # 25.0
```

**Paramètres principaux :**
* `axis` (0 ou `'index'`, optionnel, défaut `0`)
  Sans effet pratique sur une Series (plus utile dans un DataFrame).
  Présent pour maintenir la cohérence API.
* `skipna` (bool, optionnel, défaut `True`)
  * Si `True`, les valeurs manquantes (`NaN`) sont **ignorées**.
  * Si `False`, la présence d’un seul `NaN` rendra le résultat **`NaN`**.
* `numeric_only` (bool, optionnel, défaut `False`)
  Concerne surtout les DataFrame avec plusieurs colonnes.
  Pour une Series, ce paramètre n’a généralement pas d’impact.

**Retour :**
* Retourne un **scalaire** (int, float ou timedelta) correspondant à la **médiane des valeurs**.
* Si la Series contient uniquement des valeurs `NaN`, le résultat est **`NaN`**.
* Si une Series possède un nombre *pair* d’éléments, la médiane est la **moyenne des deux valeurs centrales**.

**Notes importantes :**
* `s.median()` trie virtuellement les données via un algorithme optimisé (type **QuickSelect**) — il ne s’agit pas d’un tri Python classique.
* Pour une Series **pair** en longueur :
  ex. `[10, 20, 30, 40]` → médiane = `(20 + 30) / 2 = 25.0`
* Les `NaN` sont **ignorés par défaut**, ce qui est généralement souhaitable en analyse statistique.
* Fonctionne sur :
  * **données numériques**
  * **timedelta**
  * **booléens** (où `True=1`, `False=0` → médiane logique)

---

Voici la version détaillée pour **`s.max()`**, suivant exactement le même format :

---

#### `s.max()` <a id="smax-"></a>

La méthode `max()` permet de **retourner la valeur maximale** d’une Series.
Elle est **vectorisée**, donc très rapide même sur de grands ensembles de données, et ignore automatiquement les valeurs manquantes (`NaN`) par défaut.

```python
import pandas as pd

s = pd.Series([10, 50, 30, 40])

# Valeur maximale
m = s.max()
print(m)  # 50
```

**Paramètres principaux :**
* **`axis`** (0 ou `'index'`, optionnel, défaut `0`)
  Sans impact réel pour une Series.
  Utilisé surtout dans les DataFrame.
* **`skipna`** (bool, optionnel, défaut `True`)
  * Si `True` : les valeurs `NaN` sont **ignorées**.
  * Si `False` : si la Series contient un seul `NaN`, le résultat sera **`NaN`**.
* **`numeric_only`** (bool, optionnel)
  N’a pas d’impact pour les Series (utile pour filtrer des colonnes non numériques dans un DataFrame).

**Retour :**
* Retourne un **scalaire** correspondant à la **valeur maximale**.
* Si toutes les valeurs sont `NaN`, renvoie **`NaN`**.
* Peut retourner :

  * un int / float
  * un timestamp (`datetime64`)
  * un timedelta
  * une chaîne de caractères (selon l’ordre lexicographique)

**Notes importantes :**

* `s.max()` fonctionne pour différents types :
  * **Numérique** → maximum mathématique
  * **Datetime** → date la plus récente
  * **Timedelta** → durée la plus longue
  * **Objet / string** → comparaison lexicographique (`"z"` > `"a"`)
* Elle est **vectorisée**, donc très rapide, et repose sur des routines NumPy hautes performances.
* Si vous voulez obtenir aussi la position du maximum, utilisez :
  * `s.idxmax()` → retourne l’index associé à la valeur maximale
* Si `skipna=False` et qu’une seule valeur est `NaN` → résultat = **`NaN`**

---
Voici la version détaillée pour **`s.min()`**, dans le même format que précédemment :

---

#### `s.min()` <a id="smin-"></a>

La méthode `min()` permet de **retourner la valeur minimale** d’une Series.
Elle est **vectorisée**, utilisant des algorithmes optimisés (NumPy), ce qui la rend extrêmement rapide même sur des millions de lignes.

```python
import pandas as pd

s = pd.Series([10, 50, 30, 40])

# Valeur minimale
m = s.min()
print(m)  # 10
```

**Paramètres principaux :**
* `axis` (0 ou `'index'`, optionnel, défaut `0`)
  Sans effet pour une Series (utilisé surtout dans les DataFrame).

* `skipna` (bool, optionnel, défaut `True`)
  * Si `True`, les `NaN` sont **ignorés**.
  * Si `False`, la présence d’un seul `NaN` rendra la valeur retournée **`NaN`**.
* `numeric_only` (bool, optionnel)
  Inutile pour une Series (utile pour DataFrame avec colonnes non numériques).

**Retour :**
* Retourne un **scalaire** correspondant à la **valeur minimale** de la Series.
* Si toutes les valeurs sont `NaN`, le résultat est **`NaN`**.
* Peut retourner :

  * un int / float
  * un timestamp (`datetime64`)
  * un timedelta
  * une chaîne (`string`) en suivant l’ordre lexicographique ( `"a"` < `"z"` )

**Notes importantes :**
* Fonctionne avec différents types :
  * **Numérique** → minimum mathématique
  * **Datetime** → date la plus ancienne
  * **Timedelta** → la plus petite durée
  * **Objet / string** → comparaison lexicographique (`"apple"` < `"zoo"`)
* Très performant grâce aux opérations **vectorisées** basées sur NumPy.
* Pour obtenir l’index du minimum, utilisez :
  * `s.idxmin()` → retourne l’index de la plus petite valeur
* Comportement avec les `NaN` :
  * ignorés par défaut (`skipna=True`)
  * propagés si `skipna=False`

---

#### `s.idxmax()` <a id="sidxmax-"></a>

La méthode `idxmax()` permet de **retourner l’index associé à la valeur maximale** d’une Series.
Contrairement à `s.max()` qui renvoie la valeur, `s.idxmax()` renvoie **l’étiquette d’index** où se trouve cette valeur.
Elle ignore automatiquement les `NaN` par défaut et utilise des opérations vectorisées très rapides.

```python
import pandas as pd

s = pd.Series([10, 50, 30, 40], index=["a", "b", "c", "d"])

# Index de la valeur maximale
idx = s.idxmax()
print(idx)  # 'b'
```

**Paramètres principaux :**

* `axis` (0 ou `'index'`, optionnel, défaut `0`)
  Inclus pour compatibilité avec l’API pandas, mais n’a aucun impact sur une Series.
* `skipna` (bool, optionnel, défaut `True`)
  * Si `True`, les `NaN` sont **ignorés** dans la recherche du maximum.
  * Si `False`, si la Series contient au moins un `NaN`, le résultat sera **`NaN`**.

**Retour :**
* Retourne un **scalaire** représentant **l’index** (label) de la valeur maximale.
* Types possibles :
  * string
  * entier
  * datetime index
  * niveau d’un MultiIndex
* Si la Series est entièrement composée de valeurs `NaN`, lèvera une **ValueError** :
  ```
  ValueError: attempt to get argmax of an empty sequence
  ```

**Notes importantes :**

* `idxmax()` renvoie **l’index**, pas la valeur maximale elle-même.
  Pour la valeur, il faut utiliser `s.max()`.
* Si plusieurs valeurs sont égales au maximum, **l’index du premier max** rencontré sera retourné.
* Fonctionne avec :
  * données numériques
  * dates (`datetime64`)
  * timedelta
  * chaînes de caractères (`max` basé sur ordre lexicographique)
* Comportement avec les `NaN` :
  * ignorés par défaut
  * si `skipna=False`, renvoie `NaN` même si une valeur max existe
* Souvent utilisé conjointement avec `idxmin()` pour localiser les extrêmes statistiquement.

---
Voici la version détaillée pour **`s.idxmin()`**, dans le même format que `s.idxmax()` :

---

### `s.idxmin()` <a id="sidxmin-"></a>

La méthode `idxmin()` permet de **retourner l’index associé à la valeur minimale** d’une Series.
Contrairement à `s.min()` qui renvoie la valeur, `s.idxmin()` renvoie **l’étiquette d’index** correspondant à cette valeur minimale.
Elle est **vectorisée** et ignore par défaut les `NaN`.

```python
import pandas as pd

s = pd.Series([10, 50, 30, 40], index=["a", "b", "c", "d"])

# Index de la valeur minimale
idx = s.idxmin()
print(idx)  # 'a'
```

**Paramètres principaux :**

* `axis` (0 ou `'index'`, optionnel, défaut `0`)
  Inclus pour compatibilité API pandas ; n’a pas d’effet sur une Series.

* `skipna` (bool, optionnel, défaut `True`)
  * Si `True`, les valeurs `NaN` sont **ignorées** lors de la recherche du minimum.
  * Si `False`, et qu’au moins un `NaN` est présent, le résultat sera **`NaN`**.

**Retour :**

* Retourne un **scalaire** représentant **l’index** de la valeur minimale.
* Types possibles :
  * string
  * int
  * datetime index
  * niveau d’un MultiIndex
* Si la Series est entièrement composée de `NaN`, une **ValueError** est levée :
  ```
  ValueError: attempt to get argmin of an empty sequence
  ```

**Notes importantes :**

* `idxmin()` renvoie **l’index**, pas la valeur minimale elle-même. Pour la valeur, utilisez `s.min()`.
* Si plusieurs valeurs sont égales au minimum, **l’index du premier minimum** rencontré sera retourné.
* Fonctionne sur :
  * données numériques
  * dates (`datetime64`)
  * timedelta
  * chaînes de caractères (min basé sur ordre lexicographique)
* Les `NaN` sont ignorés par défaut.
* Souvent utilisé avec `idxmax()` pour localiser rapidement les extrêmes d’une Series.

---

#### `s.std()` <a id="sstd-"></a>

La méthode `std()` permet de **calculer l’écart-type** d’une Series, c’est-à-dire la **dispersion des valeurs autour de la moyenne**.
Elle est **vectorisée** et optimisée pour traiter de grandes Series rapidement.

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

# Calcul de l'écart-type
écart_type = s.std()
print(écart_type)  # 12.909944487358056
```

**Paramètres principaux :**
* `axis` (0 ou `'index'`, optionnel, défaut `0`)
  Sans effet pour une Series (utile principalement pour les DataFrame).
* `skipna` (bool, optionnel, défaut `True`)
  * Si `True` : les valeurs manquantes (`NaN`) sont **ignorées** dans le calcul.
  * Si `False` : la présence d’un `NaN` rendra le résultat **`NaN`**.
* `level` (int ou nom, optionnel)
  Pour les Series avec **MultiIndex**, calcule l’écart-type **par niveau d’index**, et retourne une Series.
* `ddof` (int, optionnel, défaut `1`)
  Le degré de liberté utilisé dans le calcul.
  * `ddof=1` → écart-type **échantillon** (par défaut)
  * `ddof=0` → écart-type **population**

**Retour :**
* Retourne un **float** représentant l’écart-type de la Series.
* Si `level` est spécifié, retourne une **Series** avec l’écart-type calculé par niveau.
* Si toutes les valeurs sont `NaN`, retourne **`NaN`**.

**Notes importantes :**
* L’écart-type est calculé selon la formule classique :

[
\sigma = \sqrt{\frac{\sum (x_i - \bar{x})^2}{n - ddof}}
]

* `s.std(ddof=1)` → écart-type d’échantillon (par défaut)
* `s.std(ddof=0)` → écart-type population
* Les valeurs `NaN` sont ignorées par défaut (`skipna=True`).
* Peut être utilisé sur :
  * **données numériques**
  * **booléens** (`True=1`, `False=0`)
  * **timedelta** pour dispersion temporelle.

---

#### `s.describe()` <a id="sdescribe-"></a>

La méthode `describe()` fournit un **résumé statistique complet** d’une Series.
Elle est très utile pour obtenir rapidement des informations descriptives sur les données, comme le **compte, la moyenne, l’écart-type, les quartiles, le minimum et le maximum**.
Pour les Series non numériques, elle fournit des informations sur les valeurs uniques et la fréquence de la valeur la plus fréquente.

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40, 50])

# Résumé statistique
résumé = s.describe()
print(résumé)
```

**Exemple de sortie :**
```
count     5.0
mean     30.0
std      15.811388
min      10.0
25%      20.0
50%      30.0
75%      40.0
max      50.0
dtype: float64
```

**Paramètres principaux :**
* `percentiles` (list-like, optionnel, défaut `[0.25, 0.5, 0.75]`)
  Liste des percentiles à inclure dans le résumé. Peut être personnalisé.
* `include` / `exclude` (optionnel)
  Utilisés surtout pour les DataFrames pour inclure ou exclure certaines colonnes selon le type de données.
  Pour une Series, ces paramètres sont généralement ignorés.
* `datetime_is_numeric` (bool, optionnel, défaut `False`)
  Si `True`, les colonnes datetime sont traitées comme des nombres pour les calculs statistiques.

**Retour :**
* Une **Series** contenant le résumé statistique.
  * Pour **Series numériques** : `count`, `mean`, `std`, `min`, `25%`, `50%`, `75%`, `max`
  * Pour **Series non numériques** : `count`, `unique`, `top`, `freq`
* Chaque valeur est un **scalaire** représentant le calcul correspondant.

**Notes importantes :**
* Très utile pour une **analyse exploratoire rapide** des données.
* Pour les Series numériques, les valeurs `NaN` sont **ignorées** par défaut.
* Les percentiles par défaut sont les **quartiles**, mais peuvent être personnalisés.
* Peut être combiné avec des filtres ou des méthodes comme `loc` pour analyser des sous-ensembles de données.

---

### Conversion Series ↔ DataFrame <a id="conversion-series-dataframe-"></a>

```python
df = s.to_frame(name="valeurs")  # Series → DataFrame
s3 = df["valeurs"]               # DataFrame → Series
```

---

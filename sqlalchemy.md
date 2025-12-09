# Notebook pour SQLAlchemy

## Table of Contents

- [Notebook pour SQLAlchemy](#notebook-pour-sqlalchemy)
  - [Table of Contents](#table-of-contents)
  - [Introduction / Description ](#introduction--description-)
    - [Présentation de SQLAlchemy ](#présentation-de-sqlalchemy-)
      - [Objectif ](#objectif-)
      - [Fonctionnalités principales ](#fonctionnalités-principales-)
  - [Installation / Import ](#installation--import-)
    - [Installation de SQLAlchemy ](#installation-de-sqlalchemy-)
    - [Importer SQLAlchemy ](#importer-sqlalchemy-)
  - [Création de la base de données ](#création-de-la-base-de-données-)
    - [`Engine` ](#engine-)
  - [`Session` ](#session-)
    - [`sessionmaker()` ](#sessionmaker-)
    - [Méthodes principales de `Session` ](#méthodes-principales-de-session-)
      - [`add(obj)` ](#addobj-)
      - [`add_all(objs)` ](#add_allobjs-)
      - [`commit()` ](#commit-)
      - [`rollback()` ](#rollback-)
      - [`close()` ](#close-)
      - [`query(*entities)` ](#queryentities-)
      - [`delete(obj)` ](#deleteobj-)
      - [`refresh(obj)` ](#refreshobj-)
      - [`flush(obj)` ](#flushobj-)
  - [Forcer l’exécution d’une requête dépendante](#forcer-lexécution-dune-requête-dépendante)
      - [`expunge(obj)` ](#expungeobj-)
      - [`merge(obj)` ](#mergeobj-)
      - [`expire(obj)` ](#expireobj-)
      - [`get(entity, ident)` ](#getentity-ident-)
      - [`execute(statement)` ](#executestatement-)
      - [`scalar(statement)` ](#scalarstatement-)
      - [`scalars(statement)` ](#scalarsstatement-)
      - [`begin()` ](#begin-)
      - [`begin_nested()` ](#begin_nested-)
      - [`in_transaction()` ](#in_transaction-)
  - [Définition des modèles ](#définition-des-modèles-)
    - [`Base` et `Table` ](#base-et-table-)
    - [Colonnes et types ](#colonnes-et-types-)
  - [Opérations CRUD ](#opérations-crud-)
    - [Create (Créer des enregistrements) ](#create-créer-des-enregistrements-)
    - [Read (Lire des données) ](#read-lire-des-données-)
    - [Update (Modifier des enregistrements) ](#update-modifier-des-enregistrements-)
    - [Delete (Supprimer des enregistrements) ](#delete-supprimer-des-enregistrements-)
    - [Tips importants pour CRUD :](#tips-importants-pour-crud-)
  - [Relations entre tables ](#relations-entre-tables-)
    - [`relationship()` ](#relationship-)
    - [ForeignKey et relationship ](#foreignkey-et-relationship-)
    - [Types de relations ](#types-de-relations-)
  - [Requêtes avancées et jointures ](#requêtes-avancées-et-jointures-)
    - [Filtrage avec `filter()` et `filter_by()` ](#filtrage-avec-filter-et-filter_by-)
    - [Tri avec `order_by()` ](#tri-avec-order_by-)
    - [Jointures avec `join()` ](#jointures-avec-join-)
    - [Jointures externes (`outerjoin`) ](#jointures-externes-outerjoin-)
    - [Groupements et agrégations ](#groupements-et-agrégations-)
    - [Filtres avancés et combinés ](#filtres-avancés-et-combinés-)

---
---

## Introduction / Description <a id="introduction--description-"></a>

### Présentation de SQLAlchemy <a id="présentation-de-sqlalchemy-"></a>

SQLAlchemy est une **bibliothèque Python open-source** pour travailler avec des bases de données relationnelles de manière **structurée et efficace**.
Elle fournit **un ORM (Object Relational Mapper)** permettant de manipuler des bases de données avec des objets Python, ainsi qu’une **API SQL Expression Language** pour écrire des requêtes SQL de manière programmatique.

#### Objectif <a id="objectif-"></a>

SQLAlchemy vise à :

* Simplifier la connexion et l’interaction avec différents SGBD (PostgreSQL, MySQL, SQLite…)
* Fournir un ORM complet pour manipuler les données via des objets Python
* Permettre la construction de requêtes SQL complexes de manière lisible et sûre
* Garantir la portabilité du code entre différents systèmes de base de données

#### Fonctionnalités principales <a id="fonctionnalités-principales-"></a>

* ORM complet avec mapping des classes Python aux tables
* Génération automatique de schéma et migrations possibles avec Alembic
* Requêtes SQL composables et sécurisées
* Support des transactions et sessions
* Compatibilité avec la plupart des SGBD relationnels
* Gestion avancée des relations (One-to-Many, Many-to-Many)
* Requêtes SQL optimisées pour performance et flexibilité

---
---

## Installation / Import <a id="installation--import-"></a>

### Installation de SQLAlchemy <a id="installation-de-sqlalchemy-"></a>

Installez SQLAlchemy avec pip :

```bash
pip install SQLAlchemy
```

Si vous utilisez un environnement virtuel, assurez-vous qu’il est activé avant l’installation.

Pour certains SGBD comme PostgreSQL ou MySQL, vous aurez besoin d’installer également le driver correspondant :

```bash
pip install psycopg2  # pour PostgreSQL
pip install pymysql    # pour MySQL
```

### Importer SQLAlchemy <a id="importer-sqlalchemy-"></a>

Dans votre script Python, importez les modules nécessaires :

```python
from sqlalchemy import create_engine, Column, Integer, String, ForeignKey
from sqlalchemy.orm import declarative_base, sessionmaker, relationship
```

---
---

## Création de la base de données <a id="création-de-la-base-de-données-"></a>

### `Engine` <a id="engine-"></a>

L’**Engine** est le point d’entrée vers la base de données. Il gère la connexion et permet d’exécuter des requêtes SQL.

```python
from sqlalchemy import create_engine

# Création d'un engine SQLite en mémoire
engine = create_engine("sqlite:///:memory:", echo=True)
```

**Paramètres :**

* `url` (str) : chaîne de connexion vers la base de données.
  Exemples :

  * SQLite : `"sqlite:///nom_base.db"`
  * PostgreSQL : `"postgresql+psycopg2://user:password@host:port/dbname"`
  * MySQL : `"mysql+pymysql://user:password@host:port/dbname"`
* `echo` (bool, optionnel) : si `True`, affiche toutes les requêtes SQL exécutées pour debug.
* `connect_args` (dict, optionnel) : arguments supplémentaires transmis au driver (ex : `{"check_same_thread": False}` pour SQLite).
* `pool_size`, `max_overflow` (int, optionnel) : paramètres pour la gestion du pool de connexions.

**Retour :** un objet `Engine` permettant de se connecter et d’exécuter des requêtes.

**Notes :**
* L’Engine **ne crée pas automatiquement les tables**, il sert uniquement de connecteur.
* Peut être utilisé avec `Session` pour gérer les transactions.

---
---

## `Session` <a id="session-"></a>

La **Session** est le point central pour interagir avec l’ORM SQLAlchemy. Elle **gère les transactions, les objets persistants et les requêtes**.

```python
from sqlalchemy.orm import sessionmaker, Session

SessionLocal = sessionmaker(bind=engine)
session = SessionLocal()
```
---

### `sessionmaker()` <a id="sessionmaker-"></a>

`sessionmaker()` est une **fabrique de sessions** dans SQLAlchemy. Elle permet de créer des objets `Session` configurés avec des paramètres par défaut (liaison à l’engine, comportement de flush/commit, expiration des objets, etc.). Cela facilite la création et la réutilisation des sessions dans votre application.

```python
from sqlalchemy.orm import sessionmaker

# Création d'une fabrique de sessions liée à l'engine
SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=True,
    expire_on_commit=True,
    class_=Session,
    info=None
)

# Création d'une session
session = SessionLocal()
```

**Paramètres principaux :**

* `bind` (`Engine` ou `Connection`, optionnel)
  L’engine ou la connexion à utiliser pour cette session. Si non fourni, il faudra le passer lors de la création de la session.
* `class_` (type, optionnel, défaut `Session`)
  La **classe de session** à instancier. Par défaut, `Session` de SQLAlchemy est utilisée, mais il est possible de fournir une sous-classe personnalisée.
* `autocommit` (bool, optionnel, défaut `False`)
  Si `True`, les transactions sont automatiquement validées après chaque opération.
  ⚠️ Généralement déconseillé car cela peut entraîner des incohérences.
* `autoflush` (bool, optionnel, défaut `True`)
  Si `True`, toutes les modifications en attente sont automatiquement envoyées à la base de données avant certaines opérations de requête.
  Cela garantit que les objets lus depuis la session reflètent les dernières modifications.
* `expire_on_commit` (bool, optionnel, défaut `True`)
  Si `True`, les objets deviennent **expirés** après `commit()`, ce qui force leur rechargement depuis la base de données lorsqu’ils sont à nouveau utilisés.
  Utile pour garantir que les données sont toujours à jour.
* `info` (dict, optionnel)
  Un dictionnaire pouvant contenir des **métadonnées arbitraires** liées à la session.
  Peut servir à stocker des informations contextuelles ou spécifiques à l’application.
* `query_cls` (classe, optionnel)
  Permet de définir une **classe de requête personnalisée** pour `session.query()`.
* `future` (bool, optionnel, défaut `False`)
  Active certaines fonctionnalités du moteur de SQLAlchemy **version 2.0** pour la session.
  Exemple : meilleure gestion des transactions, API simplifiée, compatibilité future.
* `info` (dict, optionnel)
  Permet de stocker des informations arbitraires dans la session (métadonnées utiles pour le contexte de l’application).

**Retour :** Une **fabrique de session** (callable) qui génère des objets `Session` configurés selon les paramètres fournis.

**Exemple complet d’utilisation :**

```python
from sqlalchemy.orm import sessionmaker, Session

# Création d'une fabrique de sessions
SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=True,
    expire_on_commit=True,
    class_=Session,
    info={"app": "MonApp"}
)

# Création d'une session
session = SessionLocal()

# Ajouter un utilisateur
nouvel_utilisateur = Utilisateur(nom="Alice")
session.add(nouvel_utilisateur)
session.commit()

# Requête
user = session.query(Utilisateur).filter_by(nom="Alice").first()
print(user.nom)

# Fermeture de la session
session.close()
```

**Notes importantes :**

* `sessionmaker()` ne crée pas une session immédiatement : elle retourne un **callable** que l’on utilise pour instancier une session réelle.
* Permet de créer facilement plusieurs sessions avec la **même configuration**.
* Combinez-la souvent avec un contexte `with` pour gérer proprement l’ouverture et la fermeture des sessions :

```python
with SessionLocal() as session:
    user = session.query(Utilisateur).first()
    session.commit()  # si nécessaire
```
---

### Méthodes principales de `Session` <a id="méthodes-principales-de-session-"></a>


#### `add(obj)` <a id="addobj-"></a>
Ajoute un objet à la session pour qu’il soit inséré dans la base de données lors du prochain `commit()`.

```python
nouvel_utilisateur = Utilisateur(nom="Alice")
session.add(nouvel_utilisateur)
session.commit()
```

**Paramètres :**

* `obj` : instance de modèle SQLAlchemy.

**Retour :** aucun.

**Notes :**
* L’objet est suivi par la session et synchronisé avec la base à la validation.

---

#### `add_all(objs)` <a id="add_allobjs-"></a>

Ajoute plusieurs objets à la session en une seule opération.

```python
session.add_all([
    Utilisateur(nom="Bob"),
    Utilisateur(nom="Charlie")
])
session.commit()
```

**Paramètres :**
* `objs` : liste d’instances de modèles SQLAlchemy.

**Retour :** aucun.

**Notes :**
* Pratique pour insérer plusieurs objets simultanément.

---

#### `commit()` <a id="commit-"></a>

Valide toutes les modifications effectuées dans la session (insertions, mises à jour, suppressions).

```python
session.commit()
```

**Paramètres :** aucun.

**Retour :** aucun.

**Notes :**
* Toutes les opérations effectuées depuis le dernier commit ou rollback sont **persistées en base**.
* Les objets expirent si `expire_on_commit=True`.

---

#### `rollback()` <a id="rollback-"></a>

Annule toutes les modifications en attente dans la session, ramenant l’état des objets à la dernière version en base.

```python
session.rollback()
```

**Paramètres :** aucun.

**Retour :** aucun.

**Notes :**
* Utile pour gérer les erreurs ou exceptions avant de revalider.

---

#### `close()` <a id="close-"></a>

Ferme la session et libère la connexion à la base de données.

```python
session.close()
```

**Paramètres :** aucun.

**Retour :** aucun.

**Notes :**
* Toujours fermer les sessions après utilisation pour éviter les fuites de connexions.
* Peut être utilisé avec un contexte `with` pour fermeture automatique.

```python
with SessionLocal() as session:
    user = session.query(Utilisateur).first()
```

---

#### `query(*entities)` <a id="queryentities-"></a>

Prépare une **requête ORM** pour interroger la base de données sur un ou plusieurs modèles.

```python
utilisateurs = session.query(Utilisateur).filter_by(nom="Alice").all()
```

**Paramètres :**
* `*entities` : un ou plusieurs modèles SQLAlchemy ou colonnes.

**Retour :** objet `Query` pour filtrer, trier, limiter ou exécuter la requête.

**Notes :**
* La méthode `query()` est souvent combinée avec `.filter()`, `.filter_by()`, `.order_by()`, `.all()`, `.first()`.

---

#### `delete(obj)` <a id="deleteobj-"></a>

Supprime un objet de la base de données.

```python
session.delete(utilisateur)
session.commit()
```

**Paramètres :**
* `obj` : instance du modèle à supprimer.

**Retour :** aucun.

**Notes :**
* L’objet est supprimé lors du prochain `commit()`.

---

#### `refresh(obj)` <a id="refreshobj-"></a>

Recharge un objet depuis la base de données, écrasant les modifications non validées.

```python
session.refresh(utilisateur)
```

**Paramètres :**
* `obj` : instance à recharger.

**Retour :** aucun.

**Notes :**
* Utile si la base a été modifiée par une autre session et que vous voulez récupérer la valeur la plus récente.

---
#### `flush(obj)` <a id="flushobj-"></a>

Envoie les modifications à la base sans valider la transaction.

session.flush()

Sert à :

Obtenir des IDs générés automatiquement avant un commit

Forcer l’exécution d’une requête dépendante
---

#### `expunge(obj)` <a id="expungeobj-"></a>

Retire un objet de la session, **il n’est plus suivi**.

```python
session.expunge(utilisateur)
```

**Paramètres :**

* `obj` : instance à retirer de la session.

**Retour :** aucun.

**Notes :**

* L’objet ne sera pas synchronisé avec la base tant qu’il n’est pas ré-ajouté à la session.

---

#### `merge(obj)` <a id="mergeobj-"></a>

Intègre un objet détaché (non suivi) à la session en créant ou mettant à jour un objet suivi.

```python
utilisateur_detache = Utilisateur(id=1, nom="Alice modifié")
session.merge(utilisateur_detache)
session.commit()
```

**Paramètres :**
* `obj` : instance du modèle à intégrer dans la session.

**Retour :** une instance attachée à la session.

**Notes :**
* Très utile pour synchroniser des objets provenant d’une autre session ou d’un processus différent.

---

#### `expire(obj)` <a id="expireobj-"></a>

Expire un objet pour forcer son rechargement depuis la base au prochain accès.

```python
session.expire(utilisateur)
```

**Paramètres :**
* `obj` : instance à expirer.

**Retour :** aucun.

**Notes :**
* Utile pour s’assurer que les données affichées sont à jour.

---

#### `get(entity, ident)` <a id="getentity-ident-"></a>

Récupère un objet par sa **clé primaire**.

```python
user = session.get(Utilisateur, 1)
```

**Paramètres :**
* `entity` : classe du modèle.
* `ident` : valeur de la clé primaire.

**Retour :** instance du modèle ou `None`.

**Notes :**
* Méthode simple et rapide pour récupérer un objet unique par ID.

---

#### `execute(statement)` <a id="executestatement-"></a>

Exécute des requêtes SQL ou ORM modernes (SQLAlchemy 2.0).

```python
from sqlalchemy import select
result = session.execute(select(Utilisateur))
```

**Paramètres :**
* `statement` : objet SQL (select, insert, update, text…)

**Retour :** `Result`.

**Notes :**
* Interface de requête recommandée en SQLAlchemy 2.x.

---

#### `scalar(statement)` <a id="scalarstatement-"></a>

Renvoie la **première colonne du premier résultat**.

```python
count = session.scalar(select(func.count(Utilisateur.id)))
```

---

#### `scalars(statement)` <a id="scalars-"></a>

Renvoie un itérable contenant uniquement la première colonne de chaque ligne.

```python
names = session.scalars(select(Utilisateur.nom))
```

---

#### `begin()` <a id="begin-"></a>

Ouvre une transaction explicite.

```python
with session.begin():
    session.add(User(name="Pierre"))
```

---

#### `begin_nested()` <a id="begin_nested-"></a>

Crée un **SAVEPOINT** (transaction imbriquée).

```python
session.begin_nested()
```

---

#### `in_transaction()` <a id="in_transaction-"></a>

Indique si une transaction est en cours.

```python
session.in_transaction()
```

---
---

## Définition des modèles <a id="définition-des-modèles-"></a>

### `Base` et `Table` <a id="base-et-table-"></a>
SQLAlchemy utilise une **classe de base** pour déclarer les modèles (tables). Chaque modèle hérite de cette base.

```python
from sqlalchemy.orm import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class Utilisateur(Base):
    __tablename__ = "utilisateurs"  # Nom de la table

    id = Column(Integer, primary_key=True, autoincrement=True)
    nom = Column(String, nullable=False)
    age = Column(Integer)
```

**Paramètres principaux :**
* `__tablename__` (str) : Nom de la table en base.
* `Base` : classe de base créée par `declarative_base()` qui permet le mapping ORM.
* Chaque attribut du modèle est une **colonne** : `Column(type, options...)`.

**Retour :** La classe devient un **modèle ORM** pouvant être utilisée avec `Session` pour CRUD.

**Notes :**

* Les classes héritent de `Base` pour que SQLAlchemy sache qu’elles représentent une table.
* Les instances de ces classes correspondent à une **ligne** dans la table.

---

### Colonnes et types <a id="colonnes-et-types-"></a>
Les colonnes définissent les champs de la table avec leur type et leurs contraintes.

```python
from sqlalchemy import Integer, String, Boolean, Float, Date, DateTime, ForeignKey

class Article(Base):
    __tablename__ = "articles"

    id = Column(Integer, primary_key=True)
    titre = Column(String(100), nullable=False)
    contenu = Column(String)
    prix = Column(Float, default=0.0)
    publie = Column(Boolean, default=True)
    date_creation = Column(DateTime)
    utilisateur_id = Column(Integer, ForeignKey("utilisateurs.id"))
```

**Types de colonnes courants :**
* `Integer` : entier
* `String(length)` : texte avec longueur max
* `Text` : texte long
* `Boolean` : booléen True/False
* `Float` : nombre flottant
* `Date` / `Time` / `DateTime` : dates et heures
* `ForeignKey("table.colonne")` : clé étrangère

**Options possibles pour `Column` :**
* `primary_key` (bool) : clé primaire
* `nullable` (bool) : autorise ou non la valeur `NULL`
* `unique` (bool) : doit être unique
* `default` : valeur par défaut
* `autoincrement` (bool) : incrément automatique (pour entiers)
* `index` (bool) : crée un index sur la colonne
* `ForeignKey` : référence une autre table pour relations

**Notes :**
* Les relations entre tables se définissent via `ForeignKey` et `relationship()` (ORM).
* Chaque colonne peut avoir des contraintes et des options adaptées à la logique métier.

---
---

## Opérations CRUD <a id="opérations-crud-"></a>

### Create (Créer des enregistrements) <a id="create-créer-des-enregistrements-"></a>

Pour **insérer des lignes** dans une table, on crée des instances du modèle et on les ajoute à la session.

```python
from datetime import datetime

# Création d'un utilisateur
nouvel_utilisateur = Utilisateur(nom="Alice", age=30)

# Ajout à la session
session.add(nouvel_utilisateur)
session.commit()  # Validation dans la base

# Plusieurs objets à la fois
utilisateurs = [
    Utilisateur(nom="Bob", age=25),
    Utilisateur(nom="Charlie", age=35)
]
session.add_all(utilisateurs)
session.commit()
```

**Notes importantes :**

* `add(obj)` ajoute un objet à la session.
* `add_all([objs])` ajoute plusieurs objets simultanément.
* **Commit** valide les changements dans la base.
* Sans `commit()`, les objets restent dans la session mais ne sont pas enregistrés.

---

### Read (Lire des données) <a id="read-lire-des-données-"></a>

Pour **lire ou récupérer des enregistrements**, on utilise `query()` avec filtres ou conditions.

```python
# Import des fonctions SQLAlchemy
from sqlalchemy import select

# Récupérer tous les utilisateurs
utilisateurs = session.query(Utilisateur).all()
for u in utilisateurs:
    print(u.nom, u.age)

# Récupérer un utilisateur spécifique
alice = session.query(Utilisateur).filter_by(nom="Alice").first()
print(alice.nom, alice.age)

# Utilisation de filtres plus complexes
adultes = session.query(Utilisateur).filter(Utilisateur.age >= 30).all()
```

**Méthodes courantes :**
* `all()` : renvoie une liste de tous les résultats.
* `first()` : renvoie le premier résultat ou `None`.
* `filter(condition)` : filtre selon une condition (ex : `Utilisateur.age >= 30`).
* `filter_by(champ=valeur)` : filtre simple (égalité).
* `order_by(colonne)` : trie les résultats.
* `limit(n)` : limite le nombre de résultats.

---

### Update (Modifier des enregistrements) <a id="update-modifier-des-enregistrements-"></a>

Pour **mettre à jour des valeurs**, on récupère l’objet, on modifie ses attributs puis on fait un `commit()`.

```python
# Récupérer un utilisateur
alice = session.query(Utilisateur).filter_by(nom="Alice").first()

# Modifier l'âge
alice.age = 31
session.commit()
```

**Notes :**
* Toute modification sur un objet attaché à la session est **automatiquement détectée**.
* `commit()` valide les modifications dans la base.
* Pour annuler les changements avant commit, utiliser `session.rollback()`.

---

### Delete (Supprimer des enregistrements) <a id="delete-supprimer-des-enregistrements-"></a>

Pour **supprimer des lignes**, on récupère l’objet puis on utilise `delete()` ou `session.delete()`.

```python
# Supprimer un utilisateur
alice = session.query(Utilisateur).filter_by(nom="Alice").first()
session.delete(alice)
session.commit()

# Supprimer plusieurs utilisateurs avec filter
session.query(Utilisateur).filter(Utilisateur.age < 30).delete(synchronize_session='fetch')
session.commit()
```

**Notes :**
* `session.delete(obj)` supprime un objet spécifique.
* `query(Model).filter(...).delete()` permet de supprimer plusieurs lignes selon un filtre.
* Toujours **commit** pour appliquer la suppression en base.

---

### Tips importants pour CRUD :
* Toujours fermer la session après usage (`session.close()`).
* Utiliser des transactions pour plusieurs opérations sensibles pour éviter les incohérences.
* Pour des bases volumineuses, préférer les opérations en bulk (`add_all`, `delete` avec filtre) pour l’efficacité.
* SQLAlchemy ORM reflète la base dans vos objets Python, ce qui permet un code **propre et orienté objet**.

---
---

## Relations entre tables <a id="relations-entre-tables-"></a>

Parfait ! Voici une **description complète de `relationship()`** pour SQLAlchemy, dans le même format `.md` que tes autres sections :

---

### `relationship()` <a id="relationship-"></a>

Permet de **définir les relations entre les tables** dans SQLAlchemy ORM. Contrairement à `ForeignKey`, qui définit la contrainte au niveau de la base, `relationship()` **crée un lien logique dans l’ORM**, facilitant la navigation entre objets Python liés.

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class Utilisateur(Base):
    __tablename__ = "utilisateur"
    id = Column(Integer, primary_key=True)
    nom = Column(String)
    
    # Relation un-à-plusieurs avec Article
    articles = relationship("Article", back_populates="auteur")

class Article(Base):
    __tablename__ = "article"
    id = Column(Integer, primary_key=True)
    titre = Column(String)
    auteur_id = Column(Integer, ForeignKey("utilisateur.id"))
    
    # Relation inverse
    auteur = relationship("Utilisateur", back_populates="articles")
```

**Paramètres principaux :**
* `argument` (str ou classe) : nom de la classe liée ou référence à la classe.
* `back_populates` (str, optionnel) : nom de l’attribut dans la classe opposée pour créer la relation bidirectionnelle.
* `backref` (str ou BackRef, optionnel) : alternative à `back_populates`, crée automatiquement un attribut bidirectionnel.
* `uselist` (bool, optionnel) : `True` par défaut pour les relations plusieurs-à-un (listes), `False` pour une relation unique.
* `cascade` (str, optionnel) : définit le comportement de suppression ou mise à jour en cascade (`"all, delete-orphan"`, `"save-update"`, etc.).
* `lazy` (str, optionnel) : définit le **chargement des objets liés** :
  * `"select"` (par défaut) : charge à la demande via une requête SQL séparée.
  * `"joined"` : jointure SQL immédiate lors de la requête initiale.
  * `"subquery"` : utilise une sous-requête pour charger les objets liés.
  * `"noload"` : ne charge pas automatiquement.
  * `"dynamic"` : renvoie un objet Query pour filtrer les éléments liés sans les charger tous.
* `primaryjoin` / `secondaryjoin` (optionnel) : conditions SQL pour des relations complexes ou multi-tables.
* `remote_side` (optionnel) : utile pour les relations auto-référentielles (ex : arbre hiérarchique).
* `order_by` (Column ou liste, optionnel) : tri des objets liés.
* `viewonly` (bool, optionnel) : si `True`, la relation est en lecture seule (pas de cascade pour les insertions ou mises à jour).
* `foreign_keys` (Column ou liste, optionnel) : permet de spécifier explicitement les colonnes de clé étrangère dans les cas complexes.

**Retour :** un attribut de classe ORM permettant **d’accéder directement aux objets liés** comme des propriétés Python :

* Pour une relation un-à-plusieurs : une liste d’objets (`[Article, Article]`).
* Pour une relation un-à-un : un objet unique.

**Exemples d’utilisation :**

```python
# Accès aux articles d’un utilisateur
user = session.query(Utilisateur).first()
for art in user.articles:
    print(art.titre)

# Accès à l'auteur d'un article
article = session.query(Article).first()
print(article.auteur.nom)
```

**Notes importantes :**

* `relationship()` **ne crée pas de colonne** dans la base de données, c’est un mécanisme ORM.
* Pour créer la relation physique, utilisez toujours `ForeignKey`.
* Combine très bien avec `back_populates` pour créer des relations bidirectionnelles claires et synchronisées.
* Les options `lazy`, `cascade`, et `uselist` sont essentielles pour optimiser les performances et gérer correctement les dépendances.

---

### ForeignKey et relationship <a id="foreignkey-et-relationship-"></a>

SQLAlchemy permet de définir des **relations entre tables** avec des clés étrangères et des objets relationnels (`relationship`) pour naviguer facilement entre elles.

```python
from sqlalchemy import ForeignKey
from sqlalchemy.orm import relationship

class Article(Base):
    __tablename__ = "articles"

    id = Column(Integer, primary_key=True)
    titre = Column(String(100), nullable=False)
    contenu = Column(String)
    utilisateur_id = Column(Integer, ForeignKey("utilisateurs.id"))

    # Relation avec Utilisateur
    utilisateur = relationship("Utilisateur", back_populates="articles")

class Utilisateur(Base):
    __tablename__ = "utilisateurs"

    id = Column(Integer, primary_key=True, autoincrement=True)
    nom = Column(String, nullable=False)
    age = Column(Integer)

    # Relation inverse avec Article
    articles = relationship("Article", back_populates="utilisateur")
```

**Paramètres et concepts :**
* `ForeignKey("table.colonne")` : définit la **clé étrangère** pour établir la relation.
* `relationship("ClasseCible", ...)` : crée une **relation ORM** entre les modèles.
* `back_populates` : permet de lier les deux côtés de la relation (navigation bidirectionnelle).
* `uselist` (bool, optionnel) : indique si la relation est **liste** (`True` pour 1:N) ou **objet unique** (`False` pour 1:1).

---

### Types de relations <a id="types-de-relations-"></a>

1. **One-to-Many (1:N)**
   Un utilisateur peut avoir plusieurs articles.

```python
# Accéder aux articles d'un utilisateur
user = session.query(Utilisateur).first()
for art in user.articles:
    print(art.titre)

# Accéder à l'utilisateur d'un article
article = session.query(Article).first()
print(article.utilisateur.nom)
```

2. **Many-to-One (N:1)**
   Chaque article appartient à **un seul utilisateur**.

```python
article = session.query(Article).first()
print(article.utilisateur.nom)
```

3. **One-to-One (1:1)**
   Une relation 1:1 peut être définie avec `uselist=False`.

```python
class Profil(Base):
    __tablename__ = "profils"
    id = Column(Integer, primary_key=True)
    utilisateur_id = Column(Integer, ForeignKey("utilisateurs.id"))
    utilisateur = relationship("Utilisateur", back_populates="profil", uselist=False)

Utilisateur.profil = relationship("Profil", back_populates="utilisateur", uselist=False)
```

4. **Many-to-Many (N:N)**
   Nécessite une table d’association (`association table`) pour gérer la relation.

```python
from sqlalchemy import Table

association = Table(
    'utilisateur_groupe',
    Base.metadata,
    Column('utilisateur_id', ForeignKey('utilisateurs.id'), primary_key=True),
    Column('groupe_id', ForeignKey('groupes.id'), primary_key=True)
)

class Groupes(Base):
    __tablename__ = "groupes"
    id = Column(Integer, primary_key=True)
    nom = Column(String, nullable=False)
    membres = relationship("Utilisateur", secondary=association, back_populates="groupes")

Utilisateur.groupes = relationship("Groupes", secondary=association, back_populates="membres")
```

**Notes :**
* `relationship` simplifie la navigation dans les données liées.
* `secondary` est utilisé pour les relations N:N.
* `back_populates` ou `backref` permet de créer la relation inverse automatiquement.
* Les relations permettent d’éviter des jointures SQL manuelles dans la plupart des cas, en utilisant directement des objets Python.

---
---
## Requêtes avancées et jointures <a id="requêtes-avancées-et-jointures-"></a>

### Filtrage avec `filter()` et `filter_by()` <a id="filtrage-avec-filter-et-filter_by-"></a>

Permet de **sélectionner des lignes selon des conditions**.

```python
# filter_by : simple égalité sur les colonnes
utilisateur = session.query(Utilisateur).filter_by(nom="Alice").first()

# filter : conditions plus complexes
adultes = session.query(Utilisateur).filter(Utilisateur.age >= 18).all()
```

**Paramètres :**
* `filter_by(colonne=valeur)` : filtre simple basé sur des égalités.
* `filter(condition)` : filtre plus flexible avec opérateurs (`>=`, `<`, `!=`, `in_()`, `like()`).
* **Retour :** objet `Query` permettant `first()`, `all()`, `count()`.

---

### Tri avec `order_by()` <a id="tri-avec-order_by-"></a>

Permet de **trier les résultats**.

```python
# Tri croissant par nom
utilisateurs = session.query(Utilisateur).order_by(Utilisateur.nom).all()

# Tri décroissant par âge
utilisateurs = session.query(Utilisateur).order_by(Utilisateur.age.desc()).all()
```

**Paramètres :**

* `order_by(colonne)` : colonne(s) pour trier.
* `asc()` ou `desc()` : direction du tri.
* **Retour :** liste d’objets triés selon les colonnes spécifiées.

---

### Jointures avec `join()` <a id="jointures-avec-join-"></a>

Permet de **combiner plusieurs tables**.

```python
# Récupérer tous les articles avec le nom de l'utilisateur
articles = session.query(Article, Utilisateur).join(Utilisateur).all()

for art, user in articles:
    print(f"{art.titre} écrit par {user.nom}")
```

**Paramètres :**
* `join(Classe)` : table à joindre.
* `onclause` (optionnel) : condition de jointure explicite.
* `isouter=True` : pour une **left outer join**.

**Retour :** objet `Query` avec colonnes/tables jointes.

---

### Jointures externes (`outerjoin`) <a id="jointures-externes-outerjoin-"></a>

Permet de **conserver les lignes même si la relation est absente**.

```python
# Tous les utilisateurs, même s'ils n'ont pas d'articles
utilisateurs = session.query(Utilisateur, Article).outerjoin(Article).all()

for user, art in utilisateurs:
    print(f"{user.nom} - Article : {art.titre if art else 'Aucun'}")
```

**Paramètres :**
* `outerjoin(Classe, onclause=None)` : jointure externe.
* `isouter=True` peut aussi être utilisé avec `join()`.

**Retour :** objet `Query` contenant tous les objets, même sans correspondance.

---

### Groupements et agrégations <a id="groupements-et-agrégations-"></a>

Permet de **regrouper des résultats et calculer des statistiques**.

```python
from sqlalchemy import func

# Nombre d'articles par utilisateur
resultats = session.query(Utilisateur.nom, func.count(Article.id))\
    .join(Article)\
    .group_by(Utilisateur.nom)\
    .all()

for nom, nb in resultats:
    print(f"{nom} a écrit {nb} article(s)")
```

**Paramètres :**
* `group_by(colonne)` : colonne(s) pour regrouper les résultats.
* `func` : fonctions d’agrégation SQL (`count`, `sum`, `avg`, `max`, `min`).

**Retour :** liste de tuples `(valeur_groupée, agrégation)`.

---

### Filtres avancés et combinés <a id="filtres-avancés-et-combinés-"></a>

Utilisation des **opérateurs logiques** pour combiner plusieurs conditions.

```python
from sqlalchemy import and_, or_

# Utilisateurs adultes ou nom Alice
utilisateurs = session.query(Utilisateur)\
    .filter(or_(Utilisateur.age >= 18, Utilisateur.nom == "Alice"))\
    .all()

# Utilisateurs adultes ET nom commençant par "B"
utilisateurs = session.query(Utilisateur)\
    .filter(and_(Utilisateur.age >= 18, Utilisateur.nom.like("B%")))\
    .all()
```

**Paramètres :**
* `and_()` : toutes les conditions doivent être vraies.
* `or_()` : au moins une condition vraie.
* `like()` : filtrage sur motif (ex : `"B%"` = commence par B).
* `in_()` : correspondance dans une liste de valeurs.

**Retour :** liste d’objets correspondant aux conditions.

---



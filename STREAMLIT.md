# Notebook for Streamlit
# Table of Contents
- [Notebook for Streamlit](#notebook-for-streamlit)
- [Table of Contents](#table-of-contents)
  - [Introduction / Description ](#introduction--description-)
    - [Présentation de Streamlit ](#présentation-de-streamlit-)
      - [Objectif ](#objectif-)
      - [Fonctionnalités principales ](#fonctionnalités-principales-)
  - [Installation / Import ](#installation--import-)
    - [Installation de Streamlit ](#installation-de-streamlit-)
    - [Installation des dépendances du projet ](#installation-des-dépendances-du-projet-)
    - [Importer Streamlit ](#importer-streamlit-)
  - [Fonctions d'écriture ](#fonctions-décriture-)
    - [`st.title()` ](#sttitle-)
    - [`st.header()` ](#stheader-)
    - [`st.subheader()` ](#stsubheader-)
    - [`st.write()` ](#stwrite-)
    - [`st.dataframe()` ](#stdataframe-)
    - [`st.table()` ](#sttable-)
    - [`st.markdown()` ](#stmarkdown-)
    - [`st.code()` ](#stcode-)
    - [`st.caption()` ](#stcaption-)
    - [`st.html()`  *(Streamlit ≥ 1.30)*](#sthtml--streamlit--130)
  - [Fonctions de widget de texte ](#fonctions-de-widget-de-texte-)
    - [`st.text_input()` ](#sttext_input-)
    - [`st.number_input()` ](#stnumber_input-)
    - [`st.password_input()` ](#stpassword_input-)
    - [`st.date_input()` ](#stdate_input-)
    - [`st.time_input()` ](#sttime_input-)
  - [Fonctions de widget de selection ](#fonctions-de-widget-de-selection-)
    - [`st.selectbox()` ](#stselectbox-)
    - [`st.multiselect()` ](#stmultiselect-)
    - [`st.radio()` ](#stradio-)
    - [`st.checkbox()` ](#stcheckbox-)
    - [`st.toggle()`  *(Streamlit ≥ 1.22)*](#sttoggle--streamlit--122)
    - [`st.segmented_control()`  *(Streamlit ≥ 1.30)*](#stsegmented_control--streamlit--130)
  - [Fonctions de widget de curseurs ](#fonctions-de-widget-de-curseurs-)
    - [`st.slider()` ](#stslider-)
    - [`st.slider()` — Sélection d’un intervalle ](#stslider--sélection-dun-intervalle-)
    - [`st.select_slider()` ](#stselect_slider-)
  - [Fonctions de widget de boutton](#fonctions-de-widget-de-boutton)
    - [`st.button()` ](#stbutton-)
    - [`st.form_submit_button()` ](#stform_submit_button-)
    - [`st.download_button()` ](#stdownload_button-)
  - [Fonctions de widget de fichier](#fonctions-de-widget-de-fichier)
    - [`st.file_uploader()` ](#stfile_uploader-)
    - [`st.camera_input()` ](#stcamera_input-)
    - [`st.data_editor()` ](#stdata_editor-)
  - [Fonctions de widget de conteneur ](#fonctions-de-widget-de-conteneur-)
    - [`st.form()` ](#stform-)
    - [`st.expander()` ](#stexpander-)
    - [`st.tabs()` ](#sttabs-)
    - [`st.columns()` ](#stcolumns-)
    - [`st.container()` ](#stcontainer-)
    - [`st.sidebar()` ](#stsidebar-)
    - [`st.popover()` ](#stpopover-)
    - [`st.empty()` ](#stempty-)
  - [Fonction de média ](#fonction-de-média-)
    - [`st.image()` ](#stimage-)
    - [`st.audio()` ](#staudio-)
    - [`st.video()` ](#stvideo-)
  - [Fonction d'affichage](#fonction-daffichage)
    - [`st.map()` ](#stmap-)
    - [`st.pyplot()` ](#stpyplot-)
    - [`st.pydeck_chart()` ](#stpydeck_chart-)
    - [`st.graphviz_chart()` ](#stgraphviz_chart-)
    - [`st.json()` ](#stjson-)
    - [`st.bar_chart()` ](#stbar_chart-)
    - [`st.line_chart()` ](#stline_chart-)
    - [`st.area_chart()` ](#starea_chart-)
    - [`st.altair_chart()` ](#staltair_chart-)
    - [`st.plotly_chart()` ](#stplotly_chart-)
    - [`st.bokeh_chart()` ](#stbokeh_chart-)
  - [Fonction de Message d'alerte ](#fonction-de-message-dalerte-)
    - [`st.success()` ](#stsuccess-)
    - [`st.error()` ](#sterror-)
    - [`st.warning()` ](#stwarning-)
    - [`st.info()` ](#stinfo-)
    - [`st.exception()` ](#stexception-)
    - [`st.toast()`  (Streamlit \>= 1.25)](#sttoast--streamlit--125)


## Introduction / Description <a class="anchor" id="introduction--description-"></a>

### Présentation de Streamlit <a id="présentation-de-streamlit-"></a>

Streamlit est une librairie Python open-source qui permet de créer très facilement des **applications web interactives** pour la data science et le machine learning, directement à partir de scripts Python.

#### Objectif <a id="objectif-"></a>

Streamlit simplifie la création d'interfaces utilisateur pour :

- Tester des fonctions Python de manière interactive
- Visualiser des données en temps réel
- Partager des prototypes ou dashboards rapidement, sans connaissances en développement web

#### Fonctionnalités principales <a id="fonctionnalités-principales-"></a>

- Widgets interactifs : `st.button()`, `st.slider()`, `st.text_input()`, `st.selectbox()`, etc.
- Affichage de données et de graphiques : `st.write()`, `st.dataframe()`, `st.pyplot()`, `st.plotly_chart()`
- Layout automatique et responsive
- Support des bibliothèques de visualisation tierces : Matplotlib, Plotly, Altair, Seaborn
- Possibilité de créer des apps multi-pages pour organiser des projets plus complexes

## Installation / Import <a id="installation--import-"></a>

### Installation de Streamlit <a id="installation-de-streamlit-"></a>

Installez Streamlit avec pip :

```bash
pip install streamlit
``` 
Si vous utilisez un environnement virtuel, assurez-vous qu’il est activé avant l’installation.

Pour vérifier que l’installation a réussi, vous pouvez lancer l’application de démonstration intégrée :

```bash  
streamlit hello
``` 
Cette commande ouvre une app interactive avec plusieurs exemples pour tester Streamlit.

### Installation des dépendances du projet <a id="installation-des-dépendances-du-projet-"></a> 
Si votre projet utilise d’autres bibliothèques (ex : pandas, matplotlib, plotly), créez un fichier requirements.txt et installez-les toutes en une seule commande :

```bash  
pip install -r requirements.txt
``` 
### Importer Streamlit <a id="importer-streamlit-"></a> 
Dans votre notebook Python, importez Streamlit pour commencer à créer l’interface :

```python 
import streamlit as st
```

---
---
## Fonctions d'écriture <a id="fonctions-décriture-"></a>

Streamlit fournit de nombreuses fonctions pour créer rapidement une interface interactive. Voici quelques fonctions de base avec un exemple et la description de leurs paramètres.

---

### `st.title()` <a id="sttitle-"></a>

Crée un titre principal pour votre application.

```python
st.title("Bienvenue dans mon app Streamlit")
```

**Paramètres :**

* `body` (str) : le texte du titre.
* Affiche le texte en grande taille, comme un `<h1>` en HTML.

---

### `st.header()` <a id="stheader-"></a>

Crée un en-tête secondaire (comme un `<h2>` en HTML).

```python
st.header("Section Analyse des données")
```

**Paramètres :**
* `body` (str) : texte de l’en-tête.
* Sert à structurer votre application en sections.

**Retour** : aucun

---

### `st.subheader()` <a id="stsubheader-"></a>

Crée un sous-en-tête (similaire à `<h3>`).

```python
st.subheader("Visualisation graphique")
```

**Paramètres :**
* `body` (str) : texte du sous-en-tête.
* Utilisé pour sous-diviser les sections de votre app.

**Retour** : aucun

---

### `st.write()` <a id="stwrite-"></a>

Affiche du texte, des nombres, des objets Python, des dataframes, ou des graphiques. Fonction très flexible pour afficher à peu près n’importe quel type d’objet.

```python
st.write("Voici un dataframe :", df)
```

**Paramètres :**
* `*args` : un ou plusieurs objets Python : Peut être : str, int, float, bool, list, dict, pandas DataFrame, matplotlib figure, plotly figure…
* `unsafe_allow_html` (bool, optionnel) : si True, permet d’interpréter le HTML dans le texte.

**Retour** : aucun

---

### `st.dataframe()` <a id="stdataframe-"></a>

Affiche un tableau interactif (DataFrame pandas ou autre).

```python
import pandas as pd

df = pd.DataFrame({
    "Nom": ["Alice", "Bob"],
    "Âge": [25, 30]
})

st.dataframe(df)
```

**Paramètres :**
* `data` un DataFrame, numpy array, ou tableau.
* `width` (int, optionnel) : largeur du tableau en pixels.
* `height` (int, optionnel) : hauteur du tableau en pixels.
* `use_container_width ` (bool, optionnel) : si True, le tableau s’adapte automatiquement à la largeur du conteneur.
* Affiche un tableau interactif avec tri et scroll.

**Retour** : aucun

---

### `st.table()` <a id="st-table"></a>

Affiche un **tableau statique** à partir d’un DataFrame ou d’un tableau Python. Contrairement à `st.dataframe()`, **il n’est pas interactif** : pas de tri, pas de scroll ni de redimensionnement.

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    "Nom": ["Alice", "Bob", "Charlie"],
    "Âge": [25, 30, 35],
    "Ville": ["Paris", "Lyon", "Marseille"]
})

st.table(df)
```

**Paramètres :**

* `data` (DataFrame, list, tuple ou numpy array) : tableau à afficher.
* `width` (int, optionnel) : largeur du tableau en pixels (option non documentée, peut varier selon la version).
* `height` (int, optionnel) : hauteur du tableau en pixels (option non documentée, généralement ignorée).
* `use_container_width` (bool, optionnel) : non applicable à `st.table()`, uniquement pour `st.dataframe()`.

**Retour** : aucun (affiche simplement le tableau statique dans l’application).

**Notes :**

* Idéal pour afficher des **résultats simples** ou des tableaux avec peu de lignes.
* Pour un tableau interactif avec tri et scroll, utilisez `st.dataframe()`.


---

### `st.markdown()` <a id="stmarkdown-"></a>

Affiche du texte **Markdown** directement dans l’application Streamlit, avec possibilité d’inclure du **HTML simple** si autorisé.

```python
st.markdown("# Titre principal\nVoici du **texte formaté** en Markdown.")
```

**Paramètres :**
* `body` (str) : contenu Markdown à afficher.
  Peut inclure titres, listes, tableaux, liens, code, etc.
* `unsafe_allow_html` (bool, optionnel) :
  autorise le HTML brut (`<p>`, `<div>`, couleurs inline…).
  *Défaut : False*
  ⚠️ JavaScript et CSS complexes restent bloqués pour des raisons de sécurité.
* `help` (str, optionnel) : texte d’aide affiché au survol.
* `key` (str, optionnel) : identifiant unique pour le widget.

**Retour** : aucun (le Markdown est simplement affiché).

---

### `st.code()` <a id="stcode-"></a>

Affiche un bloc de code avec coloration syntaxique.

```python
code = """
def hello():
    print("Hello Streamlit")
"""
st.code(code, language="python")
```

**Paramètres :**
* `body` (str) : code à afficher dans le bloc.
* `language` (str, optionnel) : langage pour la coloration syntaxique
  (ex : `"python"`, `"css"`, `"json"`, `"sql"`).
* `line_numbers` (bool, optionnel) : affiche les numéros de lignes si `True`.
  *Défaut : False*
* `help` (str, optionnel) : texte d’aide au survol.
* `key` (str, optionnel) : identifiant unique.

**Retour** : aucun (affiche un bloc de code formaté).

---

### `st.caption()` <a id="stcaption-"></a>

Affiche une courte légende ou indication sous forme de texte discret (style “caption”).

```python
st.caption("Données mises à jour quotidiennement.")
```

**Paramètres :**
* `body` (str) : texte court à afficher en style “caption”.
* `help` (str, optionnel) : texte d’aide au survol.
* `key` (str, optionnel) : identifiant unique.

**Retour** : aucun.

---

### `st.html()` <a id="sthtml--streamlit--130"></a> *(Streamlit ≥ 1.30)*

Affiche directement du contenu **HTML**, avec support complet du rendering (mais sans JavaScript).

```python
import streamlit as st

st.html("""
<div style="padding:10px; background:#eef;">
    <h3 style="color:#3366cc;">Titre en HTML</h3>
    <p>Contenu affiché avec <b>HTML natif</b>.</p>
</div>
""")
```

**Paramètres :**
* `html` (str) : contenu HTML brut à afficher.
* `height` (int, optionnel) : hauteur de la zone d’affichage en pixels.
  *Défaut : auto*
* `scrolling` (bool, optionnel) : si `True`, active le scroll si le contenu dépasse.
  *Défaut : False*
* `help` (str, optionnel) : texte d’aide au survol.
* `key` (str, optionnel) : identifiant unique.

**Retour** : aucun.

**Notes importantes :**

* **JavaScript n’est pas autorisé** (sécurité).
* Le CSS inline fonctionne (`style=""`).
* Support parfait pour intégrer des layouts, div, tables, HTML décoratif.

---
---

## Fonctions de widget de texte <a id="#fonctions-de-widget-de-texte-"></a>

### `st.text_input()` <a id="sttext_input-"></a>

Permet à l’utilisateur de saisir du texte.

```python
nom = st.text_input("Entrez votre nom :")
st.write("Bonjour", nom)
```

**Paramètres :**
* `label` (str) : le texte affiché devant le champ.
* `value` (str, optionnel) : valeur par défaut.
* `max_chars` (int, optionnel) : limite de caractères.
* `key` (str, optionnel) : identifiant unique pour différencier plusieurs widgets.
* `placeholder ` (str, optionnel) : texte affiché quand le champ est vide.

**Retour** : le texte saisi par l’utilisateur

---

### `st.number_input()` <a id="stnumber_input-"></a>

Permet à l’utilisateur de saisir une valeur numérique (int ou float) avec ou sans limites, et de manière interactive.

```python
import streamlit as st

valeur = st.number_input("Entrez un nombre", min_value=0, max_value=100, value=10, step=1)
st.write("Vous avez saisi :", valeur)
```

**Paramètres :**
* `label` (str) : texte affiché devant le champ.
* `min_value` (int ou float, optionnel) : valeur minimale autorisée.
* `max_value` (int ou float, optionnel) : valeur maximale autorisée.
* `value` (int ou float, optionnel) : valeur par défaut affichée.
* `step` (int ou float, optionnel) : incrément utilisé lors de l’augmentation/diminution.
* `format` (str, optionnel) : format d’affichage (ex : `"%.2f"` pour 2 décimales).
* `key` (str, optionnel) : identifiant unique pour le widget.
* `help` (str, optionnel) : texte d’aide affiché au survol.
* `on_change` (callable, optionnel) : fonction à exécuter quand la valeur change.
* `args` / `kwargs` (optionnel) : arguments passés à `on_change`.

**Retour** : la valeur numérique saisie par l’utilisateur (int ou float selon le type du `value`).

---

### `st.password_input()` <a id="stpassword_input-"></a>

Champ de saisie destiné aux mots de passe : le texte entré est masqué à l’écran.

```python
mdp = st.password_input(
    "Entrez votre mot de passe",
    placeholder="Votre mot de passe...",
    max_chars=20
)
```

 **Paramètres :**
* `label` (str) : Texte affiché au-dessus du champ.
* `value` (str, optionnel) : Valeur pré-remplie dans le champ.
  *Défaut : ""*
* `max_chars` (int, optionnel) : Nombre maximum de caractères autorisés.
* `type` (str, optionnel) : Toujours `"password"` pour cette fonction (caractères masqués).
* `placeholder` (str, optionnel) : Texte grisé affiché avant la saisie.
* `help` (str, optionnel) : Texte d’aide affiché au survol.
* `autocomplete` (str, optionnel) : Permet de contrôler l’auto-complétion du navigateur :
  exemples : `"current-password"` / `"new-password"` / `"off"`
* `key` (str, optionnel) : Identifiant unique si plusieurs widgets similaires.
* `on_change` (callable, optionnel) : Fonction appelée automatiquement lorsque la valeur change.
* `args` (tuple, optionnel) : Arguments passés à `on_change`.
* `kwargs` (dict, optionnel) : Arguments nommés passés à `on_change`.

**Retour :** La chaîne de caractères saisie (non masquée dans Python).

---

### `st.date_input()` <a id="stdate_input-"></a>

Permet à l’utilisateur de sélectionner **une date** ou **une plage de dates** via un calendrier interactif.

```python
import streamlit as st
from datetime import date

date_selection = st.date_input(
    "Sélectionnez une date",
    value=date.today()
)

st.write("Date choisie :", date_selection)
```

**Paramètres :**
* `label` (str)
  Texte affiché au-dessus du calendrier.
* `value` (date, tuple de dates, liste de dates, optionnel)
  Valeur par défaut :
  * une date unique → sélection simple
  * un tuple `(date_debut, date_fin)` → sélection d’un intervalle
  * une liste de dates → sélection multiple
    Par défaut : `date.today()`.
* `min_value` (date, optionnel)
  Date minimale sélectionnable.
* `max_value` (date, optionnel)
  Date maximale sélectionnable.
* `key` (str, optionnel)
  Identifiant unique du widget.
* `help` (str, optionnel)
  Texte affiché au survol.
* `on_change` (callable, optionnel)
  Fonction déclenchée lorsque la date change.
* `args` / `kwargs`
  Arguments passés à la fonction `on_change`.
* `disabled` (bool, optionnel)
  Désactive la sélection si `True`.

**Retour :** *Une date unique* ou *une liste de dates / un tuple*, selon la sélection.

**Notes :**
* Très utile pour les filtres temporels, bookings, reporting, dashboards.
* Lorsque `value` est un tuple → mode plage de dates automatiquement activé.

---

### `st.time_input()` <a id="sttime_input-"></a>

Permet à l’utilisateur de sélectionner **une heure** via un widget interactif (HH:MM ou HH:MM:SS).

```python
import streamlit as st
from datetime import time

heure = st.time_input(
    "Sélectionnez une heure",
    value=time(12, 0)
)

st.write("Heure choisie :", heure)
```

**Paramètres :**
* `label` (str)
  Texte affiché au-dessus du widget.
* `value` (time, optionnel)
  Heure par défaut.
  Par exemple `time(14, 30)`.
* `step` (int, timedelta ou None, optionnel)
  Intervalle entre valeurs sélectionnables :
  * en **secondes** (ex : 60 = increments de 1 min)
  * en `timedelta`
  * `None` → réglage libre
    Par défaut : `60` (1 minute).
* `key` (str, optionnel)
  Identifiant unique.
* `help` (str, optionnel)
  Texte au survol.
* `on_change` (callable, optionnel)
  Fonction appelée quand l’heure change.
* `args` / `kwargs`
  Arguments transmis à `on_change`.
* `disabled` (bool, optionnel)
  Désactive le widget si `True`.

**Retour :** Une valeur `datetime.time`.

**Notes :**
* Ne supporte **pas les intervalles d’heures** (uniquement sélection simple).
* Combine très bien avec `st.date_input()` pour créer un datetime complet.

---
---

## Fonctions de widget de selection <a id="fonctions-de-widget-de-selection-"></a>

### `st.selectbox()` <a id="stselectbox-"></a>

Permet à l’utilisateur de sélectionner **une seule valeur** dans une liste déroulante.

```python
genre = st.selectbox(
    "Choisissez un genre",
    ["Homme", "Femme", "Autre"],
    index=0
)
```

**Paramètres :**
* `label` (str) : Texte affiché.
* `options` (list, tuple, np.array, pd.Series) : Liste des choix.
* `index` (int, optionnel) : Index du choix sélectionné par défaut.
* `format_func` (callable, optionnel) : Fonction appliquée aux éléments pour changer leur affichage sans modifier la valeur réelle.
* `placeholder` (str, optionnel, Streamlit ≥ 1.24) : Texte affiché avant la sélection.
* `help` (str, optionnel) : Aide affichée au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction déclenchée si changement.
* `args`, `kwargs` : Arguments pour `on_change`.

**Retour :** La valeur choisie.

---

### `st.multiselect()` <a id="stmultiselect-"></a>

Permet de sélectionner **plusieurs valeurs** dans une liste.

```python
options = st.multiselect(
    "Choisissez des éléments",
    ["Python", "Java", "C++", "Go"],
    default=["Python"]
)
```

**Paramètres :**
* `label` (str) : Texte affiché.
* `options` (list, tuple, np.array, pd.Series) : Choix disponibles.
* `default` (list, optionnel) : Valeurs sélectionnées par défaut.
* `max_selections` (int ou None, optionnel) : Limite max de sélections.
* `format_func` (callable, optionnel) : Format visuel des options.
* `placeholder` (str, optionnel) : Texte affiché avant toute sélection.
* `help` (str, optionnel) : Aide affichée au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction déclenchée si changement.
* `args`, `kwargs` : Arguments pour `on_change`.

**Retour :** Une **liste** des valeurs choisies.

---

### `st.radio()` <a id="stradio-"></a>

Permet la sélection **d’une option unique** via des boutons radio.

```python
choix = st.radio(
    "Choisissez une option :",
    ["Oui", "Non", "Peut-être"],
    index=1
)
```

**Paramètres :**

* `label` (str) : Titre du widget.
* `options` (list, tuple, np.array, pd.Series) : Options disponibles.
* `index` (int, optionnel) : Option sélectionnée par défaut.
* `format_func` (callable, optionnel) : Affichage modifié des options.
* `horizontal` (bool, optionnel) : Affiche les options sur une ligne.
* `help` (str, optionnel) : Aide affichée au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction déclenchée si changement.
* `args`, `kwargs` : Arguments pour `on_change`.

**Retour :** La valeur sélectionnée.

---

### `st.checkbox()` <a id="stcheckbox-"></a>

Affiche une **case à cocher**.

```python
agree = st.checkbox("J'accepte les conditions")
```

**Paramètres :**

* `label` (str) — Texte affiché.
* `value` (bool, optionnel) — Valeur par défaut.
* `help` (str, optionnel) : Aide affichée au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction déclenchée si changement.
* `args`, `kwargs` : Arguments pour `on_change`.

**Retour :**  `True` si coché, `False` sinon.

---

### `st.toggle()` <a id="sttoggle--streamlit--122"></a> *(Streamlit ≥ 1.22)*

Un **interrupteur moderne** ON/OFF, alternative à `checkbox`.

```python
mode = st.toggle("Activer le mode avancé")
```

**Paramètres :**

* `label` (str) : Texte affiché.
* `value` (bool, optionnel) : Valeur initiale.
* `help` (str, optionnel) : Aide affichée au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction déclenchée si changement.
* `args`, `kwargs` : Arguments pour `on_change`.

**Retour** : `True` si activé, `False` sinon.

---

### `st.segmented_control()` <a id="stsegmented_control--streamlit--130"></a> *(Streamlit ≥ 1.30)*

Permet de choisir **une seule option** sous forme de boutons segmentés (style iOS / macOS).

```python
option = st.segmented_control(
    "Mode d'affichage",
    ["Liste", "Grille", "Tableau"],
    index=0
)
```

**Paramètres :**
* `label` (str ou None) : Optionnel : description au-dessus du widget.
* `options` (list-like) : Choix affichés sur les segments.
* `index` (int, optionnel) : Position sélectionnée par défaut.
* `format_func` (callable, optionnel) : Formatage des options.
* `disabled` (bool, optionnel) : Désactive le widget.
* `help` (str, optionnel) : Aide au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction déclenchée si changement.
* `args`, `kwargs` : Arguments pour `on_change`.

**Retour** : La valeur sélectionnée.

---
---

## Fonctions de widget de curseurs <a id="fonctions-de-widget-de-curseurs"></a>

### `st.slider()` <a id="stslider-"></a>

Permet à l’utilisateur de sélectionner une valeur numérique sur une plage.

```python
age = st.slider("Quel est votre âge ?", 0, 100, 25)
```

**Paramètres :**
* `label` (str) : texte affiché.
* `min_value` (int ou float) : valeur minimale.
* `max_value` (int ou float) : valeur maximale.
* `value` (int ou float, optionnel) : valeur par défaut.
* `step` (int ou float, optionnel) : incrément du slider.
* `format` (str, optionnel) : format d’affichage de la valeur (ex : "%.2f").
* `key` (str, optionnel) : identifiant unique
* `help` (str, optionnel) : texte affiché au survol

**Retour** la valeur choisie par l’utilisateur.

---

### `st.slider()` — Sélection d’un intervalle <a id="stslider--sélection-dun-intervalle-"></a>

Le slider peut aussi permettre la sélection **d’une plage de valeurs** en utilisant **un tuple** comme valeur par défaut.

```python
valeurs = st.slider(
    "Sélectionnez une plage de valeurs",
    min_value=0,
    max_value=100,
    value=(20, 80),
    step=5
)
```

**Paramètres :**
* `label` (str) : Texte affiché au-dessus du slider.
* `min_value` (int, float, date, time ou datetime) : Valeur minimale possible.
* `max_value` (int, float, date, time ou datetime) : Valeur maximale possible.
* `value` (tuple, obligatoire pour un range) : Format : `(valeur_min, valeur_max)`
  *Défaut : (min_value, max_value)* Cela force Streamlit à afficher un slider **à deux poignées**.
* `step` (int, float, timedelta, optionnel) : Incrément entre chaque position.
* `format` (str, optionnel) : Format d’affichage, par exemple `"%.2f"`.
* `help` (str, optionnel) : Texte affiché au survol.
* `key` (str, optionnel) : Identifiant unique.
* `on_change` (callable, optionnel) : Fonction exécutée à chaque changement de valeur.
* `args` (tuple, optionnel) : Paramètres à passer à `on_change`.
* `kwargs` (dict, optionnel) : Paramètres nommés à passer à `on_change`.

**Retour :** Un **tuple (min_selection, max_selection)** correspondant à la plage choisie.

---

Voici la documentation complète de **`st.select_slider()`**, avec l’exemple **simple** et **range (double sélection)**, et tous les paramètres détaillés, dans le même format que tes autres widgets.

---

### `st.select_slider()` <a id="stselect_slider-"></a>

Permet de créer un slider basé **sur une liste d’options non numériques** (texte, labels, catégories, dates, niveaux, etc.).
Il peut fonctionner en **sélection simple** ou en **sélection d’intervalle** (range).

```python
niveau = st.select_slider(
    "Choisissez un niveau",
    options=["Débutant", "Intermédiaire", "Avancé", "Expert"],
    value="Intermédiaire"
)

st.write("Niveau sélectionné :", niveau)
```

**Paramètres :**
* `label` (str) : Titre du widget.
* `options` (list, tuple, np.array, pd.Series) : Liste ordonnée des valeurs possibles.
* `value` (élément ou tuple, optionnel) : un élément de `options` ou un tuple `(début, fin)`
    *Défaut : premier élément de `options`*
* `format_func` (callable, optionnel) : Fonction pour modifier l’affichage sans changer la valeur.
* `help` (str, optionnel) : Texte d’aide au survol.
* `key` (str, optionnel): Identifiant unique du widget.
* `on_change` (callable, optionnel) : Fonction exécutée à chaque changement de valeur.
* `args` (tuple, optionnel) : Paramètres à passer à `on_change`.
* `kwargs` (dict, optionnel) : Paramètres nommés à passer à `on_change`.

**Retour :** : une valeur (parmi `options`) ou un tuple `(valeur_debut, valeur_fin)`

---
---
## Fonctions de widget de boutton<a id="fonctions-de-widget-de-boutton"></a>

### `st.button()` <a id="stbutton-"></a>

Crée un bouton cliquable.

```python
if st.button("Cliquez ici"):
    st.write("Bouton cliqué !")
```

**Paramètres :**
* `label` (str) : texte affiché sur le bouton.
* `key` (str, optionnel) : identifiant unique si plusieurs boutons sont utilisés.
* `help` (str, optionnel) : texte affiché au survol pour expliquer le bouton.
* `on_click ` (callable, optionnel) : fonction à exécuter quand le bouton est cliqué.
* `args` / `kwargs` (optionnel) : arguments passés à on_click.

**Retour :** `True` uniquement lors du clic.

---
### `st.form_submit_button()` <a id="st-form-submit-button"></a>

Crée un bouton **de soumission** dans un formulaire (`st.form`) et déclenche l’action uniquement lorsque l’utilisateur clique dessus.

```python
import streamlit as st

with st.form("mon_formulaire"):
    nom = st.text_input("Entrez votre nom")
    age = st.number_input("Entrez votre âge", min_value=0, max_value=120, value=25)
    
    # Bouton de soumission
    submitted = st.form_submit_button("Soumettre")
    
    if submitted:
        st.success(f"Bonjour {nom}, vous avez {age} ans !")
```

**Paramètres :**
* `label` (str, optionnel) : texte affiché sur le bouton.
* `key` (str, optionnel) : identifiant unique du bouton, utile si plusieurs boutons dans le même formulaire.
* `help` (str, optionnel) : texte d’aide affiché au survol du bouton.
* `on_click` (callable, optionnel) : fonction à exécuter lorsque le bouton est cliqué.
* `args` / `kwargs` (optionnel) : arguments passés à `on_click`.

**Retour** : `True` si le bouton a été cliqué (donc si le formulaire a été soumis), sinon `False`.

**Notes importantes :**
* `st.form_submit_button()` **doit être utilisé à l’intérieur d’un `st.form()`**.
* Les valeurs des widgets dans le formulaire ne sont prises en compte que **lorsque ce bouton est cliqué**.
* Utile pour regrouper plusieurs widgets et éviter des mises à jour immédiates à chaque modification.

---

### `st.download_button()` <a id="st-download-button"></a>

Crée un **bouton permettant à l’utilisateur de télécharger des fichiers ou des données** depuis l’application Streamlit.

```python
import streamlit as st

# Exemple simple : téléchargement d'un texte
texte = "Ceci est un exemple de contenu à télécharger."
st.download_button(
    label="Télécharger le texte",
    data=texte,
    file_name="exemple.txt",
    mime="text/plain"
)
```

**Paramètres :**
* `label` (str) : texte affiché sur le bouton.
* `data` (str, bytes, bytearray, file-like ou pandas DataFrame) : contenu à télécharger.
* `file_name` (str, optionnel) : nom du fichier téléchargé.
* `mime` (str, optionnel) : type MIME du fichier (ex : `"text/plain"`, `"application/json"`, `"application/pdf"`).
* `key` (str, optionnel) : identifiant unique pour différencier plusieurs boutons.
* `help` (str, optionnel) : texte d’aide affiché au survol.
* `on_click` (callable, optionnel) : fonction exécutée lorsque l’utilisateur clique sur le bouton.
* `args` / `kwargs` (optionnel) : arguments passés à `on_click`.
* `disabled` (bool, optionnel) : si True, le bouton est désactivé.
* `use_container_width` (bool, optionnel) : si True, le bouton prend toute la largeur du conteneur.

**Retour** : `True` si le bouton a été cliqué (l’utilisateur a lancé le téléchargement), sinon `False`.

**Notes :**
* Permet de générer des **téléchargements de fichiers texte, CSV, Excel, images, JSON, etc.**.
* Idéal pour partager des résultats ou des exports depuis l’application Streamlit.

---
---
## Fonctions de widget de fichier<a id="fonctions-de-widget-de-fichier"></a>

### `st.file_uploader()` <a id="stfile_uploader-"></a>

Permet à l’utilisateur **d’envoyer un ou plusieurs fichiers** via l’interface Streamlit.
Idéal pour importer des images, CSV, PDF, modèles, etc.

```python
import streamlit as st

fichier = st.file_uploader(
    label="Importer un fichier",
    type=["csv", "txt", "pdf"],
    accept_multiple_files=False
)

if fichier:
    st.write("Nom du fichier :", fichier.name)
```

**Paramètres :**
* `label` (str) : texte affiché au-dessus du bouton d’import.
* `type` (str ou liste de str, optionnel) : extensions autorisées (ex. `"csv"` ou `["png", "jpg"]`).
* `accept_multiple_files` (bool, optionnel) : permet d’uploader plusieurs fichiers.
* `key` (str, optionnel) : identifiant unique.
* `help` (str, optionnel) : info-bulle affichée au survol.
* `on_change` (callable, optionnel) : fonction exécutée lorsque l’utilisateur ajoute un fichier.
* `args` / `kwargs` : arguments pour `on_change`.
* `disabled` (bool, optionnel) : désactive le widget.

**Retour :** 
* un objet `UploadedFile`
* ou une **liste de `UploadedFile`** si `accept_multiple_files=True`.

**Notes :**
* `UploadedFile` comporte : `.name`, `.type`, `.size`, `.read()`.
* Parfait pour importer des CSV puis les charger dans pandas.

---

### `st.camera_input()` <a id="stcamera_input-"></a>

Permet de **prendre une photo directement depuis la caméra** (ordinateur, tablette, mobile).
Très utile pour des applications de computer vision ou d’identification.

```python
import streamlit as st

photo = st.camera_input("Prenez une photo")

if photo:
    st.image(photo)
```

**Paramètres :**
* `label` (str) : texte affiché au-dessus du cadre caméra.
* `key` (str, optionnel) : identifiant unique.
* `help` (str, optionnel) : info-bulle au survol.
* `on_change` (callable, optionnel) : fonction déclenchée après capture.
* `args` / `kwargs` : paramètres passés à `on_change`.
* `disabled` (bool, optionnel) : désactive la caméra.

**Retour** : un objet `UploadedFile` contenant la photo capturée (format PNG).

**Notes :**
* Ne fonctionne que dans un navigateur compatible (Chrome, Safari, Firefox).
* Parfait pour analyser des images via OpenCV, PIL ou modèles IA.
  
---

### `st.data_editor()` <a id="stdata_editor-"></a>

Affiche un **tableau éditable** dans l’interface Streamlit.
L’utilisateur peut modifier des cellules, ajouter ou supprimer des lignes (selon la configuration), et renvoyer le résultat sous forme de DataFrame mis à jour.

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    "Nom": ["Alice", "Bob", "Charlie"],
    "Âge": [25, 30, 35],
    "Actif": [True, False, True]
})

result = st.data_editor(
    df,
    num_rows="dynamic",
    use_container_width=True
)

st.write("Données modifiées :")
st.write(result)
```

**Paramètres :**
* `data` (DataFrame, liste de dicts, liste de listes, ndarray)
  Données à afficher et rendre éditables.

* `columns` (dict, optionnel)
  Permet de configurer chaque colonne individuellement.
  Exemple : type forcé, libellé, format, validation, widget interne (toggle, select…).

  ```python
  columns={
      "Âge": {"type": "number", "min": 0, "max": 120},
      "Actif": {"type": "checkbox"}
  }
  ```

* `num_rows` (str ou int, optionnel)
  Contrôle l’ajout ou suppression de lignes.
  * `"dynamic"` : l’utilisateur peut ajouter/supprimer des lignes
  * `"fixed"` : nombre de lignes fixe
  * `int` : impose un nombre exact de lignes

* `disabled` (bool ou list, optionnel)
  * `True` : tableau non éditable
  * liste : désactive l’édition de certaines colonnes
    Ex : `disabled=["Nom", "Âge"]`

* `hide_index` (bool, optionnel)
  Si `True`, masque la colonne d’index.

* `key` (str, optionnel)
  Identifie le widget de façon unique.

* `use_container_width` (bool, optionnel)
  Si `True`, le tableau s’adapte à la largeur du conteneur.

* `on_change` (callable, optionnel)
  Fonction appelée lors d’une modification du tableau.

* `args` / `kwargs`
  Paramètres transmis à la fonction `on_change`.

**Retour :**
*Retourne un DataFrame contenant les valeurs modifiées par l’utilisateur.*

**Notes :**
* Supporte les types automatiques : texte, nombre, checkbox, select, date…
* Peut remplacer `st.dataframe()` si l’utilisateur doit modifier les données.
* Idéal pour des outils de nettoyage de données, édition de paramètres, etc.

---
---

## Fonctions de widget de conteneur <a id="#fonctions-de-widget-de-conteneur-"></a>

### `st.form()` <a id="stform-"></a>

Permet de créer un **formulaire interactif** regroupant plusieurs widgets et de déclencher une action uniquement après soumission.

```python
import streamlit as st

# Création d'un formulaire avec un identifiant unique
with st.form("mon_formulaire"):
    nom = st.text_input("Entrez votre nom")
    age = st.number_input("Entrez votre âge", min_value=0, max_value=120, value=25)
    
    # Bouton de soumission du formulaire
    submitted = st.form_submit_button("Soumettre")
    
    if submitted:
        st.success(f"Bonjour {nom}, vous avez {age} ans !")
```

**Paramètres :**
* `key` (str, optionnel) : identifiant unique du formulaire si plusieurs formulaires sont présents dans la même app.
* `clear_on_submit` (bool, optionnel, par défaut `False`) : si `True`, les widgets du formulaire sont réinitialisés après la soumission.

**Retour** : la valeur de `st.form_submit_button()` renvoie `True` si le formulaire a été soumis.

**Notes importantes :**
* Tous les widgets placés à l’intérieur du `with st.form("key"):` ne seront pris en compte qu’après l’appui sur `st.form_submit_button()`.
* Utile pour **regrouper plusieurs entrées** et éviter que l’interface ne réagisse à chaque modification de widget individuelle.
* Peut contenir n’importe quel type de widget Streamlit (`st.text_input`, `st.number_input`, `st.selectbox`, etc.).

---

### `st.expander()` <a id="stexpander-"></a>

Crée une zone repliable / dépliable, idéale pour cacher des détails ou informations secondaires.

```python
import streamlit as st

with st.expander("Voir plus de détails"):
    st.write("Voici du contenu additionnel...")
```

**Paramètres :**
* `label` (str)
  Titre affiché sur l’expander.
* `expanded` (bool, optionnel)
  Si `True`, l’expander est ouvert par défaut.
* `icon` (str, optionnel, ≥ Streamlit 1.29)
  Icône personnalisée (emoji ou nom d’icône).
  Exemple : `"📦"` ou `"info"`
* `key` (str, optionnel)
  Identifiant unique.

**Retour :** Un *contexte* (`with`) dans lequel le contenu est encapsulé.

---

### `st.tabs()` <a id="sttabs-"></a>

Crée un ensemble d’onglets permettant d’organiser le contenu en sections distinctes.

```python
import streamlit as st

tab1, tab2, tab3 = st.tabs(["Accueil", "Données", "Paramètres"])

with tab1:
    st.write("Bienvenue !")

with tab2:
    st.write("Voici vos données.")

with tab3:
    st.write("Réglages avancés.")
```

**Paramètres :**
* `tabs` (liste de str)
  Liste des noms des onglets.

**Retour :** Une liste d’objets onglets (`tab1`, `tab2`, …), à utiliser via `with`.

**Notes :**
* Chaque onglet peut contenir n’importe quel widget Streamlit.
* Les noms peuvent inclure des emojis.

---

### `st.columns()` <a id="stcolumns-"></a>

Permet de diviser la page en **colonnes** pour créer des mises en page horizontales.

```python
import streamlit as st

col1, col2, col3 = st.columns([1, 2, 1])

with col1:
    st.write("Colonne 1")

with col2:
    st.write("Colonne 2 (plus large)")

with col3:
    st.write("Colonne 3")
```

**Paramètres :**
* `spec` (int, liste d’int, optionnel)
  * `int` → nombre de colonnes égales
    ex : `st.columns(3)`
  * liste d’int → largeur relative des colonnes
    ex : `[1, 3, 1]`
* `gap` ("small" ou "large", optionnel)
  définie l’espacement horizontal entre colonnes.
  Par défaut : `"small"`.

**Retour :** Une liste de conteneurs à utiliser avec `with`.

**Notes :**
* Les colonnes peuvent contenir n’importe quels widgets.
* Combine très bien avec `st.tabs()` et `st.expander()` pour organiser l’interface.

---

### `st.container()` <a id="stcontainer-"></a>

Crée un **conteneur flexible** pouvant regrouper plusieurs éléments Streamlit.
Il peut être rempli directement ou mis à jour dynamiquement.

```python
import streamlit as st

container = st.container()

with container:
    st.write("Contenu dans le conteneur")
    st.button("Bouton")
```

**Paramètres :**
* Aucun paramètre.

**Retour :** Un conteneur utilisable avec `with`.

**Notes :**
* Utile pour organiser une page ou créer des zones ajustables.
* Peut être stocké dans une variable afin d’être **mis à jour plus tard**.
* Fonctionne très bien pour afficher / remplacer des ensembles de widgets.

---

### `st.sidebar()` <a id="stsidebar-"></a>

Permet d’afficher du contenu dans la **barre latérale** de Streamlit (menu à gauche).

```python
import streamlit as st

with st.sidebar:
    st.header("Menu")
    option = st.selectbox("Choix :", ["Accueil", "Profil", "Paramètres"])
```

**Paramètres :**
* Aucun paramètre (s’utilise comme un conteneur).

**Retour :** Un conteneur représentant la sidebar.

**Notes :**
* Idéal pour créer des menus, réglages, filtres.
* Tous les widgets ajoutés dans ce contexte apparaissent automatiquement dans la barre latérale.
* Peut être combiné avec `st.tabs()` ou `st.form()` dans certaines mises en page.

---

### `st.popover()` <a id="st-popover"></a>

Crée un **popover** — un conteneur masqué sous forme de bouton qui, lorsqu’il est cliqué, affiche un contenu additionnel (widgets, texte, etc.).

```python
import streamlit as st

with st.popover("Ouvrir le popover"):
    st.write("Contenu du popover 👋")
    name = st.text_input("Votre nom")
    st.button("Valider")
```

**Paramètres :**
* `label` (str) : texte du bouton ouvrant le popover.
  * Peut contenir du Markdown (gras, italique, liens, code, images, emoji…). 
* `help` (str, optionnel) : info‑bulle affichée au survol du bouton. 
* `icon` (str, optionnel) : emoji ou icône (Material Symbols) affichée à côté du label. 
* `disabled` (bool, optionnel) : si `True`, le bouton est désactivé (inutile). Par défaut `False`. 
* `use_container_width` (bool, optionnel) : si `True`, le bouton s’étend sur toute la largeur du conteneur parent. Sinon, largeur automatique. 
* `width` (int, `"stretch"` ou `"content"`, optionnel) : définit la largeur du bouton.

  * `"content"` (par défaut) : largeur adaptée au contenu.
  * `"stretch"` : s’étend sur toute la largeur du conteneur parent.
  * Un entier fixe en pixels est aussi possible.
    Le popover qui s’ouvre aura au moins la largeur du bouton, mais peut être plus large pour contenir son contenu.

**Retour :** Le conteneur popover — utilisable avec `with`, ou via des appels directs sur l’objet retourné pour ajouter des widgets.

**Notes :**
* Ouvrir ou fermer le popover **ne relance pas** l’app. 
* Interagir avec des widgets à l’intérieur déclenche un rerun, tout en gardant le popover ouvert. 
* Ne pas imbriquer un popover dans un autre popover (nesting non supporté). 

---

### `st.empty()` <a id="stempty-"></a>

Crée un **espace réservé** (placeholder) pouvant être remplacé dynamiquement.

```python
import streamlit as st
import time

slot = st.empty()
slot.write("Texte initial...")

time.sleep(2)
slot.write("Texte mis à jour !")
```

**Paramètres :**
* Aucun paramètre.

**Retour :** Un placeholder pouvant être remplacé par n’importe quel widget Streamlit.

---
---
## Fonction de média <a id="fonction-de-média-"></a>

### `st.image()` <a id="stimage-"></a>

Affiche une ou plusieurs images dans l’application.

```python
from PIL import Image
import streamlit as st

img = Image.open("exemple.png")
st.image(img, caption="Image exemple", use_column_width=True)
```

**Paramètres :**
* `image` : image unique ou liste d’images (`PIL.Image.Image`, `np.array`, URL ou `BytesIO`).
* `caption` (str ou list de str, optionnel) : légende(s) sous l’image.
* `width` (int, optionnel) : largeur de l’image en pixels.
* `output_format` (str, optionnel) : format de rendu : `"auto"` (défaut), `"PNG"`, `"JPEG"`.
* `channels` (str, optionnel) : `"RGB"` (défaut) ou `"BGR"` si tableau NumPy.
* `clamp` (bool, optionnel) : si `True`, limite les valeurs numériques entre 0 et 255.
* `use_column_width` (bool, optionnel) : si `True`, adapte l’image à la largeur du conteneur.

**Retour :** aucun (affiche l’image).

---

### `st.audio()` <a id="staudio-"></a>

Intègre un **lecteur audio** dans l’application.

```python
import streamlit as st

with open("exemple.mp3", "rb") as f:
    st.audio(f.read(), format="audio/mp3", start_time=0)
```

**Paramètres :**
* `data` : bytes, fichier ouvert (`io.BytesIO`) ou URL.
* `format` (str, optionnel) : type MIME de l’audio. Exemples :

  * `"audio/mpeg"` ou `"audio/mp3"` pour MP3
  * `"audio/wav"` pour WAV
  * `"audio/ogg"` pour OGG
  * `"audio/x-flac"` pour FLAC
* `start_time` (float, optionnel) : seconde de départ pour la lecture.
* `help` (str, optionnel) : texte d’aide au survol.
* `key` (str, optionnel) : identifiant unique.

**Retour :** aucun (lecteur intégré).

---

### `st.video()` <a id="stvideo-"></a>

Affiche un **lecteur vidéo** dans l’application.

```python
import streamlit as st

with open("exemple.mp4", "rb") as f:
    st.video(f.read(), format="video/mp4", start_time=0)
```

**Paramètres :**
* `data` : bytes, fichier ouvert (`io.BytesIO`) ou URL.
* `format` (str, optionnel) : type MIME. Exemples :

  * `"video/mp4"` pour MP4
  * `"video/ogg"` pour OGG
  * `"video/webm"` pour WebM
* `start_time` (float, optionnel) : seconde de départ pour la lecture.
* `caption` (str, optionnel) : légende sous la vidéo.
* `help` (str, optionnel) : texte d’aide au survol.
* `key` (str, optionnel) : identifiant unique.

**Retour :** aucun (lecteur intégré).

---
---
## Fonction d'affichage 
Parfait ! Voici les widgets **visualisation et graphiques** de Streamlit au format `.md` que tu utilises, avec tous les paramètres détaillés et exemples :

---

### `st.map()` <a id="stmap-"></a>

Affiche une **carte interactive** à partir de données géographiques.

```python
import streamlit as st
import pandas as pd

data = pd.DataFrame({
    'lat': [48.8566, 43.6047],
    'lon': [2.3522, 1.4442]
})

st.map(data, zoom=5)
```

**Paramètres :**
* `data` : DataFrame ou autre tableau avec colonnes `lat` et `lon`.
* `zoom` (int, optionnel) : niveau de zoom de la carte (0-20).
* **Notes :** Streamlit utilise `pydeck` en arrière-plan pour le rendu.

**Retour :** aucun (affiche la carte).

---

### `st.pyplot()` <a id="stpyplot-"></a>

Affiche une figure **Matplotlib** dans votre application Streamlit.

```python
import streamlit as st
import matplotlib.pyplot as plt

# Création d'une figure Matplotlib
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4], [10, 20, 30, 25], label="Ventes")
ax.set_title("Graphique des ventes")
ax.set_xlabel("Trimestre")
ax.set_ylabel("Ventes")
ax.legend()

# Affichage dans Streamlit
st.pyplot(fig)
```

**Paramètres :**
* `fig` (matplotlib.figure.Figure) : figure Matplotlib à afficher.
* `clear_figure` (bool, optionnel, défaut `True`) : si `True`, la figure est effacée après affichage pour éviter que les figures suivantes se superposent.
* `**kwargs` : arguments supplémentaires passés à `st._legacy_figure`, généralement peu utilisés par l’utilisateur final.

**Retour :** aucun (affiche directement la figure Matplotlib dans l’application).

**Notes :**
* Supporte toutes les fonctionnalités Matplotlib, y compris les sous-graphiques (`subplots`), légendes, titres et annotations.
* Utile pour intégrer vos visualisations scientifiques directement dans Streamlit sans avoir besoin de bibliothèques supplémentaires.

---
### `st.pydeck_chart()` <a id="stpydeck_chart-"></a>

Intègre des **visualisations avancées avec PyDeck** (cartographie 3D, couches multiples).

```python
import streamlit as st
import pydeck as pdk
import pandas as pd

df = pd.DataFrame({
    'lat': [48.8566, 43.6047],
    'lon': [2.3522, 1.4442],
    'value': [100, 200]
})

layer = pdk.Layer(
    "ScatterplotLayer",
    df,
    get_position=['lon', 'lat'],
    get_radius='value',
    get_color=[255, 0, 0],
    pickable=True
)

view_state = pdk.ViewState(latitude=46.0, longitude=2.0, zoom=5)

r = pdk.Deck(layers=[layer], initial_view_state=view_state)
st.pydeck_chart(r)
```

**Paramètres :**

* `deck` : objet `pdk.Deck` contenant les couches et la vue.
* `use_container_width` (bool, optionnel) : si `True`, le graphique s’adapte à la largeur du conteneur.

**Retour :** aucun (affiche le graphique PyDeck interactif).

---

### `st.graphviz_chart()` <a id="stgraphviz_chart-"></a>

Affiche un **graph ou diagramme** à partir du langage DOT (Graphviz).

```python
import streamlit as st

dot = """
digraph {
    A -> B
    B -> C
    A -> C
}
"""

st.graphviz_chart(dot)
```

**Paramètres :**
* `dot` (str ou `graphviz.Source`) : code DOT décrivant le graph.
* `use_container_width` (bool, optionnel) : ajuste la largeur du graph au conteneur.

**Retour :** aucun (affiche le diagramme Graphviz).

---

### `st.json()` <a id="stjson-"></a>

Affiche un **objet JSON** sous forme lisible et coloré.

```python
import streamlit as st

data = {"nom": "Alice", "âge": 25, "ville": "Paris"}
st.json(data)
```

**Paramètres :**
* `body` (dict, list, str) : données JSON à afficher.
* `expanded` (bool, optionnel) : si `True`, affiche tout le JSON ouvert par défaut.
* `height` (int, optionnel) : hauteur de la zone en pixels.

**Retour :** aucun (affiche le JSON).

---

### `st.bar_chart()` <a id="stbar_chart-"></a>

Crée un **diagramme en barres** simple.

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    "Année": [2020, 2021, 2022],
    "Ventes": [100, 150, 200]
})

st.bar_chart(df.set_index("Année"))
```

**Paramètres :**
* `data` (DataFrame, np.array, dict, list) : données à tracer.
* `width` (int, optionnel) : largeur du graphique en pixels.
* `height` (int, optionnel) : hauteur du graphique en pixels.
* `use_container_width` (bool, optionnel) : adapte automatiquement la largeur au conteneur.

**Retour :** aucun (affiche le graphique).

---
Parfait ! Voici la suite des widgets de visualisation Streamlit au format `.md` détaillé et cohérent avec ce que tu utilises :

---

### `st.line_chart()` <a id="stline_chart-"></a>

Crée un **graphique linéaire simple** à partir de données numériques.

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    "Mois": ["Jan", "Fév", "Mar", "Avr"],
    "Ventes": [100, 120, 90, 140]
})

st.line_chart(df.set_index("Mois"))
```

**Paramètres :**
* `data` (DataFrame, np.array, dict, list) : données à tracer.
* `width` (int, optionnel) : largeur du graphique en pixels.
* `height` (int, optionnel) : hauteur du graphique en pixels.
* `use_container_width` (bool, optionnel) : adapte automatiquement la largeur au conteneur.

**Retour :** aucun (affiche le graphique).

---

### `st.area_chart()` <a id="starea_chart-"></a>

Crée un **graphique en aires** pour visualiser des données cumulatives.

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    "Mois": ["Jan", "Fév", "Mar", "Avr"],
    "Ventes": [100, 120, 90, 140]
})

st.area_chart(df.set_index("Mois"))
```

**Paramètres :**

* `data` (DataFrame, np.array, dict, list) : données à tracer.
* `width` (int, optionnel) : largeur du graphique en pixels.
* `height` (int, optionnel) : hauteur du graphique en pixels.
* `use_container_width` (bool, optionnel) : adapte automatiquement la largeur au conteneur.

**Retour :** aucun (affiche le graphique).

---

### `st.altair_chart()` <a id="staltair_chart-"></a>

Affiche un graphique **Altair** interactif.

```python
import streamlit as st
import altair as alt
import pandas as pd

df = pd.DataFrame({
    'x': [1, 2, 3, 4],
    'y': [10, 20, 30, 25]
})

chart = alt.Chart(df).mark_line().encode(
    x='x',
    y='y'
)

st.altair_chart(chart, use_container_width=True)
```

**Paramètres :**
* `chart` : objet `alt.Chart`.
* `use_container_width` (bool, optionnel) : adapte la largeur au conteneur.

**Retour :** aucun (affiche le graphique Altair interactif).

---

### `st.plotly_chart()` <a id="stplotly_chart-"></a>

Affiche un graphique **Plotly** interactif.

```python
import streamlit as st
import plotly.express as px
import pandas as pd

df = pd.DataFrame({
    'Mois': ["Jan", "Fév", "Mar", "Avr"],
    'Ventes': [100, 120, 90, 140]
})

fig = px.line(df, x='Mois', y='Ventes')
st.plotly_chart(fig, use_container_width=True)
```

**Paramètres :**
* `figure` : objet Plotly (`go.Figure` ou `px` figure).
* `use_container_width` (bool, optionnel) : adapte automatiquement la largeur au conteneur.
* `sharing` (str, optionnel) : mode de partage (`'streamlit'` par défaut).

**Retour :** aucun (affiche le graphique Plotly interactif).

---

### `st.bokeh_chart()` <a id="stbokeh_chart-"></a>

Affiche un graphique **Bokeh** interactif.

```python
import streamlit as st
from bokeh.plotting import figure

p = figure(title="Exemple Bokeh", x_axis_label='x', y_axis_label='y')
p.line([1, 2, 3, 4], [10, 20, 30, 25], line_width=2)

st.bokeh_chart(p, use_container_width=True)
```

**Paramètres :**
* `figure` : objet `bokeh.plotting.figure`.
* `use_container_width` (bool, optionnel) : adapte la largeur au conteneur.

**Retour :** aucun (affiche le graphique Bokeh interactif).

---
---

## Fonction de Message d'alerte <a id="fonction-de-message-dalerte-"></a>

### `st.success()` <a id="stsuccess-"></a>

Affiche un message de succès encadré en vert.

```python
st.success("Opération réussie !")
```

**Paramètres :**
* `body` (str) : texte du message.
* `icon` (str ou None, optionnel) : icône affichée devant le message (par défaut "✅").

**Retour** : aucun.

**Notes :** 
* Utilisé pour signaler une réussite ou une action terminée correctement.

---

### `st.error()` <a id="sterror-"></a>

Affiche un message d’erreur encadré en rouge.

```python
st.error("Une erreur est survenue !")
```

**Paramètres :**
* `body` (str) : texte du message.
* `icon` (str ou None, optionnel) : icône affichée devant le message (par défaut "❌").

**Retour** : aucun.

**Notes :** 
* Idéal pour signaler une erreur critique ou bloquante.

---

### `st.warning()` <a id="stwarning-"></a>

Affiche un message d’avertissement encadré en jaune.

```python
st.warning("Attention : vérifiez vos données.")
```

**Paramètres :**
* `body` (str) : texte du message.
* `icon` (str ou None, optionnel) : icône affichée devant le message (par défaut "⚠️").

**Retour** : aucun.

**Notes :** 
* Utilisé pour attirer l’attention sur un point important ou potentiellement problématique.

---

### `st.info()` <a id="stinfo-"></a>

Affiche un message d’information encadré en bleu.

```python
st.info("Information : cette action est irréversible.")
```

**Paramètres :**
* `body` (str) : texte du message.
* `icon` (str ou None, optionnel) : icône affichée devant le message (par défaut "ℹ️").

**Retour** : aucun.
  
**Notes :** 
* Sert à fournir des informations utiles à l’utilisateur sans alerter.

---

### `st.exception()` <a id="stexception-"></a>

Affiche une exception Python avec son traceback complet.

```python
try:
    1 / 0
except Exception as e:
    st.exception(e)
```

**Paramètres :**
* `exception` (Exception) : objet exception Python à afficher.
* `icon` (str ou None, optionnel) : icône affichée devant le message (par défaut "❌").

**Retour** : aucun.

**Notes :** 
* Très utile pour le débogage et pour afficher les erreurs détaillées à l’utilisateur.

---
### `st.toast()` <a id="sttoast--streamlit--125"></a> (Streamlit >= 1.25)

Affiche un message temporaire flottant qui disparaît automatiquement après quelques secondes.

```python
st.toast("Opération effectuée avec succès !")
```

**Paramètres :**
* `body` (str) : texte affiché dans le toast.

* `icon` (str ou None, optionnel) : icône affichée devant le toast (par défaut "ℹ️").

**Retour** : aucun.

**Notes :** 
* Idéal pour des notifications non intrusives ou temporaires.
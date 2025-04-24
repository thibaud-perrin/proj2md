# Cahier des charges : Proj2MD

## 1. Contexte et objectif

**But du projet**\
Développer un **package Python** nommé `proj2md` (ou équivalent) qui, via une
unique commande CLI, parcourt un dossier de projet, extrait sa structure et son
contenu, puis génère un **fichier Markdown** complet et auto-descriptif. Ce
document servira de base d’ingestion pour un LLM, ou de documentation statique
pour un développeur.

---

## 2. Fonctionnalités principales

1. **Parcours récursif**
   - Lecture de tous les fichiers du répertoire d’entrée, avec possibilité de
     filtrer par extension (par défaut `.py`, `.md`, `.yaml`, `.json`).
2. **Génération de l’arborescence**
   - Affichage optionnel d’une vue “tree” ASCII.
3. **Extraction de contenu**
   - Pour chaque fichier :
     - Titre de niveau 3 (`###`) décrivant le chemin complet relatif.
     - Bloc de code Markdown avec le contenu intégral du fichier.
4. **Table des matières automatique**
   - Liens vers chaque section/fichier.
5. **Flags / Options CLI**
   - `--input-dir <path>` : dossier racine du projet (par défaut `.`).
   - `--output-file <path>` : chemin du fichier Markdown généré (par défaut
     `project.md`).
   - `--no-deps` / `--with-deps` : activer ou désactiver la liste des
     dépendences.
   - `--no-tree` / `--with-tree` : activer ou désactiver l’arborescence.
   - `--extensions <ext1,ext2,…>` : liste d’extensions à inclure.
   - `--mode <light|full>` :
     - `light` : seulement arborescence + README existant.
     - `full` : extraction complète de tous les fichiers.
   - `--max-snippet-lines <n>` : (optionnel) limiter l’affichage à n lignes par
     fichier.
   - `--exclude <pattern>` : motifs de fichiers ou dossiers à ignorer (ex.
     `tests/*`).
6. **Front-matter YAML**
   - Bloc en tête avec :
     ```yaml
     project_name: "<nom_du_projet>"
     version: "<version>"
     author: "<auteur>"
     date_generated: "<YYYY-MM-DD>"
     ```
7. **Publication**
   - Structure du package standard (`pyproject.toml`, `setup.cfg`, `README.md`,
     etc.)
   - Commande console : `proj2md` après installation (`pip install .`).

---

## 3. Structure du Markdown généré

````markdown
---
project_name: "mon_projet"
version: "0.1.0"
author: "Auteur Nom"
date_generated: "2025-04-24"
---

# mon_projet

> **Version** : 0.1.0\
> **Auteur** : Auteur Nom

---

## Table des matières

1. [Arborescence du projet](#arborescence-du-projet)
2. [Fichiers détaillés](#fichiers-détaillés)

---

## Arborescence du projet

```text
.
├── README.md
├── setup.py
├── src/
│   ├── module1.py
│   └── utils.py
└── tests/
    └── test_module1.py
```

---

## Dépendances du projet

```text
- numpy
- pytorch
- ...
```
````

---

## Fichiers détaillés

### `README.md`

```markdown
# Mon Projet

Description du projet…
```

---

_(Répéter pour chaque fichier inclus, avec la syntaxe et identifiants
appropriés)_

---

## 4. Exemples d’utilisation

```bash
# Mode complet, arbre inclus
proj2md --input-dir ./mon_projet --output-file ./doc.md --with-tree --mode full

# Mode léger, filtrage extensions
proj2md -i ./src -o projet_light.md --no-tree --extensions .py,.md
```

---

## 5. Tests et CI

- Fichiers de tests pour chaque option CLI (pytest ou unittest).
- Intégration continue (GitHub Actions) :
  - Linting (flake8, black)
  - Tests unitaires
  - Packaging & publication sur PyPI (optionnel)

---

## 6. Livrable attendu

Un **package Python** publiable sur PyPI et installable localement, fournissant
la commande `proj2md` permettant de générer, à partir d’un dossier de projet, un
**unique** fichier Markdown détaillant :

- Le **YAML front-matter**
- La **table des matières**
- L’**arborescence** (optionnelle)
- Le contenu intégral de chaque fichier (path en titre H3 + bloc de code)

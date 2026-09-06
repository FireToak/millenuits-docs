# SP 2 - Mission 1 - Mise en place MkDocs

**SP 2 : Gestion parc informatique**

**Mission 1 : Création d'une documentation avec MkDocs et GitHub Pages**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 05/02/2026
- **Dernière modification** : 05/02/2026
- **Auteur** : MEDO Louis

---
## Sommaire

- A. Installation et utilisation locale de MkDocs
- B. Automatisation du déploiement (CI/CD)
- C. Fonctionnement du dépôt

---
## Objectif

Cette procédure permet d'installer le générateur de site statique MkDocs sur un environnement Windows, de le configurer avec le thème "Material", et d'automatiser son déploiement sur GitHub Pages via les GitHub Actions.

---
## Prérequis

* Python 3.x installé sur la machine.
* Git installé et configuré.
* Un compte GitHub et un dépôt créé.
* VS Code (ou autre éditeur de texte).

---
## A. Installation et utilisation locale de MkDocs

### 1. Installation des dépendances

1. **Mise à jour de pip.** Mise à jour du gestionnaire de paquets Python.
```bash
python.exe -m pip install --upgrade pip
```

* `python.exe -m pip` : Exécute le module pip via l'interpréteur Python (évite les soucis de PATH).
* `install` : Commande pour installer un paquet.
* `--upgrade` : Option forçant la mise à jour si le paquet existe déjà.

2. **Installation de MkDocs Material.** Installation du framework MkDocs avec le thème visuel Material.
```bash
pip install mkdocs-material
```

3. **Vérification.** Contrôle de la bonne installation.
```bash
python -m mkdocs --version
```

* `--version` : Affiche le numéro de version installé.

### 2. Initialisation du projet

1. **Création de la structure.** Création du dossier qui contiendra la documentation (selon l'arborescence du projet `docs_millenuits`).
```bash
python -m mkdocs new docs_millenuits
```

* `new` : Commande pour générer l'échafaudage de base (fichier yaml et dossier docs).
* `docs_millenuits` : Nom du dossier racine de la documentation.

2. **Configuration.** Modification du fichier `docs_millenuits/mkdocs.yaml`.
```yaml
site_name: Documentation - Millenuits
theme:
  name: material            # Définition du thème visuel
  language: fr              # Langue de l'interface

plugins:
  - search                  # Active la barre de recherche interne
```

### 3. Utilisation courante

1. **Prévisualisation locale.** Lancement d'un serveur web local pour voir le rendu en direct.
```bash
python -m mkdocs serve
```

* `serve` : Démarre un serveur de développement (généralement sur localhost:8000) avec rechargement automatique à chaque modification de fichier.

2. **Compilation manuelle (Optionnel).** Génération des fichiers HTML statiques.
```bash
python -m mkdocs build
```

* `build` : Convertit les fichiers Markdown en HTML dans le dossier `site/`.

---
## B. Automatisation du déploiement (CI/CD)

### 1. Configuration du Workflow

1. **Création du dossier.** Créer l'arborescence `.github/workflows` à la racine du dépôt.
2. **Création du fichier de pipeline.** Créer le fichier `publish.yaml` avec le contenu suivant :
```yaml
name: Deploy MkDocs
on:
  push:
    branches:
      - main                # Déclencheur : push sur la branche main

permissions:
  contents: write           # Nécessaire pour que le bot puisse écrire sur la branche gh-pages

jobs:
  deploy:
    runs-on: ubuntu-latest  # Environnement virtuel Linux
    steps:
      - uses: actions/checkout@v4
        # Récupère le code source du dépôt

      - uses: actions/setup-python@v5
        with:
          python-version: 3.11
        # Installe Python dans l'environnement virtuel

      - run: pip install mkdocs-material
        # Installe les dépendances nécessaires à la compilation

      - run: mkdocs gh-deploy --config-file docs_millenuits/mkdocs.yaml --force
        # Compile et déploie le site
```

* `on: push`: Définit l'événement qui lance l'action.
* `runs-on`: Spécifie le système d'exploitation du conteneur (runner).
* `actions/checkout`: Action officielle permettant au script d'accéder aux fichiers du dépôt.
* `mkdocs gh-deploy`: Commande spécifique à MkDocs pour compiler et pousser le résultat sur la branche `gh-pages`.
* `--config-file`: Indique le chemin spécifique du fichier de configuration (car il n'est pas à la racine).
* `--force`: Force l'écrasement de l'historique de la branche de déploiement si nécessaire.

### 2. Mise en production

1. **Envoi sur GitHub.** Pousser les fichiers de configuration et le workflow.
```bash
git add .
git commit -m "Ajout pipeline CI/CD MkDocs"
git push -u origin main
```

* `add .` : Ajoute tous les fichiers modifiés à l'index (staging area).
* `commit -m` : Enregistre les modifications avec un message descriptif.
* `push` : Envoie les commits locaux vers le serveur distant (GitHub).

### 3. Activation GitHub Pages

1. Aller dans l'onglet **Settings** du dépôt GitHub.
2. Menu **Pages** (barre latérale gauche).
3. Dans **Build and deployment** > **Branch**, sélectionner `gh-pages` et `/ (root)`.
4. Cliquer sur **Save**.
### 4. Vérification finale

Accéder à l'URL fournie par GitHub (ex: `https://ap-bts-sio-louis.github.io/millenuits/`).

---
## C. Fonctionnement du dépôt

[ap-bts-sio-louis.github.io/millenuits/](https://ap-bts-sio-louis.github.io/millenuits/ "https://ap-bts-sio-louis.github.io/millenuits/")
### Organisation de l'arborescence

Le dépôt est structuré pour séparer la configuration technique, l'automatisation et la documentation métier.

| Dossier / Fichier | Description |
| --- | --- |
| **.github/workflows/** | Contient les scripts d'automatisation (CI/CD). Ici, `publish.yaml` gère la compilation et la publication automatique du site lors d'une modification. |
| **config/** | Contient les fichiers de configuration technique des équipements réseau (Switchs, Routeurs) et les données VLAN (`vlan.dat`). Ce dossier est séparé de la documentation pour être exploitable directement par des scripts ou des techniciens. |
| **docs_millenuits/** | Dossier racine du projet MkDocs. Il isole l'environnement de documentation du reste du dépôt. |
| ↳ **mkdocs.yaml** | Fichier de configuration principal du site (nom, thème, plugins, structure de navigation). |
| ↳ **docs/** | Contient les fichiers sources en Markdown (`.md`). C'est le contenu brut qui sera transformé en page HTML. |
|     ↳ **index.md** | Page d'accueil du site de documentation. |
|     ↳ **01-situation...** | Dossier regroupant les missions liées à l'infrastructure réseau. |
|     ↳ **02-situation...** | Dossier regroupant les missions liées à la gestion du parc informatique (dont cette procédure). |
| **images/** | Stockage des ressources statiques globales (logos, schémas d'architecture) utilisées à la fois dans le `readme.md` racine et dans les pages de documentation. |
| **readme.md** | Fichier d'accueil du dépôt GitHub, présentant le projet globalement (avant même d'aller sur le site de documentation). |

---
## Notes importantes

* **Chemins d'images** : Dans les fichiers Markdown situés dans `docs_millenuits/docs/`, pour utiliser une image du dossier racine `images`, il faut utiliser le chemin relatif `../../images/nom_image.png` ou l'URL absolue GitHub (moins recommandé pour le hors-ligne).
* **Indentation YAML** : Le fichier `publish.yaml` est très sensible à l'indentation (espaces). Ne pas utiliser de tabulations.

---
## Bibliographie

* [Documentation officielle MkDocs](https://www.mkdocs.org/)
* [Documentation Thème Material](https://squidfunk.github.io/mkdocs-material/)
* [GitHub Actions Documentation](https://docs.github.com/en/actions)
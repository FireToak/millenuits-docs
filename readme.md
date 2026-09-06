# BTS SIO - Documentation - Millenuits

![Bannière Millenuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

🪢 *Accéder à la documentation :* [Documentation - Millenuits](https://millenuits.bts.loutik.fr)

## A. Contexte de la situation professionnelle

Millenuits est une entreprise en forte croissance spécialisée dans la fabrication de couettes et d'oreillers, répartie sur deux sites (Baugé-en-Anjou et Joué-lès-Tours).

**Problématiques :** L'entreprise a récemment subi des incidents de sécurité (propagation de virus via USB) et son réseau actuel manque de segmentation. Parallèlement, le parc informatique vieillissant nécessite un renouvellement, le support utilisateur manque de suivi, et les développeurs ne disposent pas d'un environnement de test isolé, ce qui crée des conflits et menace la production.

**Objectifs :** La DSI a lancé un plan de refonte divisé en quatre missions principales :

1.  **Infrastructure :** Segmenter et sécuriser le réseau (VLAN, adressage VLSM, Wi-Fi visiteurs/commerciaux).
2.  **Parc informatique :** Moderniser les postes de travail (Windows 11), automatiser le déploiement (FOG) et intégrer un outil de gestion d'incidents.
3.  **Services principaux :** Centraliser les identités (Active Directory, DNS) et automatiser l'adressage (DHCP sous Linux).
4.  **Espace de développement :** Créer une DMZ interne conteneurisée (Docker) et un réseau Wi-Fi isolé et sécurisé pour les développeurs.

### A.1 Notions mises en place

L'ensemble des projets aborde des compétences transversales et techniques variées :

**Infrastructure réseau :**

  * Conception de plans d'adressage (VLSM).
  * Segmentation et sécurisation par VLANs (Isolation des flux Production/Admin/Visiteurs).
  * Routage et translation d'adresses (NAT/PAT).

**Administration système :**

  * Gestion des environnements Windows Server et Linux.
  * Services réseaux (DNS, DHCP, AD, NAS).

**Environnement de développement & sécurité (SP4) :**

  * Conteneurisation de services et gestion avec Docker / Docker Compose.
  * Création d'une DMZ interne pour l'isolation des environnements de test.
  * Déploiement de portail captif et sécurisation avancée du Wi-Fi (SSID caché).

**Méthodologie de projet :**

  * Gestion des tâches et planification (Notion/Kanban).
  * Rédaction de documentation technique et fonctionnelle (Markdown, MkDocs).
  * Travail collaboratif et gestion de version (Git).

-----

## B. Organisation du dépôt

Le dépôt est organisé de manière chronologique et modulaire, chaque dossier correspondant à une **Situation Professionnelle (SP)** spécifique rencontrée par l'entreprise.

```
millenuits/
├── .github/ workflows/     # Pipelines CI/CD
├── config/                 # Configurations des équipements réseau
├── images/                 # Ressources graphiques globales du dépôt
└── docs_millenuits/        # Cœur du projet de documentation (Propulsé par MkDocs)
    ├── mkdocs.yaml         # Fichier de configuration MkDocs
    └── docs/               # Fichiers sources de la documentation
        ├── 01-situation-*/ # SP 1 : Documentation de l'infrastructure réseau
        ├── 02-situation-*/ # SP 2 : Documentation du parc informatique
        ├── 03-situation-*/ # SP 3 : Documentation des services principaux
        ├── 04-situation-*/ # SP 4 : Documentation de l'environnement de développement
        └── ressources/     # Référentiel transversal
```

-----

## C. Comment modifier la documentation ?

Pour contribuer ou mettre à jour la documentation, suivez cette procédure Git standard :

1.  **Cloner le dépôt en local :**

    ```bash
    git clone https://github.com/AP-BTS-SIO-Louis/millenuits.git
    cd millenuits
    ```

      * `git clone [url]` : Télécharge une copie complète du dépôt distant sur votre machine locale.
      * `cd [dossier]` : Change le répertoire courant pour entrer dans le dossier nouvellement cloné.

2.  **Créer ou modifier les fichiers :** Éditez les fichiers `.md` situés dans l'arborescence correspondante.

3.  **Indexer les modifications :**

    ```bash
    git add .
    ```

      * `git add .` : Ajoute tous les fichiers modifiés, supprimés ou créés dans le répertoire courant à la zone de préparation (staging area) avant de créer une version.

4.  **Créer un commit descriptif :**

    ```bash
    git commit -m "docs: ajout de la procédure de réinitialisation du routeur"
    ```

      * `git commit -m "[message]"` : Enregistre les modifications préparées dans l'historique local avec un message descriptif permettant de comprendre l'évolution.

5.  **Pousser les modifications :**

    ```bash
    git push origin main
    ```

      * `git push origin main` : Envoie vos commits locaux vers le dépôt distant ("origin") sur la branche spécifiée (ici "main").

*Une fois le `push` effectué, la chaîne CI/CD via GitHub Actions compilera automatiquement les fichiers et déploiera la nouvelle version du site MkDocs.*

-----

## **👥 Auteurs**

Ce contexte est réalisé par des étudiants en BTS SIO au lycée Paul-Courier (Tours).

  * **Louis MEDO** - [LinkedIn](https://www.linkedin.com/in/louismedo/) | [Portfolio](https://louis.loutik.fr/) | [GitHub](https://github.com/FireToak)
  * **Louis BISERAY** - [LinkedIn](#) | [Portfolio](#) | [GitHub](#)

----

<div align="center">
  <br/>
  <small><i>Dernière mise à jour : 30 avril 2026</i></small>
</div>

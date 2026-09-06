# **📚 Introduction**

![Bannière Millenuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

Bienvenue sur le site de documentation technique du projet **MilleNuits**. Ce site centralise l'ensemble des procédures, architectures et configurations mises en place dans le cadre de la refonte de l'infrastructure réseau et de la gestion du parc informatique de l'entreprise.

---

## **1. 🏢 Contexte**

L'entreprise Mille Nuits connaît une croissance importante nécessitant la modernisation de son infrastructure informatique. Suite à des incidents de sécurité liés à la propagation de virus, la DSI a décidé de segmenter le réseau, de sécuriser les accès, de renouveler le parc informatique vieillissant et de structurer la gestion des services et des incidents.

### **SP1 - Gestion de l'infrastructure réseau**

L'objectif est de sécuriser les flux de l'entreprise et de préparer sa croissance en segmentant le réseau physique et logique.

  - Définition d'un nouveau plan d'adressage (VLSM).
  - Maquettage et mise en place de l'infrastructure réseau (VLAN, routage).
  - Mise en place d'accès Wi-Fi sécurisés et dédiés (Visiteurs et Commerciaux).

### **SP2 - Gestion du parc informatique**

L'objectif est de remplacer les postes clients obsolètes et d'industrialiser les processus de déploiement et de support.

  - Mise en place d'un système de documentation en ligne (MkDocs).
  - Création d'un master et installation des nouveaux postes sous Windows 11.
  - Déploiement automatisé des postes via la solution FOG.
  - Mise en place d'un outil de gestion d'incidents (ticketing).

### **SP3 - Gestion des services principaux AD et DHCP**

L'objectif est de centraliser la gestion des identités, d'automatiser la configuration réseau des hôtes et de sécuriser le stockage.

  - Mise en place d'un contrôleur de domaine Active Directory et DNS (Windows Server 2019).
  - Mise en place d'un serveur DHCP sous Linux.
  - Déploiement d'un serveur NAS avec authentification AD et redirection de dossiers.

### **SP4 - Mise en place d'un espace de développement**

L'objectif est de fournir un environnement isolé, moderne et sécurisé pour les équipes de développement.

  - Mise en place d'une DMZ interne conteneurisée avec Docker.
  - Création d'un sous-réseau dédié aux développeurs avec accès Wi-Fi sécurisé (SSID caché).
  - Mise en place d'un portail captif pour le filtrage et l'authentification.

---

## **2. 🎯 Compétences**

  - **Gérer le patrimoine informatique**
    * Recenser et identifier les ressources numériques.
    * Mettre en place et vérifier les niveaux d'habilitation associés à un service.
  - **Répondre aux incidents et aux demandes d'assistance et d'évolution**
    * Traiter des demandes concernant les services réseau et système, applicatifs.
    * Collecter, suivre et orienter des demandes.
  - **Concevoir une solution d'infrastructure réseau**
    * Élaborer un dossier de choix d'une solution d'infrastructure et rédiger les spécifications techniques.
    * Maquetter et prototyper une solution d'infrastructure permettant d'atteindre la qualité de service attendue.
  - **Installer, tester et déployer une solution d'infrastructure réseau**
    * Installer et configurer des éléments d'infrastructure.
    * Rédiger ou mettre à jour la documentation technique et utilisateur d'une solution d'infrastructure.
  - **Assurer la cybersécurité d'une infrastructure réseau, d'un système, d'un service**
    * Prendre en compte la sécurité dans un projet de mise en œuvre d'une solution d'infrastructure.
    * Mettre en œuvre et vérifier la conformité d'une infrastructure à un référentiel, une norme ou un standard de sécurité.

-----

## **3. 🛠️ Comment utiliser la documentation ?**

Ce site de documentation est généré automatiquement à partir de fichiers Markdown hébergés depuis le dépôt : [millenuits](https://github.com/firetoak/millenuits-docs)

### **3.1 Structure de la documentation**

  - **01 à 04 - Situations (Infrastructure, Parc, Services AD/DHCP, Développement) :** Ces dossiers contiennent l'ensemble des livrables, documentations techniques et fiches de tests relatifs à chaque mission spécifique des quatre situations professionnelles.
  - **Ressources :** Ce répertoire regroupe les éléments transverses du projet. Il contient les configurations brutes des équipements (Cisco 1921, 2960), les schémas topologiques, les tableaux de bord (matrice des flux, plan d'adressage, table de routage) ainsi que le socle technique (procédures Linux Debian, guides de documentation).

### **3.2 Modifier la documentation**

Pour contribuer ou mettre à jour la documentation, suivez cette procédure Git standard :

1.  **Cloner le dépôt en local :**
    ```bash
    git clone https://github.com/AP-BTS-SIO-Louis/millenuits.git
    cd millenuits
    ```
2.  **Créer ou modifier les fichiers :** Éditez les fichiers `.md` situés dans l'arborescence correspondante.
3.  **Indexer les modifications :**
    ```bash
    git add .
    ```
4.  **Créer un commit descriptif :**
    ```bash
    git commit -m "docs: ajout de la procédure de réinitialisation du routeur"
    ```
5.  **Pousser les modifications :**
    ```bash
    git push origin main
    ```

*Une fois le `push` effectué, la chaîne CI/CD via GitHub Actions compilera automatiquement les fichiers et déploiera la nouvelle version du site MkDocs.*

---

## **👥 Auteurs**

Ce contexte est réalisé par des étudiants en BTS SIO au lycée Paul-Courier (Tours).

  * **Louis MEDO** - [LinkedIn](https://www.linkedin.com/in/louismedo/) | [Portfolio](https://louis.loutik.fr/) | [GitHub](https://github.com/FireToak)
  * **Louis BISERAY** - [LinkedIn](#) | [Portfolio](#) | [GitHub](#)
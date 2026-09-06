# SP 3 - Mission 3 - Synchronisation AD

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 3 : Relier un NAS à l'AD

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 02/04/2026
- **Dernière modification** : 02/04/2026
- **Auteur** : BISERAY Louis

___

## 1. Présentation du projet

L'objectif de cette mission est de relier notre serveur de stockage **TrueNAS** à notre contrôleur de domaine **Active Directory (AD)**. Cette centralisation nous permet d'éviter la double saisie des comptes utilisateurs : les identifiants créés sur l'AD sont automatiquement reconnus par le NAS pour l'attribution des droits d'accès.

---

## 2. Préparation de l'environnement Active Directory

Avant de configurer le NAS, nous devons préparer l'annuaire Windows pour accueillir cet équipement.

### Création du compte de service et délégation

1. Nous nous connectons en RDP sur notre serveur AD (**172.16.51.1**) avec un compte administrateur.
    
2. Dans la console **Utilisateurs et ordinateurs Active Directory**, nous créons une nouvelle **Unité d'Organisation (OU)** dédiée à nos infrastructures.
    
3. Nous créons un utilisateur nommé `TrueNas_Service` (ou un nom explicite pour le NAS).
    
4. **Gestion des droits :** * Nous créons un groupe de sécurité nommé `GRP_TrueNas_Admin`.
    
    - Nous y ajoutons notre utilisateur `TrueNas_Service`.
        
    - Nous effectuons une **Délégation de contrôle** sur l'OU des utilisateurs pour autoriser ce groupe à "Lire toutes les informations sur les utilisateurs" et "Gérer les comptes d'utilisateurs".
        

---

## 3. Configuration de la liaison sur TrueNAS

Une fois l'AD prêt, nous passons sur l'interface de gestion de TrueNAS pour établir le pont.

### Procédure de jonction au domaine

1. Nous nous rendons dans l'onglet **Directory Services** > **Active Directory**.
    
2. Nous renseignons les champs suivants :
    
    - **Domain Name :** Notre nom de domaine complet (ex: `millenuits.local`).
        
    - **Domain Account :** Le compte de service créé précédemment.
        
    - **Domain Password :** Le mot de passe associé.
        
3. Nous cochons la case **Enable**.
    
4. **Note technique :** Si la liaison échoue, nous vérifions impérativement la synchronisation de l'heure du système (FreeBSD) avec celle de l'AD. Un décalage de plus de 5 minutes bloque l'authentification Kerberos.
    

---

## 4. Gestion du stockage et des permissions

Maintenant que le lien est actif, nous devons organiser nos données.

### Création des Datasets

Nous allons dans **Storage** > **Pools** pour créer nos partitions logiques :

- Sur notre Pool principal, via les options (trois points), nous sélectionnons **Add Dataset**.
    
- **Dataset 1 :** Nom : `Admin` | Share Type : `SMB`.
    
- **Dataset 2 :** Nom : `Service` | Share Type : `SMB`.
    

### Configuration fine des ACL (Permissions)

C'est l'étape cruciale où nous lions nos groupes AD aux dossiers :

1. Pour chaque Dataset (ex: Admin), nous cliquons sur **Edit Permissions** puis **Use ACL Manager**.
    
2. Nous appliquons le template **Restricted** pour purger les accès par défaut.
    
3. **Ajout des accès :**
    
    - **Who :** Group
        
    - **Group :** Nous recherchons notre groupe AD (format : `DOMAINE\Nom_du_Groupe`).
        
    - **Permissions :** Full Control.
        
    - **Flags :** Inherit (pour que les sous-dossiers héritent de ces droits).
        
4. Nous supprimons systématiquement les entrées `everyone` ou `builtin_users`.
    
5. Nous cochons **Apply recursively** avant de sauvegarder.
    

---

## 5. Partage réseau et optimisation

Pour rendre ces dossiers accessibles sur les postes de travail :

1. Nous allons dans **Sharing** > **Windows Shares (SMB)**.
    
2. Nous ajoutons un partage pointant vers nos Datasets respectifs (ex: `/mnt/pool/Admin`).
    
3. **Optimisation "Access Based Enumeration" (ABE) :** Afin qu'un utilisateur ne voie que les dossiers auxquels il a droit, nous activons l'ABE :
    
    - Dans les paramètres du partage, nous cliquons sur **Advanced Options**.
        
    - Nous cochons la case **Access Based Enumeration**.
        
    - Ainsi, si un membre du groupe "Service" n'a pas de droits sur le dossier "Admin", ce dernier sera totalement invisible pour lui sur le réseau.
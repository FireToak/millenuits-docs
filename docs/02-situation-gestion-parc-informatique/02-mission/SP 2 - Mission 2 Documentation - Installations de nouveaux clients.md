**SP 2 : Gestion du Parc Informatique**

**Mission 2 : Installation du PC maître**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

___
## Informations générales

- __Auteur__ : Biseray Louis
- __Date de création__ : 05/02/2026

___
## 1. Introduction

L'objectif de cette procédure est la création d'une image disque de référence (**Maitre**) pour le parc informatique de MilleNuits. Cette méthode garantit l'homogénéité des postes de travail, facilite la maintenance et réduit le temps de déploiement initial.

## 2. Spécifications de l'Environnement de Travail

Afin d'isoler la configuration des contraintes matérielles physiques, le maitre est réalisé sur un environnement virtualisé.

### 2.1. Configuration de l'Hyperviseur (VirtualBox)

- **Nom de la VM :** `Master_Win11_2026`

- **Système d'exploitation :** Windows 11 (64-bit)

- **Mémoire vive :** 4 Go (minimum conseillé : 8 Go pour la fluidité)

- **Disque Dur :** 30 Go 

- **Sécurité :** Activation de l'EFI 


### 2.2. Vérification de l'image source (ISO)

L'ISO doit être téléchargée depuis le portail officiel Microsoft. Avant toute installation, l'intégrité du fichier doit être vérifiée via la commande PowerShell : `Get-FileHash .\Win11_French_x64.iso -Algorithm SHA256`

---

## 3. Déploiement du Système d'Exploitation

### 3.1. Phase d'installation

L'installation est effectuée sans clé de produit (licence de volume appliquée après déploiement). Le partitionnement est laissé par défaut en mode "Espace non alloué" pour laisser Windows créer les partitions système (EFI, Récupération, MSR).

### 3.2. Contournement OOBE (Out-Of-Box Experience)

Pour éviter la liaison avec un compte Microsoft (Cloud), la procédure suivante est appliquée :

1. Choix de la région et du clavier.

2. Option **"Se joindre au domaine à la place"** pour forcer un compte local.

3. Création d'un utilisateur de transition : `ThrowAway`.


---

## 4. Personnalisation et Administration

### 4.1. Gestion des privilèges (LUA - Least-privileged User Account)

Le compte d'administration final est créé via l'outil **Netplwiz** pour garantir une configuration propre des groupes locaux.

- **Identifiant :** `Admin`

- **Groupe :** `Administrateurs`

- **Action :** Suppression du profil `ThrowAway` et de son dossier utilisateur dans `C:\Users\`.


### 4.2. Socle Logiciel Standard (SLS)

Les logiciels sont installés dans leur version "Stable" la plus récente :

1. **Navigateur :** Mozilla Firefox (Paramétré par défaut).

2. **Bureautique :** LibreOffice (Version x64).

3. **PDF :** Adobe Acrobat Reader.

4. **Multimédia :** VLC Media Player.


---

## 5. Préparation à la Capture (Sysprep)

Cette étape est la plus critique. Elle prépare le système au clonage en supprimant les identifiants uniques (**SID**) et en réinitialisant l'activation.

### 5.1. Prérequis à la généralisation

- **Désactivation de BitLocker :** Obligatoire pour permettre la capture de l'image par des outils tiers.

- **Nettoyage du disque :** Suppression des fichiers temporaires et des caches de mise à jour (Windows Update).


### 5.2. Exécution du Sysprep

L'outil est exécuté en ligne de commande ou via l'interface graphique : `C:\Windows\System32\Sysprep\sysprep.exe /audit /generalize /shutdown`

---

## 6. Exportation et Archivage

Le master est figé. La machine virtuelle est exportée au format **Open Virtualization Format (.OVA)**. Ce fichier est le "master" pour les futurs déploiements sur le réseau MilleNuits.

___
## 7. Fiche test

| Validation | Test à réaliser                                                                         | Résultat attendu                                                                   | Commentaires |
| ---------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ------------ |
|            | **Lancer Windows**<br><br>Démarrer Windows pour vérifier l'état du client               | Windows doit booter sur le compte de base et être utilisable immédiatement         |              |
|            | **Vérification des installation**<br><br>Essayer de lancer les 4 application installer  | Les 4 applications doivent s'exécuter sans erreur                                  |              |
|            | **Droits d'administration**<br><br>Essayer d'exécuter une application en administrateur | Une fenêtre demandant le login et mot de passe de l'administrateur doit apparaitre |              |

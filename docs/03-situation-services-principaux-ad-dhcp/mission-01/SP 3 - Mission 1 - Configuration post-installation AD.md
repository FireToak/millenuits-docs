# SP 3 - Mission 1 - Configuration post-installation AD

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 1 : Mise en place du serveur Windows Server 2019**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 05/02/2026
- **Dernière modification** : 21/03/2026
- **Auteur** : MEDO Louis

---

## Sommaire

1. [Création d'une unité d'organisation](#1-creation-dune-unitee-dorganisation)
2. [Création d'un utilisateur](#2-creation-dun-utilisateur)
3. [Sécurisation du service DNS (Désactivation de la récursivité)](#3-securisation-du-service-dns-desactivation-de-la-recursivite)

---

## 1. Création d'une unité d'organisation {#1-creation-dune-unitee-dorganisation}

> L'objectif d'une Unité d'Organisation (UO) est de structurer logiquement l'annuaire Active Directory. Pour le réseau MILLENUITS, la bonne pratique exige de créer une UO distincte pour chaque service de l'entreprise. Chaque UO regroupera les utilisateurs, les postes de travail et les imprimantes propres à ce service, facilitant la délégation d'administration et l'application des stratégies de groupe (GPO).

1. **Ouverture de la console.** Depuis le **Gestionnaire de serveur**, cliquez sur le menu **Outils**, puis sélectionnez **Utilisateurs et ordinateurs Active Directory**.

2. **Initialisation de la création.** Dans l'arborescence à gauche, faites un clic droit sur le nom du domaine (ou l'UO parente), sélectionnez **Nouveau**, puis **Unité d'organisation**.

3. **Paramétrage.** Renseignez le nom du service (ex: `Comptabilite`, `Ressources_Humaines`).

> 💡 **Conseil :** Laissez toujours la case "Protéger le conteneur contre une suppression accidentelle" cochée pour sécuriser l'arborescence contre les erreurs de manipulation.

4. **Validation.** Cliquez sur **OK** pour finaliser la création. Recommencez l'opération pour créer des sous-UOs si nécessaire (ex: UO "Utilisateurs" et UO "Ordinateurs" dans l'UO du service).

---

## 2. Création d'un utilisateur {#2-creation-dun-utilisateur}

> La création d'un utilisateur permet d'attribuer une identité unique sur le domaine. Sur le réseau MILLENUITS, il est impératif de respecter une convention de nommage standardisée (ex: *p.nom* pour la première lettre du prénom et le nom). L'utilisateur doit être créé directement au sein de l'UO de son service d'affectation pour hériter des bons droits et paramètres.

1. **Sélection de l'emplacement.** Dans **Utilisateurs et ordinateurs Active Directory**, naviguez et cliquez sur l'UO du service concerné.

2. **Initialisation de la création.** Faites un clic droit dans la zone centrale vide, choisissez **Nouveau**, puis **Utilisateur**.

3. **Saisie de l'identité.** Renseignez les champs **Prénom** et **Nom de famille**. Le champ **Nom d'ouverture de session de l'utilisateur** (le login) doit respecter la nomenclature établie. Cliquez sur **Suivant**.

4. **Configuration de la sécurité.** Saisissez un mot de passe temporaire respectant la politique de complexité (au moins 8 caractères, majuscules, minuscules, chiffres, caractères spéciaux).

> 💡 **Conseil :** Cochez impérativement l'option "L'utilisateur doit changer le mot de passe à la prochaine ouverture de session". Cela garantit la stricte confidentialité du mot de passe définitif de l'employé.

5. **Validation.** Cliquez sur **Suivant**, vérifiez le récapitulatif des informations, puis cliquez sur **Terminer**.

---

## 3. Sécurisation du service DNS (Désactivation de la récursivité) {#3-securisation-du-service-dns-desactivation-de-la-recursivite}

> L'objectif est de limiter la surface d'attaque. Par défaut, un serveur DNS Windows agit comme un résolveur récursif : s'il ne connaît pas une adresse, il interroge d'autres serveurs sur Internet. Désactiver cette fonction empêche le serveur d'être utilisé pour des attaques par empoisonnement de cache (DNS cache poisoning) ou des attaques par amplification.

1. **Désactivation via PowerShell.** Ouvrez une console PowerShell en tant qu'administrateur pour appliquer le paramètre de sécurité.

   **Commande à exécuter :**
   ```powershell
   Set-DnsServerRecursion -Enable $false
   ```
   - `Set-DnsServerRecursion` : Commande permettant de modifier les paramètres de récursivité du serveur DNS.
   - `-Enable $false` : Désactive la fonctionnalité. Le serveur ne répondra plus qu'aux requêtes concernant sa propre zone locale (ex: `millenuits.local`).

> 💡 **Conseil :** Attention, en désactivant la récursivité, ce contrôleur de domaine ne pourra plus résoudre les noms de domaine Internet (comme `google.fr`) pour les postes clients du réseau. Appliquez cette restriction de sécurité uniquement si vos clients utilisent un autre système pour naviguer sur Internet (comme un proxy ou un résolveur DNS dédié), ou si l'environnement est strictement isolé.
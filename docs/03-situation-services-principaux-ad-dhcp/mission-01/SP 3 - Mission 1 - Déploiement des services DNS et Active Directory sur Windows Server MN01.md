# SP 3 - Mission 1 - Déploiement des services DNS et Active Directory sur Windows Server MN01

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 1 : Mise en place du serveur Windows Server 2019**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 05/02/2026
- **Dernière modification** : 25/03/2026
- **Auteur** : MEDO Louis

---
## Sommaire

1. Installation conjointe des rôles Active Directory et DNS
2. Configuration post-installation DNS (Sécurisation)

---
## 1. Installation conjointe des rôles Active Directory et DNS

!!! info
    Dans les règles de l'art, le rôle DNS ne s'installe pas isolément au préalable. Il est déployé et configuré automatiquement lors de la promotion du serveur en contrôleur de domaine. Cela permet d'obtenir une "Zone DNS intégrée à Active Directory", offrant une meilleure sécurité et une réplication optimisée de l'annuaire.

1. **Renommer le serveur.** Avant le déploiement des rôles, le serveur doit posséder un nom d'hôte conforme à la nomenclature du système d'information.
  
      **Commande PowerShell :**

      ```powershell
         Rename-Computer -NewName "MN01" -Restart
      ```

      `Rename-Computer` : Modifie l'identité NetBIOS et DNS de la machine.

      `-NewName` : Attribue la nouvelle valeur d'hôte.

      `-Restart` : Force un redémarrage immédiat de la machine, étape obligatoire pour valider le nom.

2. **Installation des binaires AD DS.** L'ajout s'effectue via le _Gestionnaire de serveur_ (_Gérer_ > _Ajouter des rôles et fonctionnalités_), en sélectionnant uniquement `Services AD DS`.

      **Alternative en commande PowerShell :**

      ```PowerShell
         Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
      ```

      `Install-WindowsFeature` : Télécharge et installe le rôle ciblé sur le serveur.

      `-Name AD-Domain-Services` : Spécifie les services d'annuaire Active Directory.

      `-IncludeManagementTools` : Installe simultanément les consoles de gestion (Outils RSAT) nécessaires pour administrer l'AD.

3. **Promotion en contrôleur de domaine et configuration DNS.** Une fois les binaires installés, cliquer sur l'icône de notification (drapeau jaune) dans le _Gestionnaire de serveur_ pour `Promouvoir ce serveur en contrôleur de domaine`.
    
    1. Sélectionner `Ajouter une nouvelle forêt` et définir le domaine racine (ex: `millenuits.local`).
    2. À l'étape des options du contrôleur de domaine, **laisser la case "Serveur DNS" cochée**. L'assistant se chargera de l'installer et de le lier à l'AD de façon transparente.
    3. Saisir un mot de passe de restauration des services d'annuaire (DSRM) généré via Bitwarden.
    4. Suivre les étapes par défaut de l'assistant jusqu'au bouton `Installer`. Le serveur redémarrera automatiquement.

!!! info
    Lors de la promotion du serveur via l'assistant, vous rencontrerez très probablement un avertissement indiquant : _"Une délégation pour ce serveur DNS ne peut pas être créée car la zone parente de fait pas autorité..."_. **C'est un comportement normal** lors de la création d'un domaine racine. Vous pouvez ignorer cet avertissement en toute sécurité et poursuivre l'installation.

---
## 2. Configuration post-installation DNS (Sécurisation)

!!! info
   Ici nous allons désactiver la récursivité du DNS du serveur Windows afin d'éviter une exposition aux attaques informatiques sur les résolveurs (comme l'amplification DNS ou l'empoisonnement de cache).

1. **Désactiver la récursivité.** Cette action empêche le serveur DNS de transférer les requêtes qu'il ne connaît pas vers d'autres serveurs publics.

      **Commande PowerShell :**

      ```PowerShell
         Set-DnsServerRecursion -Enable $false
      ```

      `Set-DnsServerRecursion` : Modifie les paramètres de récursivité du serveur DNS local.

      `-Enable` : Cible l'état d'activation de la fonctionnalité.

      `$false` : Valeur booléenne qui désactive la récursivité.

2. **Vérifier l'état de la configuration.** S'assurer que le paramètre a bien été pris en compte par le système.

      **Commande PowerShell :**

      ```PowerShell
         Get-DnsServerRecursion
      ```

      `Get-DnsServerRecursion` : Interroge le serveur et retourne l'état actuel des paramètres de récursivité (la propriété `IsRecursionEnabled` doit afficher `False`).

3. **Tester l'inefficacité de la récursivité.** Tenter de résoudre un nom de domaine externe pour confirmer que le serveur refuse la requête.

      **Commande PowerShell :**

      ```PowerShell
      Resolve-DnsName -Name www.google.com -Server 127.0.0.1
      ```

      `Resolve-DnsName` : Effectue une requête de résolution DNS depuis le client.

      `-Name` : Définit le nom de domaine externe à interroger.

      `-Server` : Force la requête à interroger notre serveur DNS local via l'adresse de bouclage (`127.0.0.1`).

      _Résultat attendu :_ La commande doit retourner une erreur (comme `QueryRefused`), prouvant que le serveur ne résout plus les noms en dehors de sa propre zone d'autorité.
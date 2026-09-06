# SP 3 - Mission 3 - Configuration du NAS

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 3 : Mise en place d'un serveur NAS MN07

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 26/03/2026
- **Dernière modification** : 26/03/2026
- **Auteur** : BISERAY Louis

___

## Configuration du Stockage et Service d'Annuaire

### 1. Liaison Active Directory (AD)

Pour permettre la synchronisation des utilisateurs et des groupes, le NAS doit être membre du domaine.

- **Serveur AD :** `172.16.51.1`
    
- **Flux réseau :** Assurez-vous que les ports DNS (53), Kerberos (88) et LDAP (389) sont ouverts entre le NAS et le contrôleur de domaine.
    

**Procédure de jonction :**

1. Aller dans **Directory Services** > **Active Directory**.
    
2. Saisir le nom du domaine (ex: `mondomaine.local`).
    
3. Renseigner les identifiants d'un administrateur du domaine.
    
4. Cocher **Enable** et sauvegarder.
    

> [!TIP]
> 
> Une fois la connexion établie, les utilisateurs de l'AD apparaissent automatiquement dans TrueNAS, évitant ainsi la création manuelle pour chaque employé.

---

### 2. Gestion des Utilisateurs et Habilitations

La gestion des accès repose sur le principe du **RBAC** (Role-Based Access Control). Les droits sont définis selon l'appartenance à des groupes spécifiques de l'AD.

#### A. Utilisateurs Locaux (Hors AD)

Pour les comptes de maintenance ou les utilisateurs n'appartenant pas au domaine, la création se fait manuellement :

- **Chemin :** `Accounts` > `Users` > `Add`

|**Nom Complet**|**Identifiant (Username)**|**Usage Type**|
|---|---|---|
|Hugo Gangneux|**Bob**|Administrateur Local|
|Crys Boisseau|**Jean**|Utilisateur Standard|

#### B. Gestion des Permissions (ACL)

Pour restreindre l'accès aux dossiers (Datasets) en fonction des habilitations :

1. Aller dans **Storage** > **Pools**.
    
2. Sur le dossier concerné, cliquer sur les trois points (⋮) > **Edit Permissions**.
    
3. Utiliser les **ACL Manager** pour ajouter des entrées :
    
    - **Groupe "RH" :** Lecture/Écriture sur le dossier `Recrutement`.
        
    - **Groupe "Compta" :** Accès interdit (Deny) sur le dossier `Technique`.
        

---

### 3. Partage des Données (SMB)

Pour que les utilisateurs puissent accéder au NAS depuis leur poste Windows :

1. Aller dans **Sharing** > **Windows Shares (SMB)**.
    
2. Créer un partage pointant vers le Dataset configuré.
    
3. Les utilisateurs pourront s'y connecter via le chemin : `\\172.16.51.1\NomDuPartage`.
    

---

### 4. Bonnes Pratiques de Sécurité

- **Complexité des mots de passe :** Éviter les suites simples comme `123456`. Privilégier 12 caractères minimum.
    
- **Accès Root :** Ne jamais utiliser le compte `root` pour les partages réseau quotidiens.
    
- **Snapshots :** Configurer des instantanés réguliers (Storage > Periodic Snapshot Tasks) pour protéger les données contre les ransomwares ou les suppressions accidentelles.
**SP 2 : Gestion du Parc Informatique**

**Mission 2 : Installation du PC maître**

**Contexte : MILLENUITS**
![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

___
## Informations générales

- __Auteur__ : Biseray Louis
- __Date de création__ : 05/02/2026

___

# Guide de Création d'un Poste Maître (Master) - Windows 11

Ce document détaille la procédure de mise en place d'un **Poste Maître**. Ce poste sert de modèle de référence : une fois configuré, son image disque sera capturée puis déployée à l'identique sur l'ensemble du parc informatique client.

## 1. Préparation de l'Environnement

Avant de débuter, assurez-vous de disposer des ressources nécessaires pour l'isolation du système maître.

### Prérequis Matériels et Logiciels

- **Hyperviseur :** VirtualBox (recommandé) ou tout autre logiciel de virtualisation.

- **Image ISO :** Windows 11 (version officielle).

- **Stockage :** 30 Go d'espace libre minimum.

- **Mémoire vive (RAM) :** 4 Go minimum alloués à la VM.


> [!IMPORTANT] **Sécurité et Intégrité :** Téléchargez l'ISO exclusivement sur le site de [Microsoft](https://www.microsoft.com). Utilisez le code de hachage (SHA-256) fourni sur le site pour vérifier que le fichier n'a pas été corrompu ou altéré durant le téléchargement.

---

## 2. Configuration de la Machine Virtuelle (VirtualBox)

L'utilisation d'une machine virtuelle permet de travailler dans un environnement sain avant la capture de l'image.

### Création de la VM

1. **Initialisation :** Créez une nouvelle machine, nommez-la (ex: `Master_Win11`).

2. **Type d'OS :** Sélectionnez `Microsoft Windows`, version `Windows 11 (64-bit)`.

3. **Ressources :** Allouez la RAM (4 Go+) et créez un disque dur virtuel (30 Go+).


### Montage de l'ISO

Pour que la machine puisse démarrer sur l'installateur Windows :

1. Allez dans les **Configuration** de la VM > onglet **Stockage**.

2. Dans l'arborescence, sélectionnez l'icône du disque vide (lecteur optique).

3. Cliquez sur l'icône du disque à droite et choisissez votre fichier `Win11_25H2_French_x64.iso`.

4. Validez et lancez la machine.


---

## 3. Installation du Système d'Exploitation

Cette phase installe la base du système qui sera commune à tous les futurs postes.

### Phases initiales

- Définissez la langue et la disposition du clavier.

- Lors de l'installation, choisissez **"Personnalisé : installer uniquement Windows"** pour formater le disque proprement.

- Sélectionnez **"Je n'ai pas de clé de produit"** (l'activation se fera post-déploiement).

- Choisissez l'édition **Windows 11 Professionnel**.


### Création du compte temporaire (`ThrowAway`)

L'objectif est de créer un premier compte pour passer les écrans de configuration initiale (OOBE).

1. Choisissez une configuration pour un **usage professionnel** (ou entreprise).

2. Dans les options de connexion, ne connectez pas de compte Microsoft. Choisissez **"Se joindre au domaine à la place"** pour forcer la création d'un **compte local**.

3. Nommez ce compte `ThrowAway`.


---

## 4. Gestion des Comptes Utilisateurs

Une fois sur le bureau, nous allons créer le compte d'administration définitif et supprimer les traces du compte temporaire.

### Création du compte Administrateur final

Nous utilisons l'outil de gestion des comptes avancés pour plus de précision.

1. Faites `Windows + R`, tapez **`netplwiz`** et validez.

2. Cliquez sur **Ajouter**, puis choisissez **"Se connecter sans compte Microsoft"** (Compte local).

3. **Identifiants :**

	- Nom d'utilisateur : `Admin`

    - Mot de passe : `Mille_2026`

    - Indice : `Mille`

4. **Élévation des privilèges :** Une fois créé, double-cliquez sur `Admin` dans la liste, allez dans l'onglet **Appartenance au groupe** et sélectionnez **Administrateur**.


### Nettoyage du poste

1. Déconnectez la session `ThrowAway`.

2. Connectez-vous avec le nouveau compte `Admin`.

3. Retournez dans la gestion des utilisateurs (ou via les Paramètres) et **supprimez le compte `ThrowAway`** ainsi que ses fichiers.

___
## 5. Installation des applications

Afin que le poste maître soit opérationnel dès son déploiement, nous installons un socle logiciel standard directement depuis les sites officiels des concepteurs.

### Navigateur Web Firefox (Dernière version)

- Aller sur le site officiel de **Firefox**.

- Télécharger et lancer l'installeur (autoriser l'exécution).

- Ajouter Firefox à la barre des tâches (**Taskbar**).

- Définir Firefox comme **navigateur par défaut**.

- Transférer les données depuis Edge si nécessaire et cliquer sur **Commencer la navigation**.


### LibreOffice

- Aller sur le site de **LibreOffice**.

- Télécharger l'installeur pour **Windows x64**.

- Sélectionner le mode d'installation **normale**.

- Cocher l'option pour **créer un raccourci sur le bureau**.

- Autoriser l'installation jusqu'à la fin.


### Lecteur PDF (Adobe Acrobat Reader)

- Aller sur le site de **Adobe**.

- Télécharger l'installeur d'Acrobat Reader.

- Lancer et autoriser l'installeur.

- Une fois l'installation terminée, définir le logiciel comme **lecteur PDF par défaut** du système.


### VLC Media Player

- Aller sur le site **VideoLAN**.

- Télécharger le fichier d'installation de VLC.

- Installer le logiciel sur le disque local **`C:\`**.

- Cocher les options de configuration par défaut et valider.

___
### 6. Préparation du système avec Sysprep

L'objectif de cette étape est de supprimer les informations spécifiques au matériel (identifiants de sécurité SID) pour que l'image puisse être déployée sur n'importe quel autre ordinateur sans conflit.

**Étapes :**

1. Désactivation de BitLocker :

	- Aller dans paramètres

	 - Confidentialité et sécurité

	- Chiffrement de l'appareil

	- Désactiver le chiffrement

	- Attendre jusqu'à la fin du déchiffrement

2. **Ouverture de l'outil :**

    - Faites `Windows + R`.

    - Tapez `C:\Windows\System32\Sysprep\sysprep.exe` et validez.

3. **Configuration de l'action :**

    - Dans **Action de nettoyage du système**, choisissez : `Passer au mode Audit sytéme`. Cela forcera les futurs PC à redémarrer sur l'écran de bienvenue (choix de langue, région).

    - **IMPORTANT :** Cochez la case **Généraliser**. C'est ce qui permet de réinitialiser les identifiants uniques (SID).

4. **Option d'arrêt :**

    - Sélectionnez **Arrêter le système** (Shutdown).

    - Cliquez sur **OK**.


### 7. Capture de l'image (Capture Windows)

Une fois la machine éteinte après le Sysprep, **ne pas la rallumez normalement**. il faut la redémarrer sur un outil de capture :

 **(VirtualBox) :** Exporter votre machine virtuelle au format **OVA** (Fichier > Exporter l'appareil virtuel). Cela crée un fichier unique que vous pouvez réimporter sur d'autres postes équipés de VirtualBox.
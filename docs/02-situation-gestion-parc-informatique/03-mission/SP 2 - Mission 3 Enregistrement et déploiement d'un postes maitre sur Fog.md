**SP 2 : Gestion du Parc Informatique**

**Mission 3 : Outil de déploiement des postes**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

___
## Informations générales

- __Auteur__ : Biseray Louis
- __Date de création__ : 19/03/2026
- **Sujet** : Installation de FOG

___

# Introduction

Maintenant que le server Fog est fonctionnel et en place il faut enregistre le poste Maitre que Fog va "Aspirer" et ensuite le déployer, pour cette Mission le pc maitre est sur VirtualBox il y a donc plusieurs configuration à faire.

Il y a donc 3 étapes :

- **Paramétrage de VirtualBox pour "Aspirer" le poste maitre**
- **Aspiration et sauvegarde du poste maitre**
- **Déploiement sur un poste vierge**

___

## Paramétrage de VirtualBox

### 1. Le Réseau : Passer en "Pont" (Bridged)

Par défaut, VirtualBox met les machines en mode **NAT**. Dans ce mode, le serveur FOG ne pourra jamais contacter le Windows 10.

- Aller dans les **Paramètres** de la machine virtuelle Windows 10.

- Section **Réseau**.

- Mode d'accès : Choisir **Accès par pont**.

- Sélectionner la carte réseau physique (Ethernet ou Wi-Fi) celle qui est sur le même réseau que le serveur FOG.


### 2. Le Type de carte réseau 

FOG utilise un noyau Linux (FOS) pour capturer les images. Certaines cartes virtuelles de VirtualBox sont mal reconnues.

- Dans l'onglet **Réseau** -> **Avancé**.

- Type de carte : Choisir **Intel PRO/1000 MT Desktop**.

### 3. Activer le Boot Réseau (PXE)

Pour que FOG prenne la main au démarrage, la VM doit chercher le serveur sur le réseau avant de lancer le disque dur.

- Dans **Système** -> onglet **Carte mère**.

- Dans **Ordre d'amorçage**, cocher **Réseau** et le placer tout en haut de la liste avec les flèches.

___

## Aspiration et sauvegarde du poste maitre

### 1. Préparation du Master 


1. **Sysprep :** C'est obligatoire pour réinitialiser les identifiants de sécurité (SID).

	- Appuyer sur ``Win + R``

    - Taper `C:\Windows\System32\Sysprep\sysprep.exe`

    - Choisis **OOBE**, cocher **Généraliser** et sélectionner **Arrêter le système**.

    - Note : Une fois le PC éteint, **ne pas rallumer** sous Windows, sinon le Sysprep est annulé.


### 2. Déclarer l'Image dans FOG

Avant de capturer, il faut créer le "contenant" sur le serveur FOG.

1. Sur l'interface Web -> **Image** -> **Créée une nouvelle Image**.

2. Nommer le (ex: `Win10_Master`).

3. **Image Type :** Sélectionne **Single Disk - Resizable.**

4. **Partition :** "Everything" ou "All Partitions".

5. **Operating System :** Windows 10.

6. Clique sur **Ajouter**.


### 3. Associer l'Image à  l'Hôte

Maintenant, on dit à FOG que _ce_ PC précis possède _cette_ image.

1. Va dans **Machine** -> Liste des hôtes.

2. Cliquer sur le PC Maitre.

3. Dans le champ **Host Image**, sélectionne l'image créée `Win10_Master`.

4. Cliquer sur **Update**.

### 4. Lancer la Capture (Le "Push")

1. Toujours sur la fiche de ton hôte, clique sur le bouton **Capture** (l'icône avec une flèche qui monte).

2. FOG créer une **Task**.

3. **Rallumer le PC Master** et s'assurer qu'il boot en PXE (réseau).

>[!note] En cas d'erreur "Kernel Panic" vérifier l'horloge de FOG dans Configuration > Générale > Fuseau horaire

4. Le PC ne va pas lancer Windows, il va charger l'environnement FOS. il y aura une barre de progression bleue : FOG est en train "d'aspirer" le Windows 10 vers le serveur.

___ 



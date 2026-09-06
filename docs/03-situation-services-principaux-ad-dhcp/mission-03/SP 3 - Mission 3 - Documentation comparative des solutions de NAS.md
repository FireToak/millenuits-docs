# SP 3 - Mission 3 - Choix de la solution NAS

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 3 : Documentation comparative des solutions de NAS**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 19/03/2026
- **Dernière modification** : 19/03/2026
- **Auteur** : BISERAY Louis

___

## Les Différente solutions de NAS 

### 1. Unraid 


- **Le concept :** Contrairement au RAID classique, possibilité de mélanger des disques de tailles et de marques différentes. Le seul impératif : le disque de parité doit être le plus gros du lot.

- **Avantages :** Pouvoir ajouter un disque à n'importe quel moment pour agrandir ton stockage. Si on perds plus de disques que ta parité ne peut en gérer, on ne perds que les données sur les disques morts (les autres restent lisibles individuellement).

- **Inconvénients :** Les vitesses d'écriture sont plus lentes qu'en RAID (bridées à la vitesse d'un seul disque). C'est un logiciel payant (licence annuelle ou perpétuelle).

### 2. TrueNAS (Scale/Core) : (Open Source / Gratuit)


- **Le concept :** ZFS protège les données contre la "bit rot" (la corruption silencieuse des fichiers) grâce à des sommes de contrôle (checksums).

- **Avantages :** Performances incroyables, snapshots instantanés, et une sécurité des données. La version **Scale** est basée sur Linux (Debian) et gère très bien les conteneurs Docker/Apps.

- **Inconvénients :** Très gourmand en RAM (compter 1 Go de RAM pour 1 To de stockage). **Rigide :** ne peux pas facilement ajouter un seul disque à un pool existant ; il faut souvent ajouter des groupes de disques entiers.


### 3. OpenMediaVault (OMV) : (Gratuit)

- **Le concept :** Est une surcouche graphique ultra-propre posée sur une Debian stable.

- **Avantages :** Consomme quasiment rien en CPU/RAM. Pur Linux, donc si l'interface Web plante, tout peut être gérer en ligne de commande. Très modulaire grâce à ses plugins.

- **Inconvénients :** Moins "clé en main" que les autres. Il faut souvent mettre les mains a la pate pour configurer Docker ou des systèmes de fichiers avancés.


### 4. TerraMaster (TOS) : Le compromis matériel (Hardware inclus)


- **Le concept :** C'est le "Synology-like" pour ceux qui veulent du hardware puissant à prix cassé.

- **Avantages :** Interface web moderne et simple. Très facile à mettre en place pour un débutant. Supporte le RAID classique (0, 1, 5, 10) et TRAID (leur version flexible proche de Synology).

- **Inconvénients :** L'écosystème d'applications est beaucoup moins riche que chez Synology ou TrueNAS. La sécurité logicielle a eu quelques ratés par le passé (mises à jour moins fréquentes).

___

## Choix pour répondre aux exigences :


Pour moi le meilleur choix pour le Nas est TrueNas il correspond au cahier des charges, de plus il est gratuit, Open Source et il est possible avec de rajouter le NAS dans le domaine de l'AD ce qui va permettre l'autorisation de plusieurs personnes avec des droits différents dans le NAS.
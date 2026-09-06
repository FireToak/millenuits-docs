# SP 3 - Mission 3 - Installation de TrueNas

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 3 : Mise en place d'un serveur NAS MN07

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 19/03/2026
- **Dernière modification** : 19/03/2026
- **Auteur** : BISERAY Louis

___

## Prérequis et installation 

### A. Prérequis :

Le choix du Nas est donc tourner vers True NAS. Nous disposons dans l'hyperviseur Nutanix de un ISO de TrueNas Scale.

Les paramètres mis dans la VM sont les suivants :

- Réseau :
	- Vlan 51 
- Deux disques :
	-  Un disque : 20 Go pour l'installation
	- Un disque : 40 Go pour le stockage
- Mot de passe : 
	- `0247249690`

### B. Installations :

Lancer la VM nous envoie dans la page d'installation de TrueNas, Il y a 4 Options disponible :

```
1  Install/Upgrade
2  Shell
3  Reboot System
4  Shutdown System
```

L'options qui nous intéresse ici est le `Install Upgrade` .

Il sera demander de choisir le support sur le quel sera installer l'installer de TrueNas dans notre cas nous allons l'installer sur le disque à 20 Go

Il nous est demander de créé un mot de passe qu'il faudra retenir dans notre cas le mot de passe est `0247249690` .

Et enfin si nous voulons booter soit sur sur le BIOS et sur le UEFI

Une fois l'installation effectuer :

- Retourner sur Nutanix éteignez la VM
- Appuyer sur le bouton ``UPDATE``
- Changer l'ISO pour un ``empty CD-ROM``
- Et relancez la VM

___

## Réseau 

Maintenant que le Nas est "Installer" il faut définir sont interface réseau.

1. Appuyer sur ``1`` et sur ``entrer`` pour valider.

2. Choisissez votre interface.

3. Suivez ces étapes : 

```
Remove the current settings of this interface ? (This causes a momentary dsiconnection of the network.) (y/n)  N

Configure interface for DHCP (y/n)  N

Configure IPv4 (y/n)  Y

Interface name : vtnet

IPV4 Address : 172.16.51.9/24

```

4. Retourner sur le menu et appuyer sur ``4`` et ``entrer``

```
Configure IPv4 Default Route ? (y/n) Y

IPv4 Default Route : 172.16.51.252

Configure IPv6 Default Route ? (y/n) N
```

5. Rebooter TrueNas pour que l'interface s'applique correctement

Maintenant vous devriez pouvoir accéder à l'interface de TrueNas avec l'adresse IP : `172.16.51.29` le mot de passe pour y accéder et celui que nous avons définis plutôt.

___


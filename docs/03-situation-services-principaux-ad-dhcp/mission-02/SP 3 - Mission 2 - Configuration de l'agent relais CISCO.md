# SP 3 - Mission 2 - Configuration de l'agent relais CISCO

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 2 : Mise en place du serveur DHCP sous Linux**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 05/02/2026
- **Dernière modification** : 19/03/2026
- **Auteur** : MEDO Louis

---
## Sommaire

- A. Configuration de l'agent relais (IP Helper)

---
## A. Configuration de l'agent relais (IP Helper)

> **Bonne pratique :** La commande de l'agent relais ne doit être configurée **que** sur les sous-interfaces desservant des réseaux ayant un besoin explicite d'attribution d'adresses dynamiques (DHCP). Les sous-réseaux ne nécessitant aucun service DHCP ne doivent pas posséder cet élément.

1. **Sélection et paramétrage de la sous-interface.** Configuration du transfert des requêtes DHCP vers le serveur DHCP (MN11).

```Bash
interface GigabitEthernet0/0.10
ip helper-address 172.16.51.11
exit
```

- `interface GigabitEthernet0/0.10` : Accède au mode de configuration de la sous-interface spécifique (remplacer `0/0.10` par l'identifiant réel de votre sous-interface).
- `ip helper-address 172.16.51.11` : Intercepte les requêtes de diffusion (broadcast) DHCP des postes clients et les relaie en monodiffusion (unicast) vers l'adresse IP du serveur DHCP désigné (172.16.51.11).
- `exit` : Quitte le mode de configuration de la sous-interface pour revenir au mode de configuration globale.
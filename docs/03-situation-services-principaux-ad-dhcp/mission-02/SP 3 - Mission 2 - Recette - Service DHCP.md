# SP 3 - Mission 2 - Recette - Service DHCP

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 2 : Mise en place du serveur DHCP sous Linux**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 05/02/2026
- **Dernière modification** : 19/03/2026
- **Mainteneur** : MEDO Louis

---
## Sommaire

- A. Vérification de l'état du service KEA
- B. Validation de l'attribution IP et des options
- C. Validation du fonctionnement de l'agent relais
- D. Vérification de l'enregistrement des baux

---
## A. Vérification de l'état du service KEA

#### Démarrage et stabilité du daemon

**Description du test :**
Sur le serveur Linux, exécuter la commande de vérification de statut du service (`systemctl status kea-dhcp4-server`) et analyser les derniers journaux système (`journalctl -u kea-dhcp4-server`).

**Résultat :**
Le service indique un état "active (running)". Aucun message d'erreur ou d'échec de liaison sur l'interface d'écoute n'est présent dans les logs.

**Commentaire :**

--

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé

---
## B. Validation du fonctionnement de l'agent relais

#### Obtention d'une configuration IP depuis un autre VLAN/Sous-réseau

**Description du test :**
Connecter un poste client sur un sous-réseau distant configuré avec l'agent relais (IP Helper pointant vers 172.16.51.11). Lancer une requête DHCP depuis ce client.

**Résultat :**
Le routeur relaie correctement la trame broadcast en unicast. Le client obtient une adresse IP correspondant au *pool* de son propre sous-réseau, confirmant que KEA identifie correctement l'origine de la requête via l'adresse de l'agent relais (giaddr).

**Commentaire :**

--

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé

---
## C. Vérification de l'enregistrement des baux

#### Traçabilité côté serveur

**Description du test :**
Vérification de l'attribution d'une adresse IP à un client, consulter la base de données ou le fichier d'enregistrement des baux du serveur KEA (généralement `/var/lib/kea/kea-leases4.csv`).

**Résultat :**
Une nouvelle entrée est présente. Elle associe correctement l'adresse MAC du client de test à l'adresse IP distribuée, et indique une date d'expiration cohérente avec le paramètre `valid-lifetime` configuré.

**Commentaire :**

--

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé
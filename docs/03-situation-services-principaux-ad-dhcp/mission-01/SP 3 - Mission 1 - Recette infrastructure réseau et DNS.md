# SP 3 - Mission 1 - Recette infrastructure réseau et DNS

**SP 3 : Gestion des services principaux AD (Active Directory) et DHCP**

**Mission 1 : Mise en place du serveur Windows Server 2019**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 12/03/2026
- **Dernière modification** : 12/03/2026
- **Auteur** : MEDO Louis

---
## Sommaire

- A. Vérification physique
- B. Accès passerelle
- C. Accès service internet
- D. Vérification de la translation sur le routeur
- E. Vérification résolution DNS

---
## A. Physique

**Description du test** : 

> Vérification des liens physiques.

**Résultats Attendus** : 

> LED de connexion allumées.

Réception : 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
| 
|
|

---
## B. Accès passerelle

**Description du test :** 

> Ping sur la passerelle du sous-réseau.

- Commande : `ping <passerelle_sous_reseau>`
- Exemple : `ping 172.40.1.126`

Résultats Attendus : 

> Réponse positive à la commande.

Réception : 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
|
|
|

---
## C. Accès service internet

**Description du test :** 

> Ping et chargement d'une page internet.

1. **Couche Réseau (L3) :**

- Commande : `ping <adresse_ip_exterieure>`
- Exemple : `ping 9.9.9.9`
         ⚠️ En cas de problème lors du ping, utilisez `traceroute` pour voir le chemin emprunté par le paquet et déterminer l'élément défectueux.

2. **Couche Applicative (L7) :**

- Commande : `curl <nom_domaine>`
- Exemple : `curl infomaniak.com`

**Résultats Attendus** : Réponse positive à la commande ping et affichage de la page HTML pour la commande curl.

Réception : 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
|
|
|

---

## D. Vérification de la translation sur le routeur

**Description du test :** 

> Translation des adresses IP privées vers l'adresse IP publique du routeur.

- Commande : `show ip nat translations`

**Résultats Attendus :**

> Liste contenant l'historique des translations du routeur.

_Exemple de retour de la commande :_
```
Pro Inside global      Inside local      Outside local      Outside global  
icmp 172.16.10.10:10   192.168.1.100:10  10.20.30.40:10     10.20.30.40:10
---  172.16.10.10      192.168.1.100     ---                ---          
```

**Réception :** 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
|
|
|

---
## E. Vérification résolution DNS

**Description du test :** 

> Résolution d'une adresse IP à partir d'un nom de domaine sur le serveur DNS de Millenuits.

- Commande : `nslookup glpi.mn51.lan`

**Résultats Attendus :**

> Liste contenant l'historique des translations du routeur.

_Exemple de retour de la commande :_
```
Server: [172.16.51.1]
Address: 172.16.51.1

Non-authoritative answer:
Name: glpi.mn51.lan
Address: 172.16.51.6    
```

**Réception :** 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
|
|
|
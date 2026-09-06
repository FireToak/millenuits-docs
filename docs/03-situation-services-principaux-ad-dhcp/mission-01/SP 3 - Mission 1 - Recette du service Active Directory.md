# SP 3 - Mission 1 - Recette du service Active Directory

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

- A. Test de résolution DNS interne
- B. Test de santé du contrôleur de domaine
- C. Test d'intégration d'un poste au domaine
- D. Test d'authentification utilisateur

---
## A. Test de résolution DNS interne

**Description du test** : 

> Vérifier que le serveur DNS répond correctement aux requêtes internes.
> Sur le serveur ou un poste client, ouvrir l'invite de commande (cmd) et taper :
> `nslookup millenuits.lan`.
> 
> *Explication de la commande : `nslookup` (Name Server Lookup) est un outil qui interroge le serveur DNS pour obtenir l'adresse IP associée à un nom de domaine (ou inversement), validant ainsi le bon fonctionnement du service DNS.*

**Résultats Attendus** : 

> La commande doit retourner l'adresse IP correcte du contrôleur de domaine MILLENUITS sans erreur de "TimeOut" ou "Serveur inconnu".

Réception : 

- [x] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
|
|
|

---
## B. Test de santé du contrôleur de domaine

**Description du test** : 

> Vérifier l'intégrité des services Active Directory.
> Sur le serveur, ouvrir l'invite de commande (cmd) en tant qu'administrateur et taper :
> `dcdiag`
>
> *Explication de la commande : `dcdiag` (Domain Controller Diagnostic) lance une série de tests automatisés (connectivité, réplication, services critiques, topologie) pour s'assurer que le contrôleur de domaine fonctionne correctement et identifier les erreurs.*

**Résultats Attendus** : 

> Tous les tests doivent afficher le statut "A réussi le test" (Passed). Aucune erreur critique ne doit apparaître dans le rapport.

Réception : 

- [x] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
| 
|
|

---
## C. Test d'intégration d'un poste au domaine

**Description du test** : 

> Intégrer physiquement ou virtuellement un poste client (Windows 10/11) au domaine MILLENUITS. 
> Saisir les identifiants d'un compte Administrateur du domaine lors de l'invite d'intégration.

**Résultats Attendus** : 

> Un message "Bienvenue dans le domaine MILLENUITS" s'affiche. L'ordinateur redémarre et l'objet "Ordinateur" apparaît bien dans la console *Utilisateurs et ordinateurs Active Directory* sur le serveur.

Réception : 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé :

Commentaire :
| 
|
|

---
## D. Test d'authentification utilisateur

**Description du test** : 

> Sur le poste client fraîchement intégré au domaine, tenter d'ouvrir une session avec un compte utilisateur standard créé précédemment (ex: p.nom) et son mot de passe provisoire.

**Résultats Attendus** : 

> La session s'ouvre. Le système demande immédiatement de modifier le mot de passe (si l'option a bien été cochée à la création). Une fois modifié, le bureau Windows se charge correctement.

Réception : 

- [ ] Reçu
- [ ] Reçu avec réserve
- [ ] Refusé
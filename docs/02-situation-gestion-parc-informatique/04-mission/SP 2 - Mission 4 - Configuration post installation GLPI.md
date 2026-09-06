# SP 2 - Mission 4 - Configuration post installation GLPI

**SP 2 : Gestion parc informatique**

**Mission 4 : Installation de GLPI**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- Date de création : 12/02/2025
- Dernière modification : 12/02/2025
- Mainteneur : Louis MEDO

---
## Sommaire

- A. Sécurité et nettoyage post-installation
- B. Configuration de la structure de l'entreprise
- C. Création des groupes et utilisateurs locaux
- D. Configuration des éléments de tickets

---
## A. Sécurité et nettoyage post-installation

1. **Suppression du dossier d'installation.** Il est vital de supprimer ce répertoire pour empêcher quiconque de relancer l'installation et d'écraser la configuration sur le serveur MN06.

```Bash
rm -r /var/www/glpi/install
```

*Explication de la commande :* `rm` (remove) sert à supprimer. L'option `-r` (récursif) permet de vider tout le contenu du dossier et de ses sous-dossiers.

2. **Modification des mots de passe par défaut.** GLPI installe des comptes standards (glpi, tech, normal, post-only) dont le mot de passe est identique à l'identifiant. Connectez-vous avec le compte `glpi` et modifiez-les tous dans le menu *Administration > Utilisateurs* pour sécuriser l'accès à l'outil.

3. **Sécurisation du compte Super-Admin.** Pour éviter les attaques par force brute sur l'identifiant par défaut, renommez le compte `glpi` en `coussin-chaise-longue` et appliquez un mot de passe fort issu du Bitwarden de l'entreprise.
   
   - Allez dans *Administration > Utilisateurs*, cliquez sur l'utilisateur `glpi`. Modifiez le champ "Identifiant", insérez le nouveau mot de passe, puis cliquez sur "Sauvegarder".


4. **Création des comptes administrateurs nominatifs.** Pour garantir la traçabilité des actions (principe de non-répudiation), chaque membre de l'équipe informatique doit posséder son propre accès administrateur.
   
   - Allez dans *Administration > Utilisateurs*, cliquez sur le bouton "Ajouter". Renseignez les informations (Identifiant, Nom, Prénom, Mot de passe) et ajoutez-le. Ensuite, sélectionnez ce nouvel utilisateur, allez dans l'onglet *Habilitations*, et ajoutez-lui le profil "Super-Admin" (ou "Admin") sur l'entité racine "Mille Nuits".

---
## B. Configuration de la structure de l'entreprise

1. **Création des entités.** L'entité permet de définir et cloisonner l'organisation. Allez dans *Administration > Entités* et renommez l'entité par défaut (Root entity) en "MilleNuits".

2. **Ajout des lieux.** Dans *Configuration > Intitulés > Général > Lieux*, créez l'arborescence géographique afin de localiser facilement les problèmes remontés. Ajoutez le "Site Baugé" et le "Site logistique Joué-Lès-Tours".

![](https://raw.githubusercontent.com/AP-BTS-SIO-Louis/millenuits/main/docs_millenuits/docs/02-situation-gestion-parc-informatique/04-mission/assets/capture-ecran_creation-lieu.png)

---
## C. Création des groupes et utilisateurs locaux

1. **Configuration des profils.** Dans *Administration > Profils*, vérifiez les droits : *Self-Service* pour les salariés qui déclarent les pannes , *Technician* pour les informaticiens qui attribuent et résolvent les incidents , et *Super-Admin* pour que le DSI puisse obtenir ses statistiques de temps de résolution.

2. **Création manuelle des utilisateurs.** Puisque le serveur AD n'est pas lié, allez dans *Administration > Utilisateurs* pour créer manuellement les comptes des techniciens et des premiers utilisateurs.

---
## D. Configuration des éléments de tickets

1. **Catégories de tickets.** Allez dans *Configuration > Intitulés > Assistance > Catégorie ITIL*. Créez des catégories (ex : Matériel, Logiciel, Réseau, Demande d'accès) pour classer les incidents et faciliter les statistiques.

2. **Matériels de l'utilisateur.** Pour qu'un utilisateur puisse lier son ordinateur ou son imprimante au ticket, allez dans *Administration > Profils* et modifiez le profil *Self-Service*. Dans l'onglet *Assistance*, vérifiez que l'option "Associer des éléments à un ticket" est active.

3. **Observateurs.** Un observateur peut suivre l'avancée d'un ticket sans en être le demandeur ou le technicien. Pour autoriser cet ajout, allez dans *Administration > Profils* (ex: pour le profil *Technician* ou *Self-Service*), puis dans l'onglet *Assistance*, validez les droits permettant d'ajouter ou de voir des observateurs.
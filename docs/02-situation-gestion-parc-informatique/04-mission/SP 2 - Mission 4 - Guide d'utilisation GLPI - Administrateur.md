# SP 2 - Mission 4 - Guide d'utilisation GLPI - Administrateur

**SP 2 : Gestion parc informatique**

**Mission 4 : Installation de GLPI**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- Date de création : 24/02/2025
- Dernière modification : 24/02/2025
- Mainteneur : Louis MEDO

---
## Sommaire

- A. Les fonctionnalités de l'interface Administrateur
- B. Comment y accéder ?
- C. Gestion des utilisateurs et des habilitations
- D. Supervision et gestion avancée des incidents
- E. Réalisation de statistiques et rapports
- F. Configuration avancée (Règles et SLAs)

---
## A. Les fonctionnalités de l'interface Administrateur

En tant qu'administrateur (ou Super-Admin) comme le DSI, votre rôle est de piloter l'outil et de superviser l'activité globale du service :

- **Gestion des accès :** Création des utilisateurs, attribution des profils et gestion des entités (Baugé, Joué-lès-Tours).
- **Supervision :** Modification globale, réattribution et résolution forcée des tickets.
- **Pilotage :** Génération de statistiques pour mesurer la performance du support (temps de résolution, volume par catégorie).
- **Paramétrage expert :** Création d'intitulés et de niveaux de service (SLA) pour garantir la qualité du support.

---
## B. Comment y accéder ?

- **URL de GLPI :** http://172.16.51.6

--

1. **Ouverture du navigateur.** Lancez votre navigateur web et saisissez l'URL indiquée.
   
2. **Authentification.** Connectez-vous avec votre compte administrateur nominatif. Assurez-vous que le profil sélectionné en haut à droite est bien **Super-Admin** ou **Admin** sur l'entité racine "Mille Nuits".

---
## C. Gestion des utilisateurs et des habilitations

1. **Créer un nouvel utilisateur.**
	   - Allez dans le menu *Administration > Utilisateurs*.
	   - Cliquez sur l'icône d'ajout (**+**).
	   - Renseignez les informations obligatoires (Identifiant, Nom, Prénom, Mot de passe) et validez.

2. **Attribuer un profil et une entité.**
	- Depuis la fiche de l'utilisateur nouvellement créé, cliquez sur l'onglet *Habilitations*.
	- Sélectionnez l'entité (ex: Site logistique) et le profil correspondant à son rôle (Self-Service, Technician, etc.), puis cliquez sur "Ajouter". *(Notion : Une habilitation relie un utilisateur à des droits spécifiques sur une zone géographique ou logique précise).*

---
## D. Supervision et gestion avancée des incidents

1. **Modification et réattribution d'incidents.**
	- Allez dans *Assistance > Tickets*. L'administrateur a une vue sur l'intégralité des tickets de l'entreprise.
	- Vous pouvez ouvrir n'importe quel ticket pour modifier sa catégorie, son urgence, ou réattribuer le ticket à un autre technicien en cas d'absence.

2. **Actions massives.**
	- Cochez plusieurs tickets dans la liste, puis cliquez sur le bouton "Actions".
	- Cela permet d'appliquer une modification en lot (ex: assigner 10 tickets au même technicien simultanément pour gagner du temps).

3. **Résolution d'un incident.**
	- Allez dans l'onglet *Solution* d'un ticket pour le clôturer. En tant qu'administrateur, vous avez le droit d'approuver directement la solution à la place de l'utilisateur final pour forcer la fermeture du ticket.

---
## E. Réalisation de statistiques et rapports

1. **Générer des statistiques globales.**
	- Allez dans le menu *Assistance > Statistiques*.
	- Choisissez le filtre souhaité (Par ticket, Par technicien, Par catégorie, etc.).

2. **Analyser les performances.**
	- Sélectionnez "Par technicien" pour visualiser le nombre de tickets résolus par membre de l'équipe et le temps moyen d'intervention. Ces données sont cruciales pour que le DSI puisse justifier les temps d'arrêt ou demander des embauches.

---
## F. Configuration avancée (Règles et SLAs)

1. **Création d'intitulés (Catégories, Lieux).** - Allez dans *Configuration > Intitulés* pour enrichir les listes déroulantes proposées aux utilisateurs (ex: ajouter un nouveau modèle de PC ou une nouvelle catégorie de panne logicielle).

2. **Gestion des SLAs (Service Level Agreement).** - Allez dans *Configuration > SLA* pour définir des temps de résolution maximums. 
   
   *Notion : Un SLA est un engagement de service. Si vous fixez un SLA de 4h pour une urgence Haute, le système alertera automatiquement l'équipe si le ticket n'est pas résolu dans ce délai.*
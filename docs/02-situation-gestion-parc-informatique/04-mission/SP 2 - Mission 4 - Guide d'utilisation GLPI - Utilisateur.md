# SP 2 - Mission 4 - Guide d'utilisation GLPI - Utilisateur

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

- A. Qu'est-ce que GLPI ?
- B. Les fonctionnalités principales de l'interface utilisateur
- C. Comment y accéder ?
- D. Créer un ticket

---
## A. Qu'est-ce que GLPI ?

GLPI (Gestionnaire Libre de Parc Informatique) est la plateforme d'assistance informatique de l'entreprise. C'est un outil qui vous permet de signaler un problème (panne matérielle, bug logiciel) ou de faire une demande (nouveau matériel) directement au service informatique, garantissant ainsi une prise en charge rapide et tracée.

---
## B. Les fonctionnalités principales de l'interface utilisateur

En tant qu'utilisateur standard, GLPI vous offre trois fonctionnalités majeures :

- **La création de tickets :** Pour déclarer un incident (ex: la souris ne fonctionne plus) ou formuler une demande.
- **Le suivi des demandes :** Pour visualiser en temps réel l'état d'avancement de vos tickets (en cours, en attente, résolu) et interagir avec le technicien.
- **La base de connaissances :** Un accès à une Foire Aux Questions (FAQ) rédigée par le service informatique pour résoudre vous-même les problèmes les plus courants.

---
## C. Comment y accéder ?

- **URL de GLPI :** [http://172.16.51.6](http://172.16.51.6)

--

1. **Ouverture du navigateur.** Lancez votre navigateur web (comme Firefox) et saisissez l'URL indiquée ci-dessus dans la barre d'adresse.
   
2. **Authentification.** Entrez votre identifiant et votre mot de passe (fournis par le service informatique) dans les champs correspondants, puis cliquez sur "Se connecter". L'interface s'adaptera automatiquement à votre profil utilisateur (Self-Service).

---
## D. Créer un ticket

1. **Accès au formulaire de création.** Sur la page d'accueil de votre espace, cliquez sur le bouton "Créer un ticket" (ou allez dans le menu *Assistance > Créer un ticket*).
   ![](https://raw.githubusercontent.com/AP-BTS-SIO-Louis/millenuits/main/docs_millenuits/docs/02-situation-gestion-parc-informatique/04-mission/assets/capture-ecran_creation-ticket.png)
   
2. **Saisie des détails de l'incident.** 
	- **Type :** Choisissez s'il s'agit d'un "Incident" (panne) ou d'une "Demande" (besoin).
	- **Catégorie :** Sélectionnez le domaine concerné (ex: Matériel, Logiciel, Réseau) pour bien orienter le ticket vers le bon technicien.
	- **Urgence :** Indiquez l'impact du problème sur votre travail (ex: Très haute si vous ne pouvez plus travailler du tout).
	- **Observateurs :** Ajoutez les adresses mails des collègues ou de votre responsable s'ils doivent être tenus informés de la résolution.
	- **Lieu :** Spécifiez où vous vous trouvez (ex: Site historique Baugé ou Site logistique Joué-Les-Tours) pour faciliter une éventuelle intervention physique.
	- **Matériel :** Sélectionnez l'équipement défectueux dans la liste déroulante (votre ordinateur, votre imprimante) pour donner un contexte immédiat à l'informaticien.
	- **Titre :** Résumez brièvement le problème (ex: "Connexion Internet impossible").
	- **Description :** Détaillez au maximum le problème rencontré pour aider les informaticiens (message d'erreur, actions effectuées avant la panne).

3. **Validation.** Cliquez sur le bouton "Soumettre le message". Votre ticket est alors transmis à l'équipe informatique et vous pourrez suivre son statut depuis la page d'accueil.
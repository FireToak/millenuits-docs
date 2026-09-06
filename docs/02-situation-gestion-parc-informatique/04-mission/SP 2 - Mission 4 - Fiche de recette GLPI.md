# SP 2 - Mission 4 - Fiche de recette GLPI

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

- A. Tests de sécurité et d'accès
- B. Tests du profil Utilisateur (Self-Service)
- C. Tests du profil Technicien (Helpdesk)
- D. Tests du profil Administrateur

---
## A. Tests de sécurité et d'accès

1. **Vérification de la suppression du dossier d'installation.**
	- ***Action :*** Tenter d'accéder à l'URL `http://172.16.51.6/install/install.php`.
	- ***Résultat attendu :*** Page d'erreur (404 Not Found). L'installation ne peut pas être relancée.
	- ***Statut :*** [ ] OK / [ ] KO

2. **Vérification de la désactivation des comptes par défaut.**
	- ***Action :*** Tenter de se connecter avec les identifiants `tech/tech` ou `normal/normal`.
	- ***Résultat attendu :*** Connexion refusée.
	- ***Statut :*** [ ] OK / [ ] KO

---
## B. Tests du profil Utilisateur (Self-Service)

1. **Création d'un ticket.**
	- ***Action :*** Se connecter avec un compte utilisateur standard. *Aller dans Assistance > Créer un ticket*. Remplir un ticket d'incident matériel pour le site de "Joué-lès-Tours" et valider.
	- ***Résultat attendu :*** Le ticket est créé avec succès et apparaît dans l'accueil de l'utilisateur avec le statut "Nouveau".
	- ***Statut :*** [ ] OK / [ ] KO

2. **Ajout d'un suivi.**
	- ***Action :*** Ouvrir le ticket créé et ajouter un message dans l'onglet "Suivis".
	- ***Résultat attendu :*** Le message est enregistré et visible dans l'historique du ticket
	- ***Statut :*** [ ] OK / [ ] KO

---
## C. Tests du profil Technicien (Helpdesk)

1. **Prise en charge de l'incident.**
	- ***Action :*** Se connecter avec un compte Technicien. Aller dans *Assistance > Tickets*. Ouvrir le ticket "Nouveau" de l'utilisateur et s'attribuer le ticket.
	- ***Résultat attendu :*** Le statut du ticket passe de "Nouveau" à "En cours (attribué)".
	- ***Statut :*** [ ] OK / [ ] KO

2. **Résolution du ticket.**
	   - ***Action :*** Aller dans l'onglet "Solution", rédiger une solution technique et valider.
	   - ***Résultat attendu :*** Le statut du ticket passe à "Résolu". 
	   - ***Statut :*** [ ] OK / [ ] KO

---
## D. Tests du profil Administrateur

1. **Création d'un nouvel utilisateur.**
	   - ***Action :*** Se connecter avec le compte Super-Admin (`coussin-chaise-longue`). Aller dans *Administration > Utilisateurs* et créer un compte "Test_Recette". Lui donner le profil "Self-Service".
	   - ***Résultat attendu :*** Le compte est créé, l'utilisateur peut se connecter et n'a accès qu'à l'interface simplifiée.
	   - ***Statut :*** [ ] OK / [ ] KO

2. **Génération de statistiques.**
	   - ***Action :*** Aller dans *Assistance > Statistiques*. Sélectionner les statistiques globales par technicien.
	   - ***Résultat attendu :*** Un tableau/graphique s'affiche, montrant au moins 1 ticket résolu (celui du test précédent).
	   - ***Statut :*** [ ] OK / [ ] KO
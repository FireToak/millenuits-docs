# SP 2 - Mission 4 - Guide d'utilisation GLPI - Helpdesk

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

- A. Les fonctionnalités principales de l'interface technicien
- B. Comment y accéder ?
- C. Traiter et gérer un ticket
- D. Alimenter la base de connaissances

---
## A. Les fonctionnalités principales de l'interface technicien

En tant que membre du support informatique (Helpdesk), votre interface offre des outils avancés pour gérer le parc et les incidents :

- **Gestion de la file d'attente :** Visualiser tous les tickets ouverts par les collaborateurs des sites de Baugé et de Joué-lès-Tours.
- **Prise en charge et suivi :** Vous attribuer un ticket, ajouter des tâches techniques, communiquer avec le demandeur ou escalader le problème si nécessaire.
- **Résolution et documentation :** Clôturer un incident et documenter la solution dans la base de connaissances pour capitaliser sur les résolutions de l'équipe.

---
## B. Comment y accéder ?

- **URL de GLPI :** [http://172.16.51.6](http://172.16.51.6)

--

1. **Ouverture du navigateur.** Lancez votre navigateur web (ex: Firefox) et saisissez l'URL indiquée.
   
2. **Authentification.** Entrez votre identifiant nominatif et votre mot de passe administrateur/technicien. Une fois connecté, assurez-vous que votre profil actif en haut à droite de l'écran est bien positionné sur **Technician** ou **Admin**.

---
## C. Traiter et gérer un ticket

1. **S'attribuer un ticket (Prise en charge).**
	- Allez dans le menu *Assistance > Tickets*.
	- Cliquez sur un ticket dont le statut est "Nouveau".
	- Dans le panneau principal ou latéral, cherchez le champ **Technicien** (ou le bloc d'attribution), cliquez sur l'icône d'ajout et sélectionnez "Moi" pour vous l'attribuer. Le statut du ticket passera automatiquement à "En cours (attribué)".

2. **Ajouter un suivi ou une tâche.**
    - Pour communiquer avec l'utilisateur (ex: demander un complément d'information), utilisez l'onglet **Suivis** depuis le ticket et rédigez votre message.
    - Pour tracer vos actions techniques invisibles par l'utilisateur (ex: "Redémarrage du port sur le commutateur Cisco"), utilisez l'onglet **Tâches**, indiquez le temps passé et décrivez l'action menée.

3. **Résoudre l'incident.**
     - Une fois la panne identifiée et réparée, rendez-vous dans l'onglet **Solution** du ticket.
     - Sélectionnez le type de solution et détaillez clairement la méthode de résolution appliquée. 
     - Cliquez sur "Ajouter". Le ticket bascule au statut "Résolu", et le demandeur est notifié pour validation.

---
## D. Alimenter la base de connaissances

Pour éviter que chaque informaticien redécouvre la solution à un problème déjà résolu, il est primordial de documenter les incidents complexes ou récurrents.

1. **Créer un article.** Allez dans le menu *Outils > Base de connaissances*, puis cliquez sur l'icône d'ajout (**+**) pour créer un nouvel article.

2. **Rédiger et publier.** Donnez un titre explicite (ex: "Procédure de déblocage imprimante site logistique"), détaillez les étapes de résolution dans le corps du texte, ciblez l'entité concernée, puis sauvegardez pour rendre l'article accessible au reste de l'équipe technique.
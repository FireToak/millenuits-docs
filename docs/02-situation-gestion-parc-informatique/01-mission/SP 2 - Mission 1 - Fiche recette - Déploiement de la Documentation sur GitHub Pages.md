# Fiche recette - Déploiement de la Documentation sur GitHub Pages

**SP 2 : Gestion parc informatique**

**Mission 1 : Création d'une documentation avec MkDocs et GitHub Pages**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

* **Créateur :** MEDO Louis
* **Date de création :** 05/02/2026
* **Dernière modification :** 05/02/2026
* **Validation technique :** Validé par MEDO Louis

---
## Sommaire

1. Phase 1 : Tests de l'environnement local
2. Phase 2 : Tests de la chaîne de déploiement (CI/CD)
3. Phase 3 : Recette fonctionnelle du site en ligne

---
## Phase 1 : Tests de l'environnement local

**Objectif :** Valider que l'environnement de développement est opérationnel et que le site se génère correctement sur le poste de travail.

| État | Test à réaliser                                                                        | Résultat attendu                                                    | Commentaires |
| ---- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------ |
| [  ] | **Vérification de l'installation**<br><br>Exécuter la commande : `mkdocs --version`    | La version de MkDocs doit s'afficher sans erreur python.            |              |
| [  ] | **Lancement du serveur de développement**<br><br>Exécuter la commande : `mkdocs serve` | Le serveur doit démarrer : `Serving on http://127.0.0.1:8000`.      |              |
| [  ] | **Accès local**<br><br>Ouvrir un navigateur et aller sur `http://127.0.0.1:8000`       | La page d'accueil de la documentation doit s'afficher correctement. |              |

---
## Phase 2 : Tests de la chaîne de déploiement (CI/CD)

**Objectif :** S'assurer que les GitHub Actions s'exécutent correctement et que la branche de production est mise à jour.

|**État**|**Test à réaliser**|**Résultat attendu**|**Commentaires**|
|---|---|---|---|
|[ ]|**Push des modifications**<br><br>  <br><br>Effectuer un `git push` sur la branche `main`.|Les fichiers sont envoyés sur le dépôt distant sans erreur d'authentification.||
|[ ]|**Déclenchement du Pipeline**<br><br>  <br><br>Aller dans l'onglet **Actions** du dépôt GitHub.|Un workflow nommé "Deploy MkDocs" doit apparaître en état "In progress" (Jaune) ou "Queued".||
|[ ]|**Exécution du Job**<br><br>  <br><br>Attendre la fin de l'exécution du workflow.|Le workflow doit passer au vert (Success) avec la coche validée.||
|[ ]|**Mise à jour de la branche cible**<br><br>  <br><br>Vérifier l'état de la branche `gh-pages`.|Le dernier commit sur `gh-pages` doit correspondre à l'heure du déploiement (mention "bot").||

---
## Phase 3 : Recette fonctionnelle du site en ligne

**Objectif :** Valider l'expérience utilisateur finale sur l'URL publique GitHub Pages.

|**État**|**Test à réaliser**|**Résultat attendu**|**Commentaires**|
|---|---|---|---|
|[ ]|**Accessibilité globale**<br><br>  <br><br>Accéder à l'URL : `https://ap-bts-sio-louis.github.io/millenuits/`|Le site est accessible (Code 200) et ne renvoie pas d'erreur 404.||
|[ ]|**Affichage des images**<br><br>  <br><br>Naviguer sur une page contenant le logo ou des captures d'écran.|Les images s'affichent correctement (pas d'icône d'image brisée).||
|[ ]|**Navigation inter-pages**<br><br>  <br><br>Cliquer sur les liens du menu latéral pour changer de mission.|La navigation est fluide et les liens pointent vers les bonnes pages.||
|[ ]|**Moteur de recherche**<br><br>  <br><br>Utiliser la barre de recherche (Plugin Search) pour taper un mot clé (ex: "Switch").|Des résultats pertinents s'affichent et le clic redirige vers le paragraphe concerné.||
|[ ]|**Responsive Design**<br><br>  <br><br>Réduire la fenêtre du navigateur (mode mobile).|Le menu latéral doit se transformer en menu "burger" et le texte doit rester lisible.||
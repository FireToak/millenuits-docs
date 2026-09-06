# SP 3 - Mission 2 - Installation et configuration de KEA DHCP

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

- A. Installation du service KEA DHCP
- B. Sauvegarde et préparation de la configuration
- C. Configuration globale, DNS et Passerelle
- D. Vérification et activation du service

---
## A. Installation du service KEA DHCP

1. **Mise à jour des paquets et installation.** Cette étape garantit l'installation de la dernière version stable du service DHCPv4.

```Bash
sudo apt update
sudo apt install kea-dhcp4-server
```

- `apt update` : Met à jour la liste des paquets disponibles dans les dépôts configurés.
- `apt install kea-dhcp4-server` : Télécharge et installe spécifiquement le module IPv4 du serveur Kea.

---
## B. Sauvegarde et préparation de la configuration

> **Bonne pratique :** Il est impératif de toujours sauvegarder le fichier de configuration par défaut avant d'y apporter des modifications. Cela permet un retour en arrière rapide en cas d'erreur bloquante.

1. **Création d'une copie de sauvegarde.**

```Bash
sudo cp /etc/kea/kea-dhcp4.conf /etc/kea/kea-dhcp4.conf.bak
```

- `cp` : Commande de copie de fichiers.
- `/etc/kea/kea-dhcp4.conf` : Fichier de configuration source (format JSON).
- `/etc/kea/kea-dhcp4.conf.bak` : Fichier de destination servant d'archive de sécurité.

---
## C. Configuration globale, DNS et Passerelle

1. **Édition du fichier de configuration.** Définition de l'interface d'écoute, des options globales (DNS, routeur) et de la plage d'adresses.

```Bash
sudo nano /etc/kea/kea-dhcp4.conf
```

- `nano` : Éditeur de texte en ligne de commande.

2. **Structure JSON de la configuration.** Remplacez le contenu par les paramètres adaptés à votre réseau.

```JSON
{
  "Dhcp4": {
    "interfaces-config": {
      "interfaces": [ "ens3" ]
    },
    // Durée du bail DHCP
    "valid-lifetime": 86400,
    // Serveur DHCP principal
    "authoritative": true,
    // Configuration de la base des baux DHCP
    "lease-database": {
        "type": "memfile",
        "persist": true,
        "name": "/var/lib/kea/kea-leases4.csv",
        "lfc-interval": 3600
    },

// Voir le fichier de configuration globale en annexe
```

Annexe : [kea-dhcp4.conf](./kea-dhcp4.conf)

- `"interfaces": [ "eth0" ]` : Spécifie l'interface réseau sur laquelle Kea écoutera les requêtes DHCP (à adapter selon votre système, ex: `ens33`).
- `"valid-lifetime": 4000` : Temps (en secondes) pendant lequel un client peut utiliser l'adresse IP attribuée (le bail).
- `"subnet"` : Déclare l'adresse réseau et son masque (notation CIDR).
- `"pools"` : Définit la plage d'adresses IP distribuables aux clients.
- `"routers"` : Paramètre la passerelle par défaut envoyée aux clients.
- `"domain-name-servers"` : Paramètre les serveurs DNS primaire et secondaire envoyés aux clients.

3. **Baux DHCP.** Création du dossier et du fichier contenant les baux DHCP.

```bash
sudo mkdir -p /var/lib/kea/
sudo touch /var/lib/kea/kea-leases4.csv
sudo chown -R _kea:_kea /var/lib/kea/
sudo chmod 640 /var/lib/kea/kea-leases4.csv
```

- `mkdir -p` : Crée le répertoire cible. L'option `-p` (_parents_) crée l'arborescence complète si nécessaire et évite de retourner une erreur si le dossier existe déjà.
- `touch` : Crée un fichier vide s'il n'existe pas (ou met à jour son horodatage s'il est déjà présent).
- `chown -R _kea:_kea` : Modifie le propriétaire et le groupe (`chown`) pour l'utilisateur de service `_kea` (l'utilisateur dédié créé lors de l'installation sous Debian/Ubuntu). L'option `-R` applique ce changement de manière récursive à tout le contenu du dossier.
- `chmod 640` : Applique les permissions strictes de sécurité. Le propriétaire (6 = lecture/écriture), le groupe (4 = lecture seule), et le reste du système (0 = aucun accès).

---
## D. Vérification et activation du service

> **Bonne pratique :** Toujours valider la syntaxe JSON avant de relancer le service pour éviter une interruption en production.

1. **Validation de la syntaxe.**

```Bash
sudo kea-dhcp4 -t /etc/kea/kea-dhcp4.conf
```

- `kea-dhcp4 -t` : Analyse le fichier de configuration sans démarrer le serveur pour détecter les erreurs de syntaxe JSON.

**Problème possible :**

```bash
Syntax check failed with: Unable to open file /etc/kea/kea-dhcp4.conf
```

**AppArmor** un système de sécurité peut bloquer l'exécution de la commande de vérification de syntaxe de kea. Pour corriger le problème :

```bash
sudo ln -s /etc/apparmor.d/usr.sbin.kea-dhcp4 /etc/apparmor.d/disable/
sudo apparmor_parser -R /etc/apparmor.d/usr.sbin.kea-dhcp4
```

2. **Démarrage et activation.**

```Bash
sudo systemctl restart kea-dhcp4-server
sudo systemctl enable kea-dhcp4-server
sudo systemctl status kea-dhcp4-server
```

- `systemctl restart` : Redémarre le service pour appliquer la nouvelle configuration.
- `systemctl enable` : Configure le service pour qu'il se lance automatiquement au démarrage du système.
- `systemctl status` : Affiche l'état actuel du service (vérifier qu'il est "active (running)").

---
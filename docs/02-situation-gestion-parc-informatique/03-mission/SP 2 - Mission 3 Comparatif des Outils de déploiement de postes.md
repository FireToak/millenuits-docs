**SP 2 : Gestion du Parc Informatique**

**Mission 3 : Outil de déploiement des postes**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

___
## Informations générales

- __Auteur__ : Biseray Louis
- __Date de création__ : 17/02/2026

___

## 1. Solution d'outils de déploiement  :
### Microsoft Configuration Manager (MECM / SCCM)

C'est la solution d'entreprise par excellence dans les environnements **Windows**. Elle permet de gérer le déploiement d'images système (OSD - Operating System Deployment), la mise à jour des logiciels et la conformité des postes.

- **Idéal pour :** Les réseaux locaux d'entreprise de taille moyenne à grande.

### Microsoft Intune

Intune est la solution moderne de gestion **dans le cloud**. Elle s'intègre parfaitement avec Windows 10/11 pour le déploiement (notamment via _Windows Autopilot_) et la gestion des applications, sans avoir besoin d'un serveur sur site.

- **Idéal pour :** Le travail hybride, les utilisateurs nomades et la gestion des appareils mobiles (MDM).

### FOG (Free, Open-source, Ghost)

FOG est une solution de déploiement et de gestion d'images système basée sur **Linux** (souvent installé sur un serveur Ubuntu ou Debian). Il utilise des technologies comme PXE (démarrage réseau), TFTP et NFS pour cloner des postes.

- **Idéal pour :** Les établissements scolaires, les PME, ou toute structure cherchant une solution **gratuite** et performante sans licences coûteuses, fonctionnant principalement sur un réseau local.

### 2. Comparatif des Solutions

Comparaison des Points faible / Points fort, du cout et de la pertinence des 3 solutions :

| **Caractéristique**              | **Microsoft Configuration Manager (SCCM/MECM)**                       | **Microsoft Intune**                                                                             | **FOG Project (Open Source)**                                    |
| -------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| **Architecture**                 | On-premise (Serveur local requis)                                     | Cloud (SaaS)                                                                                     | On-premise (Serveur Linux requis)                                |
| **Méthode de déploiement**       | OSD (Task Sequences), WDS/PXE                                         | Windows Autopilot, Provisioning Packages                                                         | PXE, Multicast / Unicast Imaging                                 |
| **Gestion des drivers**          | Très avancée (driver packages)                                        | Basée sur le catalogue Windows Update                                                            | Gestion via paquets de drivers post-déploiement                  |
| **Personnalisation post-image**  | Très élevée (scripts, MSI, GPO)                                       | Élevée (Scripts PowerShell, Intune Apps)                                                         | Faible (Scripts de post-clonage uniquement)                      |
| **Prérequis techniques**         | Infrastructure Active Directory, SQL Server, serveurs de distribution | Azure AD, Licences Microsoft 365                                                                 | Serveur Linux (Debian/Ubuntu), connaissances Linux               |
| **Points forts**                 | Puissance, contrôle total, idéal pour images lourdes                  | Gestion moderne, accès à distance, zéro infrastructure locale                                    | **Gratuit**, vitesse de clonage (multicast), simplicité de setup |
| **Points faibles**               | Complexité, coût, temps de mise en place                              | Coût récurrent, moins flexible pour l'imagerie sectorielle                                       | Sécurité périmétrique, pas d'outils de gestion de parc intégrés  |
| **Coût**                         | Très élevé (Licences Core + CALs)                                     | Élevé (Abonnement par utilisateur)                                                               | **Gratuit** (Open Source)                                        |
| **Analyse : 19 postes (Master)** | **Surdimensionné.** Coût et temps d'installation disproportionnés.    | **Moyen.** Mieux pour configurer des PC neufs via le cloud que pour cloner une image spécifique. | **Parfait.** C'est l'outil conçu pour cet usage précis.          |

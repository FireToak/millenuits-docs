# SP 1 - Mission 1 - Plan d'adressage

**SP 1 : Gestion de l'infrastructure réseau**

**Mission 1 : Définir un nouveau plan d'adressage**

**Contexte : MILLENUITS**

![Logo MilleNuits](https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png)

---
## Informations générales

- **Date de création** : 15/01/2026
- **Dernière modification** : 15/01/2026
- **Auteur** : MEDO Louis

---
## Sommaire

- A. Besoins en hôtes
- B. Plan d'adressage
- C. Méthodologie de calcul (Exemple)

---
## A. Besoins en hôtes

| **Nom du sous-réseau** | **Services concernés**                        | **Nombre d'hôtes** | **Hôtes avec marge (+20%)** |
| ---------------------- | --------------------------------------------- | ------------------ | --------------------------- |
| Production             | Production                                    | 110                | 110 * 1.2 ≈ 132             |
| Autres                 | Ventes, achats, qualité, études, informatique | 100                | 100 * 1.2 = 120             |
| Administratif          | Administratif, Direction                      | 52                 | 52 * 1.2 ≈ 63               |
| VentesEtudes           | Projets, Etudes                               | 48                 | 48 * 1.2 ≈ 58               |
| Logistique             | Logistique, gestion des stocks                | 30                 | 30 * 1.2 = 36               |
|                        | **Total :**                                   | 340                | 411                         |
| Serveurs               | Zone Serveurs (DMZ/LAN)                       | -                  | -                           |

> Règle de nommage : La passerelle est la dernière adresse disponible du sous-réseau.
> Exception : Le sous-réseau Serveurs utilise la passerelle 172.16.51.252/24.

---
## B. Plan d'adressage

### Réseaux et VLANs :

| **Nom**       | **N° VLAN** | **Adresse Réseau** | **Masque (CIDR)**        | **Passerelle** | **Diffusion (Broadcast)** |
| ------------- | ----------- | ------------------ | ------------------------ | -------------- | ------------------------- |
| Production    | 10          | 172.40.0.0         | 255.255.255.0 (/24)      | 172.40.0.254   | 172.40.0.255              |
| Autres        | 11          | 172.40.1.0         | 255.255.255.128 (/25)    | 172.40.1.126   | 172.40.1.127              |
| Administratif | 12          | 172.40.1.128       | 255.255.255.128 (/25)    | 172.40.1.254   | 172.40.1.255              |
| VentesEtudes  | 13          | 172.40.2.0         | 255.255.255.192<br>(/26) | 172.40.2.62    | 172.40.2.63               |
| Logistique    | 14          | 172.40.2.64        | 255.255.255.192 (/26)    | 172.40.2.126   | 172.40.2.127              |
| Invité        | 15          | 172.40.2.128       | 255.255.255.240<br>/28   | 172.40.2.142   | 172.40.2.143              |
| Management    | 99          | 172.40.2.144       | 255.255.255.240<br>/28   | 172.40.2.158   | 172.40.2.159              |

### Plages d'hôtes :

| **Nom**       | **N° VLAN** | **Première adresse** | **Dernière adresse** |
| ------------- | ----------- | -------------------- | -------------------- |
| Production    | 10          | 172.40.0.1           | 172.40.0.254         |
| Autres        | 11          | 172.40.1.1           | 172.40.1.126         |
| Administratif | 12          | 172.40.1.129         | 172.40.1.254         |
| VentesEtudes  | 13          | 172.40.2.1           | 172.40.2.62          |
| Logistique    | 14          | 172.40.2.65          | 172.40.2.126         |

---
## C. Méthodologie de calcul (Exemple)

**Détail du calcul pour le sous-réseau "Production" (132 hôtes nécessaires) :**

1. Déterminer la puissance de 2 nécessaire (n)
    
    On cherche $n$ tel que $2^n - 2 \ge \text{Nombre d'hôtes}$.
    $$2^8 - 2 = 254$$
    
    Comme $254 \ge 132$, nous avons besoin de 8 bits pour la partie hôte.
    
2. Calculer le masque de sous-réseau
    
    Le masque total est de 32 bits. On soustrait les bits hôtes trouvés ci-dessus.
    
    $$32 - 8 = 24$$
    
    Le préfixe CIDR est donc /24.
    
3. Convertir le masque en décimal
    
    On positionne les 24 premiers bits à 1 (partie réseau) et les 8 derniers à 0 (partie hôte).
    
    11111111.11111111.11111111.00000000
    
    > Résultat : **255.255.255.0**
    
4. Calculer l'adresse de diffusion (Broadcast)
    
    On prend l'adresse réseau et on passe tous les bits de la partie hôte (les 8 derniers) à 1.
    
    172.40.0.11111111
    
    > Résultat : **172.40.0.255**
    
5. **Définir la plage d'adresses utilisables**
    
    - **Première IP** : Adresse réseau + 1 $\rightarrow$ **172.40.0.1**
        
    - **Dernière IP** : Adresse de diffusion - 1 $\rightarrow$ **172.40.0.254**

---
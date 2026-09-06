# Matrice des flux - Millenuits GP1

<div style="display: flex; gap: 10px;">
  <img src="https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png" width="120" height="100">
</div>

---

- **Mainteneur** : Louis MEDO
- **Dernière édition** : 23/02/2026

---

|**Source**|**Destination**|**Protocole / Port**|**Action**|**Interface / Sens**|
|---|---|---|---|---|
|**VLAN 15 - Invité** (172.40.2.128/28)|Réseaux internes (172.16.0.0/12)|IP (Tout)|Deny|Routeur (Vlan15) - IN|
|**VLAN 15 - Invité** (172.40.2.128/28)|Internet (Any)|TCP/UDP 80, 443, 53|Permit|Routeur (Vlan15) - IN|
|**VLAN 10 - Production** (172.40.0.0/24)|Autres VLANs|IP (Tout)|Deny|Routeur (Vlan10) - IN|
|**Tous les VLANs internes**|Serveur MN01 (AD/DNS/DHCP)|UDP 53, 67, 68|Permit|Routeur (Vlans respectifs) - IN|
|**VLANs 12 & 13** (Admin / Ventes)|Serveur MN03 (PGI)|TCP (Ports PGI)|Permit|Routeur (Vlan12 & 13) - IN|
|**Tous les VLANs internes**|Serveur MN06 (Incidents) 172.16.51.6|TCP 80, 443|Permit|Routeur (Vlans respectifs) - IN|
|**Any**|**Any**|IP (Tout)|Deny|Règle implicite (Fin d'ACL)|

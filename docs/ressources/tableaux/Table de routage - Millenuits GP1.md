# Table de routage - Millenuits GP1

<div style="display: flex; gap: 10px;">
  <img src="https://millenuits.bts.loutik.fr/assets/banniere_millenuits.png" width="120" height="100">
</div>

---

- **Mainteneur** : Louis MEDO
- **Dernière édition** : 23/02/2026

---

| Commentaire   | Destination  | Masque          | Passerelle    | Interface     | Type |
| ------------- | ------------ | --------------- | ------------- | ------------- | ---- |
| Default       | 0.0.0.0      | 0.0.0.0         | 172.16.31.254 | 172.16.29.11  | S    |
| Production    | 172.40.0.0   | 255.255.255.0   | 172.40.0.254  | 172.40.0.254  | C    |
| Autres        | 172.40.1.0   | 255.255.255.128 | 172.40.1.126  | 172.40.1.127  | C    |
| Administratif | 172.40.1.128 | 255.255.255.128 | 172.40.1.254  | 172.40.1.254  | C    |
| VentesEtudes  | 172.40.2.0   | 255.255.255.192 | 172.40.2.62   | 172.40.2.63   | C    |
| Logistique    | 172.40.2.64  | 255.255.255.192 | 172.40.2.126  | 172.40.2.127  | C    |
| Invité        | 172.40.2.128 | 255.255.255.240 | 172.40.2.142  | 172.40.2.143  | C    |
| Management    | 172.40.2.144 | 255.255.255.240 | 172.40.2.158  | 172.40.2.158  | C    |
| Serveurs      | 172.16.51.0  | 255.255.255.0   | 172.16.51.252 | 172.16.51.252 | C    |

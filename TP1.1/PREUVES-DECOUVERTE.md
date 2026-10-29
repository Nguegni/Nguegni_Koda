# TP1.1 — Découverte et rapprochement des sources

**Binôme :** NGUEGNI ONGOLO Antoine Depadoux — NKODA Xavier  
**Date de relevé :** 29 octobre 2026  
**Autorisation :** topologie isolée CamTrust Bank du TP0.1, profil A.

## Méthode et périmètre

Trois sources ont été croisées : voisinage CDP, attributions DHCP et découverte active Nmap. Les seules cibles du scan sont le réseau du siège `10.10.10.0/24` et le serveur de démonstration `203.0.113.10`, conformément à l’énoncé.

| Source | Commande | Résultat utile |
|---|---|---|
| Voisinage Cisco | `show cdp neighbors detail` | R-DLA et SW-SIEGE identifiés, avec interfaces et versions annoncées. |
| Voisinage MikroTik | `/ip neighbor print detail` | R-SIEGE identifié à `172.16.12.1`, Cisco IOSv 15.6(2)T, sur `ether1`. |
| DHCP siège | `show ip dhcp binding` | Bail actif `10.10.10.100` attribué à CLIENT-LINUX. |
| DHCP Douala | `/ip dhcp-server lease print` | Aucun bail retourné à l’instant du relevé. |
| Scan local | `nmap -sn 10.10.10.0/24` | `10.10.10.1` et `10.10.10.100` répondent. |
| Services serveur | `nmap -sV 203.0.113.10` | FTP, SSH, DNS, HTTP et HTTPS détectés. |

## Équipements et services observés

| Élément | Adresse / interface | Version ou état observé | Source |
|---|---|---|---|
| R-SIEGE | `10.10.10.1`, `198.51.100.2`, `172.16.12.1` | Cisco IOSv 15.6(2)T ; trois interfaces actives | `show version`, `show ip interface brief`, CDP MikroTik |
| R-DLA | `172.16.12.2`, `10.20.10.1` | MikroTik CHR 7.23.8 long-term | CDP Cisco, `/system resource print`, `/ip address print` |
| SW-SIEGE | liaison avec `Gi0/0` de R-SIEGE | Cisco IOSvL2 expérimental 15.2 | CDP Cisco |
| CLIENT-LINUX | `10.10.10.100/24` | route par défaut `10.10.10.1` | DHCP Cisco, `ip -br addr`, `ip route`, Nmap |
| SRV-INTERNET | `203.0.113.10` | actif ; services TCP détectés | Nmap `-sV` |

## Services détectés sur SRV-INTERNET

| Port | État | Service | Produit et version |
|---:|---|---|---|
| 21/tcp | ouvert | FTP | vsftpd 3.0.5 |
| 22/tcp | ouvert | SSH | OpenSSH 9.6p1 Ubuntu 3ubuntu13.20 |
| 53/tcp | ouvert | DNS | dnsmasq 2.91 |
| 80/tcp | ouvert | HTTP | Apache httpd 2.4.58 (Ubuntu) |
| 443/tcp | ouvert | HTTPS | Apache httpd 2.4.58 (Ubuntu) |

## Différences entre les sources et explication

Les sources ne remontent pas le même périmètre : c’est attendu et justifie leur croisement.

1. Le voisinage CDP révèle R-DLA et SW-SIEGE, car il s’appuie sur des annonces de couche 2 entre équipements directement connectés. Le scan `10.10.10.0/24` ne voit pas R-DLA, qui est sur la liaison routée `172.16.12.0/30`, et ne remonte pas SW-SIEGE comme hôte IP administrable.
2. Le DHCP du siège prouve qu’une adresse `10.10.10.100` a été attribuée à CLIENT-LINUX ; Nmap confirme que ce poste est actif au moment de la mesure. Le DHCP de Douala ne retourne aucun bail à cet instant : l’absence de bail n’établit pas l’absence du routeur R-DLA, qui est bien confirmé par CDP.
3. Un inventaire d’entreprise doit donc combiner les configurations, les journaux d’adressage et les mesures réseau : une seule source peut être incomplète, ancienne ou limitée à son domaine de visibilité.

## Limite constatée

R-SIEGE a signalé des messages `CDP-4-DUPLEX_MISMATCH` avec SW-SIEGE. Ils sont consignés comme constat technique ; aucune correction n’a été appliquée pendant la phase de découverte afin de préserver l’état du lab.

# Index des captures — TP1.1

Déposer les captures réelles dans `TP1.1/captures/` en conservant uniquement les commandes et résultats utiles. Aucun mot de passe, jeton, fichier d’accès privé ou configuration non expurgée ne doit être visible.

| Fichier attendu | Vérification | État au 29 octobre 2026 |
|---|---|---|
| `01-r-siege-cdp.png` | `show cdp neighbors detail` | Réalisée |
| `02-r-dla-neighbor-et-dhcp.png` | `/ip neighbor print detail` puis `/ip dhcp-server lease print` | Réalisée — aucun bail DHCP retourné |
| `03-r-siege-dhcp-version-interfaces.png` | `show ip dhcp binding`, version et interfaces | Réalisée |
| `05-client-linux-nmap-lan.png` | `nmap -sn 10.10.10.0/24` | Réalisée |
| `06-client-linux-nmap-services.png` | `nmap -sV 203.0.113.10` | Réalisée |
| `07-client-linux-adresse-route-nmap.png` | Adresse, route et scan LAN CLIENT-LINUX | Réalisée |

Les fichiers 1 à 6 constituent les preuves principales exigées par l’étape découverte. Le fichier 7 sert à consolider l’inventaire ; il ne sera inclus dans le PDF final que si l’espace de cinq pages le permet.

# TP1.1 — Inventaire classifié, DICP et classification

**Binôme :** NGUEGNI ONGOLO Antoine Depadoux — NKODA Xavier  
**Méthode :** les éléments marqués *observé* viennent des commandes et captures du lab ; les valeurs métier et les propriétaires proviennent de la fiche d’identité fictive commune CamTrust Bank.

## 1. Inventaire des actifs

La criticité est le niveau DICP le plus élevé associé à l’actif. Les propriétaires sont désignés par fonction, afin que la responsabilité reste valide malgré les changements de personnel.

| # | Actif | Type / statut | Bien supporté ou valeur métier | Propriétaire | Criticité |
|---:|---|---|---|---|---:|
| 1 | Core banking | Valeur métier | comptes, soldes et opérations bancaires | Directeur des opérations | 4 |
| 2 | Base clients et relevés | Information | relation client et obligations bancaires | Directeur des opérations | 4 |
| 3 | Passerelle Mobile Money | Valeur métier | encaissements et paiements Mobile Money | Responsable Mobile Money | 4 |
| 4 | Plateforme monétique | Valeur métier | transactions cartes et distributeurs | Responsable monétique | 4 |
| 5 | Clés de chiffrement monétique | Information secrète | protection des transactions cartes | Responsable monétique | 4 |
| 6 | Messagerie d’entreprise | Valeur métier | échanges internes et relation client | Directeur des systèmes d’information | 3 |
| 7 | Site web bancaire | Valeur métier | information et accès clients | Responsable digital | 3 |
| 8 | Wi-Fi clients d’agence | Service | accès Internet visiteurs séparé du SI | Responsable réseau | 2 |
| 9 | R-SIEGE | Équipement observé | routage siège, Internet et liaison agence | Responsable réseau | 4 |
| 10 | R-DLA | Équipement observé | routage de l’agence Douala | Responsable réseau | 4 |
| 11 | SW-SIEGE | Équipement observé | commutation du réseau du siège | Responsable réseau | 3 |
| 12 | CLIENT-LINUX | Poste observé | poste de test du siège | Responsable réseau | 2 |
| 13 | SRV-INTERNET | Serveur observé | DNS, web, FTP et SSH de démonstration | Administrateur systèmes | 3 |
| 14 | Liaison fibre siège | Service télécom | accès Internet principal | Responsable réseau | 4 |
| 15 | Liaison 4G de secours | Service télécom | continuité en cas de coupure fibre | Responsable réseau | 3 |
| 16 | VPN agences | Service réseau | interconnexion Yaoundé, Douala et Garoua | Responsable réseau | 4 |
| 17 | Sauvegardes core banking | Information / support | reprise après incident | Responsable des opérations | 4 |
| 18 | Configurations réseau | Information | restauration et traçabilité des équipements | Responsable réseau | 3 |
| 19 | Comptes administrateurs | Information secrète | administration des systèmes et réseaux | Directeur des systèmes d’information | 4 |
| 20 | Journaux de sécurité | Information | détection, investigation et preuve | Responsable sécurité des SI | 3 |
| 21 | Dossiers de paie | Information confidentielle | gestion RH et obligations sociales | Directeur des ressources humaines | 4 |
| 22 | Procédures internes | Information interne | continuité des opérations | Directeur des systèmes d’information | 2 |

## 2. Grille DICP des six services

Échelle : 1 = faible, 2 = modéré, 3 = important, 4 = critique.

| Service | D | I | C | P | Criticité | Justification métier |
|---|---:|---:|---:|---:|---:|---|
| Core banking | 4 | 4 | 4 | 4 | 4 | Une indisponibilité empêche les opérations ; une altération ou fuite des comptes cause pertes, fraude et sanctions ; les opérations doivent être traçables. |
| Mobile Money | 4 | 4 | 4 | 4 | 4 | Une fraude ou une indisponibilité bloque les encaissements ; la banque doit prouver chaque opération contestée. |
| Monétique | 4 | 4 | 4 | 4 | 4 | Cartes et distributeurs exigent disponibilité, intégrité des transactions, confidentialité des données et preuve d’autorisation. |
| Messagerie | 3 | 3 | 3 | 3 | 3 | Une compromission facilite le phishing et perturbe les échanges avec clients et prestataires, sans arrêter immédiatement le core banking. |
| Site web bancaire | 3 | 3 | 3 | 2 | 3 | Une indisponibilité dégrade le service client ; une modification frauduleuse peut diffuser de fausses consignes ou collecter des données. |
| Wi-Fi clients en agence | 2 | 2 | 2 | 2 | 2 | Le service améliore l’accueil mais ne doit pas donner accès au SI bancaire ; sa panne ne doit pas empêcher les opérations. |

## 3. Classification de l’information

| Information | Niveau | Justification |
|---|---|---|
| Tarifs bancaires publiés | Public | Destinés à être communiqués aux clients. |
| Communiqués de presse | Public | Diffusion externe volontaire. |
| Procédures d’accueil | Interne | Réservées au personnel, impact limité si divulguées. |
| Annuaire interne | Interne | Facilite le fonctionnement, mais ne doit pas être publié librement. |
| Relevés de compte | Confidentiel | Données financières et personnelles des clients. |
| Fiches de paie | Confidentiel | Données personnelles et salariales des employés. |
| Contrats prestataires | Confidentiel | Conditions commerciales et données de contact. |
| Architecture réseau détaillée | Confidentiel | Aide un attaquant à cibler les équipements. |
| Clés de chiffrement monétique | Secret | Leur exposition compromet les transactions et les clients. |
| Identifiants administrateurs et sauvegardes de configuration | Secret | Permettent de prendre le contrôle du SI. |

### Règles réseau par niveau

| Niveau | Règle 1 | Règle 2 |
|---|---|---|
| Public | La publication externe doit passer par un service web administré. | Aucun accès au réseau interne ne doit être accordé depuis un espace public. |
| Interne | L’accès est réservé aux comptes du personnel authentifié. | Les transferts vers l’extérieur doivent passer par des canaux approuvés. |
| Confidentiel | Les flux doivent être chiffrés en transit. | L’accès est limité aux rôles ayant un besoin professionnel documenté. |
| Secret | Les données ne doivent jamais circuler par HTTP, FTP ou Telnet. | L’accès exige comptes nominatifs, journalisation et authentification renforcée. |

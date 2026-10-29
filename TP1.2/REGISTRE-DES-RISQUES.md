# TP1.2 — Registre des risques CamTrust Bank

**Binôme :** NGUEGNI ONGOLO Antoine Depadoux — NKODA Xavier  
**Périmètre :** établissement de crédit fictif de 300 employés ; siège à Yaoundé et agences de Douala et Garoua.  
**Méthode :** approche simplifiée inspirée d’EBIOS Risk Manager, fondée sur l’inventaire TP1.1 et la fiche d’identité fournie dans l’énoncé.

## Échelle retenue

| Valeur | Gravité | Vraisemblance |
|---:|---|---|
| 1 | Impact limité et réversible | Très peu probable |
| 2 | Perturbation localisée | Peu probable |
| 3 | Impact important sur un service, des clients ou la conformité | Plausible |
| 4 | Impact critique : interruption, fraude majeure ou atteinte grave aux données | Très plausible ou déjà observé dans le secteur |

**Niveau de risque = gravité × vraisemblance.** Priorité 1 : 12–16 ; priorité 2 : 8–11 ; priorité 3 : 1–7.

## Sources de risque retenues

| Source | Justification |
|---|---|
| Cybercriminel | Les services bancaires, données clients et paiements sont des cibles de rançongiciel et de fraude. |
| Employé ou prestataire négligent / malveillant | CamTrust compte quatre administrateurs et deux prestataires ; un accès légitime mal utilisé contourne une partie des défenses périmétriques. |
| Panne de télécommunication ou d’énergie | La fibre constitue l’accès principal et le jour de paie rend une interruption particulièrement coûteuse. |

## Registre

| ID | Valeur métier / événement redouté | Source de risque et scénario | G | V | Niveau | Traitement et mesures | Responsable / échéance | Risque résiduel |
|---|---|---|---:|---:|---:|---|---|---:|
| RSK-01 | **Core banking — indisponibilité supérieure à une journée.** | Un cybercriminel envoie un courriel piégé à un agent de Garoua → exécution d’un logiciel malveillant → propagation sur un réseau insuffisamment segmenté → chiffrement des serveurs et sauvegardes connectées. | 4 | 3 | 12 | **Réduire.** VLAN utilisateurs/serveurs, filtrage inter-VLAN, EDR, sauvegardes hors ligne testées, filtrage des courriels et plan de réponse. | DSI ; plan initial sous 90 jours. | 6 |
| RSK-02 | **Mobile Money et monétique — virement ou transaction frauduleuse.** | Un employé ou un prestataire disposant d’un accès au lien agence consulte/modifie un flux ou emploie un compte partagé → validation insuffisante → fraude puis difficulté à attribuer l’action. | 4 | 3 | 12 | **Réduire.** VPN chiffré entre sites, comptes nominatifs, MFA pour administration, journalisation centralisée, séparation des tâches et validation à deux niveaux. | Responsable monétique et Responsable réseau ; 60 jours. | 4 |
| RSK-03 | **Opérations de paie — indisponibilité de l’accès Internet principal.** | Coupure de fibre ou délestage le jour de paie → accès aux partenaires indisponible → retards de traitement et réclamations clients. | 4 | 3 | 12 | **Réduire.** Basculement 4G documenté et testé, supervision de lien, procédure de continuité et capacité adaptée. | Responsable réseau ; test sous 30 jours. | 6 |
| RSK-04 | **Messagerie et comptes administrateurs — prise de contrôle d’un compte.** | Courriel d’hameçonnage → saisie d’un identifiant → accès à la messagerie ou à une console d’administration → diffusion interne ou modification non autorisée. | 3 | 3 | 9 | **Réduire.** MFA, passerelle antiphishing, interdiction des comptes partagés, SSH plutôt que Telnet, comptes d’administration séparés et alertes de connexion. | RSSI ; 90 jours. | 4 |
| RSK-05 | **Données clients et service web — exposition ou interception de données.** | Un service FTP ou HTTP détecté sur le serveur `203.0.113.10` est utilisé pour échanger une information confidentielle → trafic lisible ou accès mal protégé → divulgation de données clients. | 3 | 3 | 9 | **Réduire.** Interdire FTP et HTTP pour données sensibles, imposer SFTP/HTTPS, désactiver les services inutiles, contrôler les accès et journaliser. | Administrateur systèmes ; 45 jours. | 3 |
| RSK-06 | **Configurations réseau et disponibilité agence — usage abusif d’un accès prestataire.** | Un prestataire utilise un accès distant permanent ou un compte non désactivé → modification de routeur/switch → interruption d’agence ou maintien d’un accès non autorisé. | 4 | 2 | 8 | **Réduire.** Accès prestataire temporaire via VPN, approbation préalable, comptes nominatifs, journalisation, sauvegarde de configuration et revue trimestrielle. | Responsable réseau ; 60 jours. | 4 |

## Lecture des priorités

Les risques RSK-01, RSK-02 et RSK-03 sont prioritaires car leur score est de 12/16. Ils concernent directement la continuité bancaire, la fraude et le jour de paie. Les risques RSK-04 et RSK-05 restent importants : les services FTP et HTTP ont été détectés par Nmap dans le lab, mais le scan seul ne démontre ni une fuite effective ni l’usage de données clients. Cette distinction est maintenue dans le registre.

## Liens avec l’inventaire TP1.1

| Risque | Actifs concernés |
|---|---|
| RSK-01 | Core banking, sauvegardes, VPN agences, postes d’agence |
| RSK-02 | Passerelle Mobile Money, monétique, VPN agences, journaux de sécurité |
| RSK-03 | Liaison fibre, secours 4G, core banking, passerelle Mobile Money |
| RSK-04 | Messagerie, comptes administrateurs, R-SIEGE, R-DLA |
| RSK-05 | Base clients, SRV-INTERNET, site web, DNS |
| RSK-06 | R-SIEGE, R-DLA, SW-SIEGE, configurations réseau, comptes administrateurs |

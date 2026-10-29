# Relevés opérateur complémentaires

Ce fichier retranscrit des sorties que l’opérateur a fournies dans la conversation le 29 octobre 2026. Il complète les captures d’écran déjà déposées ; ce n’est pas une capture substitutive.

## R-DLA — `/system resource print`

- Version : `7.23.8 (long-term)`
- Plateforme : MikroTik CHR QEMU Standard PC
- Architecture : `x86_64`
- Processeur : QEMU, 1 vCPU
- Mémoire totale : 256 MiB

## R-DLA — `/ip address print`

| Adresse | Réseau | Interface |
|---|---|---|
| `172.16.12.2/30` | `172.16.12.0` | `ether1` |
| `10.20.10.1/24` | `10.20.10.0` | `ether2` |

Ces valeurs concordent avec le voisinage CDP : R-DLA est relié à R-SIEGE par `ether1` / `GigabitEthernet0/2`.

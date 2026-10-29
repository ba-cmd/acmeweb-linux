# AcmeWeb – Mise en production d'un serveur web Linux

Projet personnel de consolidation de mes compétences en administration Linux.

## Architecture
| Machine  | Système       | Rôle                  | IP privée     |
|----------|---------------|-----------------------|---------------|
| web01    | Ubuntu Server | Serveur web           | 192.168.56.10 |
| backup01 | Rocky Linux   | Serveur de sauvegarde | 192.168.56.20 |

## Avancement
- [x] Étape 0 – Création des machines virtuelles
- [x] Étape 1 – Réseau : IP fixes et résolution des noms
- [ ] Étape 2 – Utilisateurs, groupes et droits
- [ ] Étape 3 – Sécurisation : SSH, Fail2ban, pare-feu
- [ ] Étape 4 – Stockage : LVM, fstab, swap
- [ ] Étape 5 – Serveur web Nginx en HTTPS
- [ ] Étape 6 – Service systemd
- [ ] Étape 7 – Scripts Bash
- [ ] Étape 8 – Automatisation et journaux
- [ ] Étape 9 – Namespaces et cgroups
- [ ] Étape 10 – Pannes et diagnostic
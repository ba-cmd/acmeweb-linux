## Etape 1 - Réseau : IP fixes et résolution des noms

## Objectif 
Donner une adresse IP fixe au serveur de production (web01) et au serveur de sauvegarde (backup01) sur le réseau privé.

## Pourquoi
Avec DHCP, l'adresse de l'interface réseau privé pouvait à chaque redémarrage. Les serveurs doivent avoir des adresses stables, puisque les connexions SSH, le pare feu et les futurs scripts de sauvegarde s'y connecteront.

## Ce que j'ai fait
| Machine  | Outil          | Carte privée (enp0s8) | Carte NAT (enp0s3) |
|----------|----------------|-----------------------|--------------------|
| web01    | Netplan        | 192.168.56.10/24      | DHCP (Internet)    |
| backup01 | NetworkManager | 192.168.56.20/24      | DHCP (Internet)    |

-L'interface privé n'a pas de passerelle : l'accès à internet passe uniquement par la carte NAT pour éviter deux routes par défaut.
-Configuration de web01: voir 'config/netplan/00-installer-config.yaml' 
-Configuration backup01:
'''bash
sudo nmcli connection modify enp0s8 ipv4.method manual \
  ipv4.addresses 192.168.56.20/24 ipv4.never-default yes
sudo nmcli connection up enp0s8
'''

## Résolution des noms
Dans un premier temps, j'ai associé un nom à chaque adresse IP dans le
fichier `/etc/hosts` des deux serveurs :

'''
192.168.56.10   web01   acmeweb.local
192.168.56.20   backup01
'''
Dans un environnement plus grand, on utiliserait un serveur DNS pour centraliser ces noms au lieu de les récopier sur  chaque machine.

### Vérification
- 'ping backup01' depuis web01 et 'ping web01' depuis backup01 : OK
- 'ping google.com' : Internet fonctionne toujours
- 'ip route' : la route par défaut passe uniquement par enp0s3
- Tout fonctionne encore après redémarrage
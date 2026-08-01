---
icon: simple/linuxserver
hide:
  - toc
  - path
---

# Présentation
![Image title](../../../assets/docker/swag/linuxserver.png){ align=right }

SWAG (Secure Web Application Gateway) est un conteneur docker créer par linuxserver.io, ce conteneur inclut un serveur web Nginx, un proxy inverse avec prise en charge PHP et un client certbot intégré qui automatise la génération et le renouvellement gratuits des certificats SSL (Let's Encrypt et ZeroSSL). Il inclut également fail2ban pour la prévention des intrusions.

## Prérequis

- __Docker__ et __Docker Compose__ installé sur sa machine.
- Conection __SSH__ à votre Serveur/NAS
- Un __Nom de domaine__ (vous pouvez utiliser <a href="https://www.duckdns.org/" target="_blank" rel="noopener noreferrer">duckdns.org</a> car il est gratuit et supporté par SWAG) 
- Un __Split DNS__ (Voir <a href="https://docs.linuxserver.io/general/split-dns/" target="_blank" rel="noopener noreferrer">docs.linuxserver.io/general/split-dns/</a> pour plus de précision)
- Redirection du port __443__ en __TCP__ vers votre Serveur/NAS sur votre firewall/box
---

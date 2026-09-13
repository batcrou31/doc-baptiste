---
icon: simple/linuxserver
hide:
  - toc
  - path
---

![Image title](../../../assets/docker/swag/linuxserver.png){ align=right }
# :material-file-find: Présentation

<a href="https://github.com/linuxserver/docker-swag" target="_blank" rel="noopener noreferrer">SWAG :fontawesome-solid-arrow-up-right-from-square:</a> (Secure Web Application Gateway) est un conteneur docker créer par linuxserver.io, ce conteneur inclut un serveur web Nginx, un proxy inverse avec prise en charge PHP et un client certbot intégré qui automatise la génération et le renouvellement gratuits des certificats SSL (Let's Encrypt et ZeroSSL). Il inclut également fail2ban pour la prévention des intrusions.

## :octicons-cpu-16: Prérequis

- __Docker__ et __Docker Compose__ installé sur sa machine.
- Conection __SSH__ à votre Serveur/NAS
- Un __Nom de domaine__ (vous pouvez utiliser <a href="https://www.duckdns.org/" target="_blank" rel="noopener noreferrer">Duck DNS :fontawesome-solid-arrow-up-right-from-square:</a> car il est gratuit et supporté par SWAG) 
- Un __Split DNS__ (Voir <a href="https://docs.linuxserver.io/general/split-dns/" target="_blank" rel="noopener noreferrer">docs.linuxserver.io/general/split-dns :fontawesome-solid-arrow-up-right-from-square:/</a> pour plus de précision)
- Redirection du port __443__ en __TCP__ vers votre Serveur/NAS sur votre firewall/box
---

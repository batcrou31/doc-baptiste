---
icon: fontawesome/solid/eye
created: 2026-09-09
modified: 2026-09-09
hide:
  - footer
---

# Serveur TigerVNC (Xfce)

## 1 - Prérequis

- Un système Debian 12 ou 13 avec un <a href="https://www.xfce.org/" target="_blank" rel="noopener noreferrer">environnement de bureau Xfce/</a>
- Une Connexion SSH

## 2 - Installation

### Installation des paquets
Mises à jour/installation des paquets de TigerVNC :
```
sudo apt update
sudo apt install tigervnc-standalone-server tigervnc-common dbus-x11 -y
```
<figure markdown="span">
  ![Image title](../../assets/linux/debian_vnc/VNC-1){ width="700" }
</figure>

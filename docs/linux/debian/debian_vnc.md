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
  ![Image title](../../assets/linux/debian/debian_vnc/VNC-1.PNG){ width="800" }
</figure>

## Définition d'un mot de passe VNC
Maintenant il faut définir un mot de passe avec la commande suivante :
```
vncpasswd
```
!!! note
    Le maximum est de 8 caractères, il est également possible de définir un mot de passe de lecture seule

<figure markdown="span">
  ![Image title](../../assets/linux/debian/debian_vnc/VNC-2.PNG){ width="650" }
</figure>

### Configuration du lancement XFCE dans VNC
Création/édition du fichier `xstartup` :
```
mkdir -p ~/.vnc
nano ~/.vnc/xstartup
```
Contenu du fichier `xstartup` :

``` bash
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec startxfce4
```
Puis il faut rendre le fichier exécutable :

```
chmod +x ~/.vnc/xstartup
```

### Test du serveur
Toujours dans le terminal, entrez la commande suivante :
```
vncserver :1 -localhost no -geometry 1920x1080 -depth 24
```

??? note

    - `:1` correspond au port `5901` (:1 = 5900+1, :2 = 5900+2, etc...)
    - Ajustez `-geometry` à la résolution voulue
    - l'argument `-localhost no` autorise les connexions distantes

Dans le client VNC de votre choix, entrez l'adresse IP ainsi que l'identifiant (Nom de la machine par exemple).
<figure markdown="span">
  ![Image title](../../assets/linux/debian/debian_vnc/VNC-3.PNG){ width="650" }
</figure>

La commande suivante est pour arrêter le server VNC :
```
vncserver -kill :1
```

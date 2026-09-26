---
icon: simple/wireguard
hide:
  - footer
---

# Wireguard
:material-calendar-blank: __26/09/2026__ - :material-note: _Tuto réalisé sur une machine virtuelle debian 13_
## 1 - Présentation

<a href="https://www.wireguard.com/" target="_blank" rel="noopener noreferrer">WireGuard :fontawesome-solid-arrow-up-right-from-square:</a> est un VPN moderne, léger et sécurisé qui permet de créer des connexions chiffrées rapides entre des appareils ou des réseaux distants.

## 2 - Prérequis

- Un __serveur Debian__ 12/13 [:fontawesome-solid-arrow-right: Configuration de base](../linux/debian/debian.md)

## 3 - Installation

Pour installer Wireguard, il faut utiliser le script de <a href="https://github.com/angristan" target="_blank" rel="noopener noreferrer">Angristan :fontawesome-solid-arrow-up-right-from-square:</a> :

```
curl -O https://raw.githubusercontent.com/angristan/wireguard-install/master/wireguard-install.sh
chmod +x wireguard-install.sh
./wireguard-install.sh
```

!!! note "Information importante"
    Si vous avez une erreur avec __curl__, cela signifie qu'il n'est pas installé sur la machine.    
    <div style="page-break-after: always;"></div>

    il l'installer avec la commande suivante :
    ``` 
    apt install curl
    ```
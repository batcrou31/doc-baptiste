---
icon: simple/cisco
date: 2026-01-03
---

# Commandes Globale
## 1 - Commandes de base
- `enable` : Se mettre en privilège élevé sur le switch
- `copy running-config startup-config` : Copier le fichier de configuration dans la mémoire interne du switch
- `show running-config` : Voir la configuration en  cours d'exécution du switch.
- `show startup-config` : Voir la configuration initiale dans la mémoire vive non volatile du switch.
- `show interface vlan[1-...]` : Voir les caractéristiques de l'interface VLAN.
- `show ip interface vlan[1-...]` : Voir les propriétés IP de l'interface VLAN.
- `show version` : Voir les informations relatives à la version de Cisco IOS du switch.
- `show interface f[0/…]` : Voir les propriétés par défaut de l'interface FastEthernet 0/…
- `show vlan` : Voir les paramètres VLAN par défaut du switch.
- `show flash` : Voir les paramètres VLAN par défaut du switch.
- `show hostname` : Attribuez le nom d'hôte du switch.
- `ping <host_ip>` : Ping une machine.
---
## 2 - Export/Import de la configuration
- `copy running-config tftp` : Copie de la configuration du switch sur le serveur FTP.
- `copy tftp running-config` : Copie de la configuration du serveur FTP vers le switch.
---
## 3 - Configuration IP
- `enable` : Se mettre en privilège élevé sur le switch
- `configure terminal` : Configuration globale du switch
- `interface vlan 1` : (vlan1 par défaut) 
- `ip address <adresse> <masque>` : (ex: ip address 192.168.1.253 255.255.255.0)
- `no shutdown` : (pas d'arrêt) Cette commande est obligatoire sinon l'interface ne s'allumera pas.
---
## 4 - Les VLAN
- `enable` : Se mettre en privilège élevé sur le switch
- `configure terminal` : Configuration globale du switch
### Création des VLAN
Création d'un VLAN 10 et 20
``` 
Switch(config)#vlan 10 
Switch(config-vlan)#name vlan_10 
Switch(config-vlan)#vlan 20
Switch(config-vlan)#name vlan_20
```
### Aplication des VLAN sur les ports en mode "trunk"
Le mode trunk permet de ==transmetre des données provenant ^^de plusieurs VLAN^^.==

<div style="page-break-after: always;"></div>

- Exemple avec le port n°1
``` 
Switch(config)#interface fa0/1
Switch(config-if)#switchport mode trunk 
Switch(config-if)#no shutdown
Switch(config-if)#exit
```
!!! note "Information importante"
    Il est également possible de spécifier les VLAN car par défaut **toutes les VLANS peuvent passer sur un port trunk**.
    ```
    Switch(config-if)#switchport trunk allowed vlan 20,30,99
    ```
### Aplication des VLAN sur les ports en mode "access"
Le mode acces permet de ==transmetre des données au sein ^^d'un même VLAN^^.==

<div style="page-break-after: always;"></div>

- Exemple avec le port n°10
``` 
Switch(config)#interface fa0/10
Switch(config-if)#switchport access vlan 20 
Switch(config-if)#no shutdown
Switch(config-if)#exit
``` 
## 5 - Configuration routeur
- `enable` : Se mettre en privilège élevé sur le routeur.
- `configure terminal` : Configuration globale du routeur.
- `interface FastEthernet 0/0` : On entre dans la configuration de l'interface 0/0.
- `ip address 192.168.1.254 255.255.255.0` : on lui attribue l'IP `192.168.1.254` avec le masque `255.255.255.0`
- `no shutdown` : on active l'interface réseau.
- `ip routing` : on applique la route des interfaces du switch.
- `show ip route` : affiche la table de routage.
## 6 - Configuration du SSH
- `configure terminal` : Configuration globale du switch
- `hostname sw1` : Nom d'hôte
- `ip domain-name baptiste` : Nom de domaine
- `crypto key generate rsa` : Générer un certificat pour la connexion SSH (2048 bits)
``` 
ip ssh version 2
line vty 0 4
transport input ssh
login local
``` 
- `username baptiste password 123456` :
!!! warning "Attention"
    Ne pas oublier d'enregistrer la conf sur le switch.
    ```
    wr : pour écrire la configuration sur le switch
    ```
Commande pour se connecter en ssh depuis windows sur un équipement cisco :
```
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedAlgorithms=+ssh-rsa -oCiphers=+3des-cbc -oMACs=+hmac-sha1 nomdutilisateur@adresseip
```
---
## 7 - Remise à plat du switch
- `write erase` : Commande de mise en configuration d’usine du switch.
- `delete flash:vlan.dat` : Commande de mise en configuration d’usine du switch. 
- `reload` : Commande de mise en configuration d’usine du switch. (NO/ENTER) 
- `copy run start` : Commande de mise en configuration d’usine du switch. 

---

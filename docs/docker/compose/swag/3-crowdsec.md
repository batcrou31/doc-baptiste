---
icon: selfhst/crowdsecd
---

# Plugin Crowdsec

<a href="https://www.crowdsec.net/" target="_blank" rel="noopener noreferrer">CrowdSec :fontawesome-solid-arrow-up-right-from-square:</a> est un outil de cybersécurité open source qui protège les serveurs et applications contre les attaques automatiques (bruteforce SSH, scans, bots, DDoS, etc.).
<div style="page-break-after: always;"></div>
Le principe est simple :
<div style="page-break-after: always;"></div>

- CrowdSec analyse les logs des vos services (Nginx, nextcloud, jellyfin etc.)
- Détecte les comportements suspects
- Bloque automatiquement les IP malveillantes
- Partage anonymement ces IP avec la communauté CrowdSec

## 1 - Fichier docker compose

``` yaml
services:
  swag:
    image: lscr.io/linuxserver/swag:latest
    container_name: swag
    cap_add:
      - NET_ADMIN
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Paris
      - URL=exemple.fr
      - SUBDOMAINS=wildcard
      - VALIDATION=dns
      - DNSPLUGIN=ovh
    volumes:
      - /home/docker/appdata/swag/config:/config
    ports:
      - 443:443
    networks:
      swag_net:
        ipv4_address: 172.25.0.5
    restart: unless-stopped

  crowdsec:
    container_name: crowdsec
    image: crowdsecurity/crowdsec
    restart: unless-stopped
    environment:
      - COLLECTIONS=crowdsecurity/nginx crowdsecurity/http-cve crowdsecurity/whitelist-good-actors # (1)
      - GID=1000
    depends_on:
      - swag
    volumes:
      - /home/docker/appdata/crowdsec/config:/etc/crowdsec:rw
      - /home/docker/appdata/crowdsec/data:/var/lib/crowdsec/data:rw
      - /home/docker/appdata/swag/config/log/nginx:/var/log/nginx:ro
      - /var/log:/var/log/host:ro 
    security_opt:
      - no-new-privileges=true
    networks:
      crowdsec_net:
        ipv4_address: 172.25.0.10

networks:
  swag_net:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 172.25.0.0/16
          gateway: 172.25.0.1
```

1.  Liste des collections disponible : <a href="https://app.crowdsec.net/hub/collections" target="_blank" rel="noopener noreferrer">app.crowdsec.net/hub/collections :fontawesome-solid-arrow-up-right-from-square:</a>

## 2 - Configuration
### Configuration du Bouncer sur SWAG

Pour ajouter un "bouncers" à notre conteneur crowdsec, il faut executer cette commande :
```
docker exec -t crowdsec cscli bouncers add bouncer-swag
```

Cela va génerer une clé API à ajouter dans les paramètres d'environnement de SWAG.
<div style="page-break-after: always;"></div>
Dans le champs "environnement:" de votre docker compose, nous allons devoirs rajouter 3 paramètres suivants :

``` yaml
- DOCKER_MODS=linuxserver/mods:swag-crowdsec
- CROWDSEC_API_KEY=hg45a7235458c69c46f59574334sk11p
- CROWDSEC_LAPI_URL=http://crowdsec:8080
```
!!! note "Information Importante"
    Si vous avez déjà un mods, il sufit d'ajouter : `|` entre vos mods exemple : `linuxserver/mods:swag-dbip|linuxserver/mods:swag-crowdsec` 

<div style="page-break-after: always;"></div>
!!! warning "Attention"
    la valeur : `hg45a7235458c69c46f59574334sk11p` de la variable __CROWDSEC_API_KEY__ est a remplacer par l'apikey que vous a donner la commande au début de ce paraphaphe.

Ensuite il faut vous faut modifier le fichier __acquis.yaml__ présent dans __/crowdsec/config/__ :

``` yaml
filenames:
  - /var/log/nginx/*.log
labels:
  type: nginx
---
```

Après avoir redémarrer votre conteneur, verifier dans les log si les fichiers d'acquisition ont bien été pris en compte par crowdsec :

```
time="2026-04-23T12:19:02Z" level=info msg="loading acquisition file : /etc/crowdsec/acquis.yaml"
time="2026-04-23T12:19:02Z" level=info msg="Configuring datasource" module=acquisition.file type=file
time="2026-04-23T12:19:02Z" level=info msg="Adding file /var/log/nginx/access.log to datasources" module=acquisition.file type=file
time="2026-04-23T12:19:02Z" level=info msg="Adding file /var/log/nginx/error.log to datasources" module=acquisition.file type=file
```
### Lier son instance à l'app Crowdsec

Tout d'abord, Aller sur le site <a href="https://app.crowdsec.net/" target="_blank" rel="noopener noreferrer">app.crowdsec.net/ :fontawesome-solid-arrow-up-right-from-square:</a> et créer un compte.
On vous proposera ensuite d'enregistrer une instance à l'aide d'une commande :

```
docker exec -t crowdsec cscli console enroll 12345xxxxxxxxxxxx
```
Retourner ensuite le site et cliquer sur "accept" pour enregistrer l'instance.


## 3 - Commandes utiles
```
docker exec -t crowdsec cscli metrics
```
Voir la liste de "decisions" en cours :

```
docker exec -t crowdsec cscli decisions list
```

Purger la liste de "decisions" en cours :
```
docker exec -t crowdsec cscli decisions delete --all
```
Supprimer les "decisions" sur une ip ( ici 1.2.3.0 ) :

```
docker exec -t crowdsec cscli decisions delete -i 1.2.3.4
```

---

## Sources

- <a href="https://github.com/linuxserver/docker-mods/tree/swag-dbip" target="_blank" rel="noopener noreferrer">github.com/linuxserver/docker-mods/tree/swag-dbip</a>
- <a href="https://github.com/linuxserver/docker-mods/tree/swag-crowdsec" target="_blank" rel="noopener noreferrer">github.com/linuxserver/docker-mods/tree/swag-crowdsec</a>

---

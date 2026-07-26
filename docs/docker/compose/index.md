---
icon: simple/docker
---

# Commandes utiles

^^__Redémarrer tout les conteneurs__^^ :
```
docker restart $(docker ps -a -q)
```
^^__Envoyer une commande dans un conteneur__^^ :
```
docker exec -t <nom_du_conteneur> <commande>
```

---

# Exemple de docker compose

## Freefilesync

``` yaml
services:
  freefilesync:
    image: jlesage/freefilesync
    container_name: freefilesync
    environment:
      - USER_ID=0 # (1)!
      - GROUP_ID=0
      - TZ=Europe/Paris
      - FFS_SCHEDULED_BATCH_JOB_1_NAME=Save1
      - FFS_SCHEDULED_BATCH_JOB_1_CRON=0 19 * * * 
    ports:
      - 5800:5800
    volumes:
      - /home/docker/appdata/freefilesync:/config:rw
      - /srv/dev-disk-by-uuid-781979ce-41dc-4bad-9e35-ee8cdcdbb0f5:/storage:rw
    restart: unless-stopped 

networks:
  default:
    name: freefilesync
```

1.  Pour trouver l'id de l'utilisateur et du groupe faite la commande "id" suivie du nom de votre utilisateur.
    <div style="page-break-after: always;"></div>
    (l'utilisateur root est toujours O)

### Sources

- <a href="https://github.com/jlesage/docker-freefilesync" target="_blank" rel="noopener noreferrer">github freefilesync</a>
- <a href="https://crontab.guru/" target="_blank" rel="noopener noreferrer">crontab</a>
---

## Pack de docker compose (Old)

[Télécharger](../../assets/docker/compose-old.zip){ .md-button target=_blank } 

---

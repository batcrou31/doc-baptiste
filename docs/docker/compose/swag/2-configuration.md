---
icon: fontawesome/solid/cogs
---

# Configuration

## 1 - Activation du HSTS

Editer votre fichier __ssl.conf__ présent dans votre dossier __/config/nginx/__
<div style="page-break-after: always;"></div>
et décommenter la ligne suivante :

``` conf
add_header Strict-Transport-Security "max-age=63072000" always;
```
puis également ajouter cette ligne afin d'empêcher vos applications d'apparaître dans les résultats des moteurs de recherche et d'être indexées :
``` conf
add_header X-Robots-Tag "noindex, nofollow, nosnippet, noarchive";
```

## 2 - Désactivation de la page par défaut du domaine

Editer votre fichier __default.conf__ présent dans votre dossier __/config/nginx/site-confs__
<div style="page-break-after: always;"></div>

et remplacez la partie __location__ :

``` conf
    location / {
        # enable for basic auth
        #auth_basic "Restricted";
        #auth_basic_user_file /config/nginx/.htpasswd;

        # enable for ldap auth (requires ldap-server.conf in the server block)
        #include /config/nginx/ldap-location.conf;

        # enable for Authelia (requires authelia-server.conf in the server block)
        #include /config/nginx/authelia-location.conf;

        # enable for Authentik (requires authentik-server.conf in the server block)
        #include /config/nginx/authentik-location.conf;

        return 444;
    }
```
l'erreur 444 sera alors retournée lors de chaques requètes sur votre domaine racine.

## 3 - Plugin DBIP

Pour activer le plugin, il sufit de rajouter la variable d'environnement suivante : 

``` yaml
- DOCKER_MODS=linuxserver/mods:swag-dbip
```
Exemples :
``` yaml
    environment:
      - PUID=996
      - PGID=100
      - TZ=Europe/Paris
      - URL=exemple.fr
      - SUBDOMAINS=wildcard
      - VALIDATION=dns
      - DNSPLUGIN=ovh
      - EMAIL=exemple@exemple.com
      - DOCKER_MODS=linuxserver/mods:swag-dbip
```

ensuite, il faut ajouter diter votre fichier __nginx.conf__ dans __/config/nginx/__ sous la section __http__ :

``` conf
include /config/nginx/dbip.conf;
```

``` conf
http {
    include /config/nginx/dbip.conf;
    # Includes mapping of file name extensions to MIME types of responses
    # and defines the default type.
    include /etc/nginx/mime.types;
    default_type application/octet-stream;
```

Après avoir redemarré votre conteneur, il faut ajouter des pays à la liste de blocage / liste blanche dans `/config/nginx/dbip.conf` :

``` conf
map $geoip2_data_country_iso_code $geo-whitelist {
    #default yes;
    # Example for whitelisting a country, comment out 'default yes;' above and uncomment 'default no;' and the whitelisted country below
    default no;
    FR yes;
}
```

Cette configuration indique que par défaut, aucun pays ne peux acceder aux ressources du proxy inverse sauf la France. 

<div style="page-break-after: always;"></div>

Il faut également créer 2 fichiers dans __/config/nginx/__ : 

- internal.conf 
- external.conf

<div style="page-break-after: always;"></div>

Contenu du fichier __internal.conf__ :

``` conf
allow 192.168.1.0/24; # Replace with your LAN subnet
deny all;
```

ce fichier autorise la connexion uniquement à vos machines présentes sur votre réseau local.

<div style="page-break-after: always;"></div>

Contenu du fichier __external.conf__ :

``` conf
    if ($lan-ip = yes) { set $geo-whitelist yes; }
    if ($geo-whitelist = no) { return 404; }
```

ce fichier autorise la conexion si votre client se situe dans votre réseau local sinon, si votre pays d'origine est autre que la France une erreur 404 sera retourné.

---

## Sources

- <a href="https://github.com/linuxserver/docker-mods/tree/swag-dbip" target="_blank" rel="noopener noreferrer">github.com/linuxserver/docker-mods/tree/swag-dbip</a>
- <a href="https://github.com/linuxserver/docker-mods/tree/swag-crowdsec" target="_blank" rel="noopener noreferrer">github.com/linuxserver/docker-mods/tree/swag-crowdsec</a>

---

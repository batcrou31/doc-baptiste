---
icon: fontawesome/solid/cogs
created: 2026-03-06
modified: 2026-03-06
---

# Configuration

## 1 - Modification du fichier de configuration
Navigez dans vers votre fichier de configuration :
```
cd /home/docker/appdata/nextcloud/config/www/nextcloud/config
```

Puis ouvrez le fichier `config.php`, contenu du fichier :

``` php
<?php
$CONFIG = array (
  'datadirectory' => '/data',
  'instanceid' => 'ocnsucaxnfrp',
  'passwordsalt' => 'eC+62u0sczgVmBejLemCdl0A3QibMl',
  'secret' => '4aLsJ4VjvJQmpYhUPLvCySZLDQM6hx2H3AJRxNdDmGVmzXve',
  'trusted_domains' => 
  array (
    0 => '192.168.1.15:450',
  ),
  'dbtype' => 'mysql',
  'version' => '33.0.0.16',
  'overwrite.cli.url' => 'https://192.168.1.15:450',
  'dbname' => 'nextcloud',
  'dbhost' => 'nextclouddb',
  'dbtableprefix' => 'oc_',
  'mysql.utf8mb4' => true,
  'dbuser' => 'oc_oc_admin',
  'dbpassword' => 's[d7%9n7qs,~8iMHdJ6;Nx<!f[rT*P',
  'installed' => true,
);
```
Paramètres de base à rajouter :

``` php
  'maintenance' => false,
  'maintenance_window_start' => 1,
  'filesystem_check_changes' => 1,
  'default_phone_region' => 'FR',
```
Paramètres SMTP à rajouter :
``` php
  'mail_smtpmode' => 'smtp',
  'mail_sendmailmode' => 'smtp',
  'mail_smtphost' => 'smtp.gmail.com',
  'mail_smtpsecure' => 'ssl',
  'mail_smtpport' => '465',
  'mail_from_address' => 'exempleSMTP',
  'mail_domain' => 'gmail.com',
  'mail_smtptimeout' => 30,
  'mail_smtpauth' => true,
  'mail_smtpname' => 'exempleSMTP@gmail.com',
  'mail_smtppassword' => 'mot_de_passe',
```
!!! warning "Attention"
    Il faut également ajouter l'adresse mail sur laquelle vous souhaitez recevoir les notifications, le paramètre se situe dans l'interface graphique de Nextcloud dans l'onglet `Informations personnelles` puis `E-Mail`.
    
Résultat : 

``` php
<?php
$CONFIG = array (
  'datadirectory' => '/data',
  'instanceid' => 'ocnsucaxnfrp',
  'passwordsalt' => 'eC+62u0sczgVmBejLemCdl0A3QibMl',
  'secret' => '4aLsJ4VjvJQmpYhUPLvCySZLDQM6hx2H3AJRxNdDmGVmzXve',
  'trusted_domains' => 
  array (
    0 => '192.168.1.15:450',
  ),
  'dbtype' => 'mysql',
  'version' => '33.0.0.16',
  'overwrite.cli.url' => 'https://192.168.1.15:450',
  'dbname' => 'nextcloud',
  'dbhost' => 'nextclouddb',
  'dbtableprefix' => 'oc_',
  'mysql.utf8mb4' => true,
  'dbuser' => 'oc_oc_admin',
  'dbpassword' => 's[d7%9n7qs,~8iMHdJ6;Nx<!f[rT*P',
  'installed' => true,
  'maintenance' => false,
  'maintenance_window_start' => 1,
  'filesystem_check_changes' => 1,
  'default_phone_region' => 'FR',
  'mail_smtpmode' => 'smtp',
  'mail_sendmailmode' => 'smtp',
  'mail_smtphost' => 'smtp.gmail.com',
  'mail_smtpsecure' => 'ssl',
  'mail_smtpport' => '465',
  'mail_from_address' => 'exempleSMTP',
  'mail_domain' => 'gmail.com',
  'mail_smtptimeout' => 30,
  'mail_smtpauth' => true,
  'mail_smtpname' => 'exempleSMTP@gmail.com',
  'mail_smtppassword' => 'mot_de_passe',
);
```

## 2 - Optimisation de la base de données
Navigez dans vers votre fichier de configuration `/home/docker/appdata/nextclouddb/config/`
<div style="page-break-after: always;"></div>

Puis ouvrez le fichier `custom.cnf` et remplacer avec ces valeurs :

``` php
innodb_buffer_pool_size = 512M
innodb_log_buffer_size  = 32M
innodb_flush_log_at_trx_commit = 2
```

## Sources

- <a href="https://docs.nextcloud.com/server/stable/admin_manual/contents.html" target="_blank" rel="noopener noreferrer">documentation Nextcloud</a>

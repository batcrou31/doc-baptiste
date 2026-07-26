---
icon: fontawesome/brands/windows
hide:
  - footer
---

# Windows 10/11

## Divers

### Désinstaller Edge
Naviguez vers le vôtre dossier de Microsoft Edge :
!!! warning "Attention"
    Attention, la version de Edge ne sera probablement pas la même mais le plus important est de localiser le fichier __setup.exe__
```
cd C:\Program Files (x86)\Microsoft\Edge\Application\87.x.xxx.xx\Installer
```
Ou selon votre version :
```
cd C:\Program Files (x86)\Microsoft\Edge\Application\87.x.xxx.xx
```
puis, entrez la commande suivante : 
```
setup.exe -uninstall -system-level -verbose-logging -force-uninstall
```

### Bloquez les mises à jour

Création du fichier __DesactiverMAJ.reg__ :

``` r
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\WindowsMediaPlayer]
"DisableAutoUpdate"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate]
"WUServer"="http://wsus.bat.local:8530"
"WUStatusServer"="http://wsus.bat.local:8530"
"UpdateServiceUrlAlternate"=""

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU]
"IncludeRecommendedUpdates"=dword:00000000
"NoAutoUpdate"=dword:00000000
"AUOptions"=dword:00000004
"ScheduledInstallDay"=dword:00000000
"ScheduledInstallTime"=dword:0000000c
"ScheduledInstallFirstWeek"=dword:00000001
"UseWUServer"=dword:00000001
```



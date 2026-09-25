---
icon: simple/keepassxc
created: 2026-09-12
modified: 2026-09-12
hide:
  - footer
---

# KeePassXC
:material-calendar-blank: __23/09/2026__ - :material-note: _Tuto réalisé avec KeePassXC version 2.7.12_
## 1 - Présentation

<a href="https://keepassxc.org/" target="_blank" rel="noopener noreferrer">KeePassXC :fontawesome-solid-arrow-up-right-from-square:</a> est un gestionnaire de mots de passe gratuit et open source qui permet de stocker en toute sécurité vos identifiants, mots de passe et informations sensibles dans une base de données chiffrée.

## 2 - Installation

Lien de téléchargement de KeePassXC : <a href="https://keepassxc.org/download/" target="_blank" rel="noopener noreferrer">:fontawesome-solid-arrow-right: keepassxc.org/download/</a>

Pour commancer, il faut sélectionner __Next__ :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-01.PNG){ width="600" }
</figure>

Cochez la case à gauche pour accepter la license, puis sélectionner une fois de plus __Next__ :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-02.PNG){ width="600" }
</figure>

Cochez la case __Create a shortcut on the desktop__ si vous souhaitez créer un raccourci sur le bureau :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-03.PNG){ width="600" }
</figure>

Pour finir sélectionner __Install__ afin d'installer l'application :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-04.PNG){ width="600" }
</figure>

??? warning "Erreur MSVCP140.dll"

    Si au lancement de KeePassXC, l'erreur suivante apparaît à l'écran :
   
    <figure markdown="span">
     ![Image title](../assets/reseau/keepass/KP-05.PNG){ width="350" }
    </figure>

    Il faut installer le package suivant : <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-c-v14-redistributable" target="_blank" rel="noopener noreferrer">:fontawesome-solid-arrow-right: learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist</a>


## 3 - Configuration

### Création d'une base de données

Après avoir démarrer KeePassXC, sur l'écran d'acceuil, sélectionner __Créer une base de données__ :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-06.PNG){ width="700" }
</figure>

Ensuite, donnez lui un nom : (ex : Mots_de_passe_Baptiste)

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-07.PNG){ width="700" }
</figure>

Pour le chiffremment de la base de données, laisser par défaut et sélectionnez __Continuer__ :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-08.PNG){ width="700" }
</figure>

Maintenant, saisissez un mots de passe __trés fort__ :

??? note "Recommandation"

    Vous pouvez tester la solidité de votre mot de passe sur le site suivant : <a href="https://www.security.org/how-secure-is-my-password/" target="_blank" rel="noopener noreferrer">:fontawesome-solid-arrow-right: security.org/how-secure-is-my-password/</a>
    <figure markdown="span">
      ![Image title](../assets/reseau/keepass/PASS-01.PNG){ width="550" }
    </figure>
    
<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-09.PNG){ width="700" }
</figure>

### Paramétrage de KeePassXC

Sélectionner l'engrenage situé à droite dans le panneau horizontal : 

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-14.PNG){ width="800" }
</figure>

Dans l'onglet __Géneral__ : 

<div style="page-break-after: always;"></div>

Cochez les éléments suivants : 

- __Cacher la fenêtre lors de la copie dans le presse-papier__ 
- __Réduire__ 

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-10.PNG){ width="700" }
</figure>

Cochez également : 

- __Réduire au lieu de fermer l'appli__ 
- __Afficher une icône dans la zone de notification__ et sélectionner __Multicolore__

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-11.PNG){ width="700" }
</figure>

Dans l'onglet __Sécurité__ : 

<div style="page-break-after: always;"></div>

Cochez/décochez les éléments suivants :

- __Vider le presse-papiers après 30 s__
- __Verrouiller les bases de données après une inactivité de 900 s__
- __Utiliser le service DuckDuckGo pour télécharger les icones de sites web__

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-12.PNG){ width="800" }
</figure>

Dans l'onglet __Intégration aux navigateurs__ : 

<div style="page-break-after: always;"></div>

Cochez les éléments suivants :

- __Activer l'intégration aux navigateurs__
- __Chrome, Vivaldi, Brave, Chromium__ (sélectionner le ou les navigateurs de votre choix)

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-13.PNG){ width="800" }
</figure>

## 4 - Création d'une entrée

Sélectionner le symbole __+__ à côté du cadenas dans le panneau horizontal :

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-14.PNG){ width="800" }
</figure>

Maintenant donner __un titre__ à cette entrée _(ex. Crédit Agricole, Steam, l'équipe etc...)_ anisi que votre __nom d'utilisateur/Mail__.

<div style="page-break-after: always;"></div>

Pour génerer un mot de passe, il faut sélectionner le __symbole du dé__. 

<figure markdown="span">
  ![Image title](../assets/reseau/keepass/KP-15.PNG){ width="750" }
</figure>
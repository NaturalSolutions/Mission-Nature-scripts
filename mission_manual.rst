====================
Générer les missions
====================
Copiez et renommez le fichier missions.csv.tpl en missions.csv.
Copiez et renommez le fichier taxons.csv.tpl en taxons.csv.

Remplissez le fichier des missions missions.csv et le fichier des taxons correspondants taxons.csv, en référant aux informations ci-dessous :
::

    missions.csv : Contient les informations relatives à chaque mission : 
        - id : Sert à trouver telle ou telle mission (utilisé dans le code)
        - numéro de la mission : Idem
        - titre : Titre de la mission
        - plural  (laisser 0) : Laisser 0 (utilisé dans le code)
        - difficulté : Difficulté de la mission de 0 (débutant), à 2 (très difficile)
        - saison (mois) : Période en mois (02-09) durant laquelle la mission est susceptible d'être accomplie
        - texte d'introduction : Zone de texte destinée à introduire la mission en quelques mots
        - id des taxons : Id des taxons présents dans la mission, séparés par une virgule (1,2,3)

    taxons.csv : Contient les informations relatives à chaque taxon :
        - id :  Sert à trouver tel ou tel taxon (utilisé dans le code)
        - cd_nom : Numéro INPN de l'espèce
        - title : Nom de l'espèce
        - family : Famille de l'espèce
        - url : Lien vers la fiche INPN de l’espèce
        - description : Description de l'espèce
        - characteristic : Caractéristiques de l'espèce (onglet "Comment l'identifier")
        - environment : Milieu au sein duquel l'espèce peut être aperçue (pour l'instant simplement en format texte (ex : "Villages"), probablement une correspondance chiffre - milieu plus tard (1 = Zones humides, 2 = Villes / villages, etc ...)
        - environment_description :  Zone de texte pour apporter des précisions quant au milieu
        - not_confuse : Zone de texte pour éviter de confondre les espèces entre elles
        - sources

Une fois les fichiers csv remplis, placez-les dans le même dossier que le script mission_tojson.php
Lancez le script dans votre terminal :
::

    php mission_tojson.php

Le fichier "missions.json" est créé dans le dossier où se trouve le script et le csv.

PLacez le fichier "missions.json" dans le dossier :
::

    www/data


===============================
Transformer les fichiers cities
===============================

Utiliser un outil sur le web pour passer le fichier csv en json (exemple : https://www.csvjson.com/csv2json)
Placez- le fichier dans le même dossier que le script mission_tojson.php

PLacez le fichier "cities.json" dans le dossier :
::

    www/data


Attention pour le fichier cities, il est lié à un fichier d'indexation "cities_index.json".
Il n'y a pas de script pour le générer pour le moment.


Images
======

Images requises
---------------
- thumb (images miniatures) : 256x256 pixels, format carré
- poster (images grandes formats) : environ 900 px de large, format paysage 4/3

Nom des images
---------------
Missions

Les images des missions, poster et thumb, sont nommées à partir de l'identifinat de la mission.

::

    Exemple pour la mission 1, l'image de présentation de cette mission sera : 01.jpg (Attention l'extension de fichier est en minuscule)
   


Taxons
Les images des taxons, poster et thumb, sont nommées à partir de l'identifiant de la mission.

::

    Exemple pour le taxon 1, l'image de présentation de ce taxon sera : 01.jpg (Attention l'extension de fichier doir être en minuscule)
   

Emplacement des images
----------------------
Mission
::

    www/images/mission_taxon/mission (/poster ou /thumb)

Taxons
::

    www/images/mission_taxon/taxon (/poster ou /thumb)



Générer les images
------------------

Exemple en ligne de commande avec la bibliothèque Image Magic

.. NOTE::

    Eviter les noms de fichiers avec espaces et accents. 
    Eviter les extensions de fichiers en capitale, ex JPG et jpg


- Créez un dossier "photos" et un dossier "photos-thumb"
- Placez les images à recadrer dans le dossier "photos"
- Placez-vous dans le dossier "photos"

::

    mogrify -path ../photos_thumb/ -thumbnail 256x256^ -gravity center -extent 256x256 *.jpg


Pour les grandes photos, créer un dossier photos_full
::

    mogrify -path ../photos_full/ -resize 900x900 *.jpg


Pour les photos dans les csv, créer un dossier photos_csv (par exemple)
::

    mogrify -path ../photos_csv/ -resize 700x700 *.jpg



Afficher des images dans les textes
===================================

- Ajouter les images dans le dossier www/data/image_source/
- Ajouter ces balises HTML dans le champ texte du csv :
::

    <figure><img class='img-thumbnail mx-auto d-block' src='data/image_source/01.jpg' /><figcaption>Fig.1 - Trulli, Puglia, Italy.</figcaption></figure>

Avec les crédits photographiques associés :
::

    <figure><img class='img-thumbnail mx-auto d-block' src='data\/image_source\/01_2.jpg'><div class='credits'>Mon crédit<\/div><figcaption>Nid ouvert de l'Hirondelle rustique<\/figcaption><\/figure>

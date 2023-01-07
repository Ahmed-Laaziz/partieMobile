## Ensaj-Monument

Ensaj-Monument est une application itinérante qui permet aux utilisateurs de rechercher dans leur voisinage afin de découvrir les points de repère les plus proches et les plus populaires.

### Principaux concepts théoriques :
-  Architecture propre
-  Programmation réactive
-  Modèles architecturaux (MVVM)
-  Développement Android

### Spécification

#### Aperçu

Ensaj-Monument est une application touristique implémentée pour Android créée dans le but de démontrer la manière dont les différents concepts architecturaux et
modèles de conception d'application peuvent être appliqués dans une pratique. L'objectif de cette documentation est d'entrer dans les détails du processus de développement et de l'architecture de l'application, en montrant comment les concepts théoriques ci-dessus ont été utilisés comme principes directeurs de l'application.
#### But

Le but de cette application est de fournir aux utilisateurs un moyen de découvrir les
monuments tout en explorant de nouvelles villes en étant averti lorsque vous êtes à proximité de
un tel point de repère. Lorsqu'ils sont avertis, ils doivent être invités à capturer une image de
le monument, constituant ainsi une collection de repères trouvés au fil du temps.
Ainsi, la principale incitation de l'application est d'inciter ses utilisateurs à se promener librement
autour et explorer les villes qu'ils visitent plutôt que de garder constamment un œil sur
leurs appareils mobiles ou cartes physiques essayant de découvrir toutes les attractions disponibles.
Après avoir configuré une session en sélectionnant la plage, le nombre maximum et le type de
points de repère qui les intéressent, l'application doit agir comme un GPS et basé sur des capteurs
boussole guidant l'utilisateur vers le monument le plus proche détecté.

En fournissant uniquement une direction générale et une distance par rapport aux balises, l'utilisateur est
libre de se déplacer et de découvrir son environnement, de pouvoir compter sur
notifications entrantes déclenchées par l'arrivée à proximité d'une telle balise.

<!-- #### Definitions

-   Beacon : Geographic location represented by its coordinates in the Geographic coordinate system specified as a pair of latitude and longitude values.
-   Geo-fence : A circular region set up around a beacon with its size given as the radius
starting from the center point i.e. the coordinates of the beacon. -->

#### Exigences fonctionnelles

- L'utilisateur doit pouvoir créer un compte avec une combinaison d'adresse e-mail
    et un mot de passe.
- Les utilisateurs doivent pouvoir s'authentifier avec leur e-mail créé et
    comptes de mots de passe ou via des fournisseurs tiers tels que des comptes Google ou Facebook.
- L'utilisateur doit pouvoir créer des sessions d'exploration après avoir été localisé par le
    application et en précisant les détails souhaités tels que le rayon de recherche, la limite imposée au nombre de points de repère à trouver, ainsi que les catégories préférées.
    Après avoir recherché des points d'intérêt sur la base des critères ci-dessus, l'application
    doit présenter le nombre de repères découverts. L'utilisateur doit alors avoir le
    possibilité de démarrer la session ou d'ajuster les critères de recherche. Après le démarrage d'une session, le
    les informations pertinentes doivent être enregistrées sur le cloud et mises en cache localement sur l'appareil par l'application, de sorte qu'elles ne dépendent plus de l'accès à Internet pour les besoins de base
    opérations.
- L'utilisateur peut sauvegarder sa progression de session active à tout moment pour synchroniser son
    données mises en cache localement avec la base de données cloud.
- L'utilisateur peut finaliser une session prématurément, à laquelle l'application doit réagir
    en poussant la session enregistrée et les informations de point de repère vers la base de données cloud
    et effacer le cache local.


- Après déconnexion de l'application, toute session active démarrée par l'utilisateur est suspendue, lui permettant de la reprendre après reconnexion.
- L'application doit fournir des moyens pour reprendre, terminer et synchroniser
    leur session active sauvegardée sur le cloud sur n'importe quel appareil connecté.
- Lorsqu'il y a une session active, l'application doit fournir un mécanisme pour guider l'utilisateur vers la balise installée la plus proche en indiquant la direction générale et la distance de celle-ci.
- Lorsqu'il y a une session active et que l'appareil de l'utilisateur entre dans la zone d'une barrière géographique
    mis en place autour d'une des balises de la session, l'application doit avertir l'utilisateur et
    invitez-le à prendre une photo du point de repère représenté par la balise. Cette
    doit être effectuée via une notification système guidant automatiquement l'utilisateur vers
    l'écran approprié à l'ouverture de la notification.
- L'application doit fournir un mécanisme pour capturer une image via le système
    caméra ainsi qu'une option pour les utilisateurs d'enregistrer leurs images localement dans le système
    répertoire partagé.
- Après la capture d'une image, l'application doit pouvoir traiter, reconnaître et
    étiqueter le point de repère, invitant l'utilisateur à répéter l'opération avec une nouvelle image
    si le processus de reconnaissance ne parvient pas à identifier le point de repère donné. Si la reconnaissance
    le processus réussit, l'application doit mettre en cache l'image et l'heure de la découverte
    localement.
- Après la découverte du point de repère, l'application doit mettre en file d'attente le processus de téléchargement du
    image respective au stockage en nuage.
- Les utilisateurs doivent pouvoir visualiser leurs sessions terminées et leurs points de repère découverts ainsi que leurs images respectives sur n'importe quel appareil connecté.

#### Exigences non fonctionnelles


*Exigences d'utilisabilité*

- L'application doit fournir des indications claires relatives à son utilisation et des messages d'erreur compréhensibles en cas de pannes inattendues.


- L'application doit être conçue avec la prise en charge de l'accessibilité activée par le système
    fonctionnalités telles que les lecteurs d'écran.
- L'application doit suivre un langage de conception cohérent en termes de polices,
    taille du texte, images et jeu de couleurs.
- L'interface utilisateur doit fournir des notifications visuelles en cas de longue durée
    mais des tâches d'arrière-plan requises et ne permettent pas à l'utilisateur d'interférer avec elles.

*Exigences de fiabilité*

- L'application doit prendre en charge plusieurs sessions utilisateur indépendantes sur le même
    appareil sans qu'ils s'influencent mutuellement.
- L'application doit suivre l'emplacement de l'appareil et envoyer des notifications uniquement pour
    l'utilisateur actuellement connecté avec une session active créée.
- Les données stockées localement doivent être cohérentes sur plusieurs appareils avec
    les données ont persisté sur la base de données cloud.
- L'application doit être capable de gérer les changements environnementaux tels que les changements
    dans l'orientation de l'écran, la batterie faible de l'appareil ou les changements de préférences à l'échelle du système.


*Exigences de performances*

- Une fois qu'une session a été créée, l'utilisateur doit pouvoir la reprendre sans
    toute connectivité réseau active. Les mécanismes de navigation devraient également être
    fonctionnel avec un accès GPS seul.
- Pendant la navigation de session active, l'application doit recevoir des mises à jour de localisation fréquentes afin de fournir les directions les plus précises possibles.
- Les mécanismes de navigation reposant sur les lectures des capteurs de l'appareil tels que les accéléromètres ou les capteurs de champ géomagnétique doivent fonctionner de manière cohérente à partir de n'importe quel point de
    le globe sans être décalibré par les champs géomagnétiques.
- Les événements déclencheurs de géo-clôture doivent être déclenchés au plus tard 20 secondes après l'entrée dans le rayon spécifié.
- L'application doit utiliser un trafic réseau minimal, en utilisant le stockage local et
    mécanismes de mise en cache dans la mesure du possible.
- L'interface utilisateur ne doit jamais être bloquée en raison d'opérations de longue durée telles que
    comme des requêtes réseau ou des actions de lecture/écriture de base de données, mais fournissent des repères visuels de
    leur présence.

*Exigences de prise en charge*

- Les fonctionnalités indépendantes du système doivent être modifiables avec des changements minimes
    à la base de code et sans interférer avec celles qui ne sont pas liées.
- La candidature doit fournir un moyen concis et général de mise en œuvre
    nouvelles fonctionnalités.
- L'application doit être utilisable de la même manière sur n'importe quel téléphone ou
    modèle de tablette fonctionnant sur un niveau d'API Android d'au moins 24.
- L'application doit enregistrer et suivre les erreurs survenues et ne collecter que les
    données pertinentes au contexte de la faute et uniquement de son propre point de vue.
    
    
#### Conception UML

Voici la conception UML de notre application
*4.1* Diagramme de cas d'utilisation  | *4.2* Diagramme de classe 
:------------:|:---------------:|:----------------:
![Imgur](https://imgur.com/lPdVXvE)  |  ![Imgur](https://imgur.com/oa6v6jw) 

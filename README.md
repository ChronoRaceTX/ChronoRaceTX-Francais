OpenTX 2.2 

Pour installer Open TX 2.2, WE ARE FPV a publié une excellente vidéo
https://www.wearefpv.fr/tutoriel-taranis-flash-opentx-script-lua-20170412/
Avec lua et luac cochés

L’option « Luac » donne la capacité à votre radio de compiler les scripts pour optimiser la mémoire. Cela permet de faire cohabiter plusieurs scripts de télémétrie sur un même modèle. 


Une fois ceci fait, vous devrez télécharger le firmware correspondant 


puis flasher à nouveau votre radio
 

RECEPTEUR – TELEMETRIE ou pas ?

Le script se base sur la force du signal RSSI pour valider le passage du point de chronométrage, cela suppose que la radio puisse recevoir cette information. Tous les RX n’ont pas cette capacité. Chez FrSky, le D4R II, le XSR, le X4R et d’autres l’ont,  en revanche les XM, XM+ ne l’ont pas, bien qu’il soit possible d’avoir cette info sur un OSD, cela reste sur la machine et en aucun cas n’est accessible sur la radio (sauf astuce que l’on ne connaitrait pas, mais on a cherché.. sans succès ! ). 

A défaut de retour télémétrique du RX vers la radio, vous pourrez malgré tout utiliser le chrono en validant  votre tour manuellement avec un inter. L’inter SH est le plus approprié puisqu’à retour. A priori … c’est [juste ] un coup de main à prendre !

DECOUVERTE DES CAPTEURS

Si ce sont vos premiers pas dans le monde merveilleux de TARANIS, vous n’aurez peut-être pas franchi cette étape qui consiste à ce que la radio puisse « lire » les  capteurs de télémétrie. 
Depuis la liste des modèles, sur le modèle à paramétrer, 
Appui long sur [Page]
Faire défiler les pages jusqu’à « Télémesures » (en principe la 13)
Descendre sur « Découvrir les capteurs »
Allumer le quad et lancer la découverte



INSTALLATION : 

Sur la SD card de votre radio :
   a. "CHRace.lua" à déposer dans "\SCRIPTS\TELEMETRY\"
   b. "race.lua", "config.lua" et "tools.lua" à déposer dans "\SCRIPTS\CHRace\"
   c. "Cstart.wav", "Cfin.wav" ,"Cbest.wav", Cpilot.wav et "CtopCD.wav" à déposer dans "\SOUNDS\fr"

 [Optionnel]  Créez  votre propre fichier "Cpilot.wav" pour que la radio puisse prononcer votre nom de pilote au franchissement de la ligne et informer vos concurrents de votre passage. 
Pour créer un fichier son pour les Taranis, il ya plusieurs étapes et plusieurs façons de faire, voici quelques liens sur le sujet
http://www.open-tx.org/2014/03/15/opentx-speaker
http://frskytaranis.forumactif.org/t2664-tutocreer-ses-annonces-vocales-avec-opentx-speaker-windows-only
http://cassoulet-soaring.blogspot.fr/2014/09/tuto-son-demarrage-taranis.html

Premiere execution sur la radio

Vos fichier « lua » doivent être compilés par la radio afin qu’ils tiennent moins de place en mémoire, celle-ci étant très limitée pour vos scripts de télémétrie (de l’ordre de 70Ko), vous ne pourrez faire cohabiter le script « Chrono Race » avec ceux pour les PIDS Bétaflight ou Kiss que s’ils sont tous compilés.

Allez dans la SD Card, depuis la page du modèle
Appui long sur [Menu]
Appui sur [Page]
Descendre sur « SCRIPTS » puis [ENT]
Puis « TELEMETRY » puis [ENT]
Puis « CHRace.lua » puis [ENT] long et « Executer »
Appuyez sur [Menu] pour aller dans les pages de configuration de « CHRace »
le script CHRace est composé de plusieurs fichiers chargés en fonction des besoins afin d’optimiser la mémoire, en allant sur [menu] la radio compilera aussi les pages de configurations.

Faire de même pour BF ou Kiss si aucun « luac »
Eteindre et Rallumer la radio.



configuration
1. écran de télémesure
Liez le script « CHRace » à un écran de télémesure, depuis la liste des modèles, sur le modèle auquel associé le script
Appui long sur [Page]
Faites défiler les pages jusqu’à celles des écrans de télémesure 
Editez l’écran de votre choix pour y associer le script « CHRace »


2. inter logique
La détection du franchissement du seuil RSSI se fait grâce à un inter logique. Le rôle de cet inter est de permettre au script de savoir si on est au-dessus du seuil ou non (en l’occurrence il agit comme un inter physique à deux états, On ou Off)

La page des inters est accessible de la même manière que les écrans de télémesure, page 10


  * Fonction : a>x
  * V1       : RSSI
  * V2       : 74db (sera écrasé par le paramètre Seuil + et les ajustements dynamiques) 
3. config DES INTERS 
Une fois définit l’inter logique (L03 sur l’écran précédent) lancez le script « CHRace » et appuyez sur [menu] une première fois pour accéder aux écrans de paramétrages, faites les défiler jusqu’à « CONFIG INTERS » et 
	- renseignez l'inter logique du RSSI
	- ajustez les autres paramètres si nécessaire (voyez leur description plus bas dans ce document)



Certains RX sont unidirectionnels (comme le XM+), aucun signal n’est renvoyé à la radio. Pour ceux-ci la validation RSSI ne sera pas possible. Vous serez obligé de valider manuellement vos tours à l’aide du switch poussoir « SH » (ou « SD » comme sur la copie écran ci-dessus).
UTILISATION
LANCEMENT 
Appui long sur "Page" pour appeler les écrans de télémétrie
Appui court sur "Page" pour faire défiler les écrans de télémétrie jusqu'à celui du chrono (si vous n'y êtes pas déjà)
 PARAMETRAGE (L'ensemble des paramètres est décrit plus bas) 
Depuis l'écran "Chronomètre ..."
Appui court sur "Menu" pour les paramètres propres aux sons
Appui court sur "Menu" pour les paramètres propres à la course (Nb de tours, Délai entre 2 validations, Seuil de décollage, Mode de départ) 
Appui court sur "Menu" pour les paramètres propres à votre radio (Inters d'armement, de validation manuelle ou logique (RSSI)  ...)
Appui court sur "Exit" pour revenir à l'écran de chrono

TEST & REGLAGES 
En théorie, la validation du tour par RSSI, c'est beau !
Sur le terrain, ça l'est un peu moins, vous devrez étudier un peu l'aire de jeu avant et si vous pouvez choisir vos emplacements de pilotage et de validation ce sera encore mieux ! 

Il va vous falloir régler deux paramètres pour pouvoir en profiter : 
- le seuil RSSI de déclenchement 
- le délai de validation entre deux tours

Le mode test fait sonner la radio tant que la force du signal [RSSI] est au-dessus du seuil réglé.
Aidez vous de ce mode pour ajuster votre seuil (touches [+] ou [-] (X9D) ou la molette (QX7) ).
Si un point intermédiaire du circuit sonne, vous pourrez le "gommer" avec le "délai". Ce paramètre ne permet la validation d'un tour qu'une fois ce délai écoulé, et ce, à chaque tour. 
Plus vous serez régulier et plus le "délai" sera efficace, puisque en mettant le "délai" un peu en dessous de votre meilleur temps, la "fenêtre de validation RSSI" (sens figuré) n'agira qu'un peu avant la fin du tour jusqu'à sa validation.

- Le mode test est engagé par un inter configurable dans les paramètres (choix de l'inter et position)
- Le délai est paramétrable dans l'écran de configuration "Race"
- Le seuil RSSI est réglable dans les paramètres ET en dynamique par [+] ou [-] (X9D) ou la molette (QX7) dans certaines conditions (mode TEST, Avant course)

AVANT COURSE
Le seuil RSSI reste réglable par [+] ou [-] (X9D) ou la molette (QX7)

COURSE
Armez, décollez, faites le circuit
Eventuellement revenez sur le délai de validation (voir DELAI dans les paramètres)
Le seuil RSSI reste réglable par [+] ou [-] (X9D) ou la molette (QX7)

APRES COURSE
Si vous avez paramétré un nombre de tours supérieur à 4, une fois désarmé, vous pouvez naviguer dans le tableau des temps avec la molette (QX7) ou les touches "+" et "-" (X9D)
Le seuil RSSI n'est plus réglable par [+] ou [-] (X9D) ou la molette (QX7) tant que vous n'aurez pas RAZ le tableau des temps
Utilisez l'inter de Reset pour remettre le chrono et les temps à zéro

Précautions d’emploi
Bien que cela ne soit pas possible, et en dehors de la stupidité de cette éventualité, il est tout de même déconseillé de mettre le script au micro-onde ou à la machine à laver (la vaisselle aussi bien que le linge). Aucun d’entre nous n’a essayé, cela ne nous étant pas venu à l’idée.

PARAMETRES
D'une manière générale, vous vous déplacez sur les différents paramètres avec les touches "+" et "-" de la radio (ou de la molette pour la QX7)
Pour éditer le paramètre appuyez sur la touche [ENT]
Le script s'adapte en fonction de ce qu'il y a renseigné : 
- soit qu'il faille manipuler un inter pour le détecter ou pour lire sa valeur (et dans ce cas il vous le dit)
- soit qu'il faille user des "+" et "-" (ou la molette sur la QX7) pour ajuster vote choix (pas d'indication contrairement au cas précédent)

Les paramètres sont répartis sur 3 écrans 
CONFIG SON

Nous avons utilisé le potentiel "vocal" de la radio, a tel point qu'il commence à y avoir pas mal d'annonces et cela peut être gênant si elles sont toutes activées.
Vous pouvez choisir d'activer celles qui vous conviendront selon vos envies ou le contexte.

Mode	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
3 options : 

Solo
  la radio émet "départ" lorsque le chrono se met en route (voir "Départ arrêté ou lancé")

A plusieurs
  > annonce le nom du pilote lorsqu'il franchit la ligne

Starter (celui qui donne le départ pour tout le monde)
  > joue la séquence de bips pour donner le départ 
  > annonce le nom du pilote lorsqu'il franchit la ligne

Pour que la radio puisse donner votre nom, vous devez créer un fichier "Cpilot.wav" compatible avec la radio et le placer dans "SOUNDS/fr/".
Le fichier des bips de départ nous a été fourni par ChronoDrone, vous reconnaitrez leurs bips, merci Adrien !

Pseudo	[ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Oui   Non
En mode "A plusieurs" ou "Starter", le choix "non" permet d'inhiber l'annonce de votre nom au franchissement de la ligne

Num Tour	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Oui   Non
Dans tous les modes, annonce du n° du tour effectué au franchissement de la ligne

Temps	[ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Oui   Non
Dans tous les modes, annonce du temps effectué au franchissement de la ligne

Best	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Oui   Non
Dans tous les modes, dès que votre temps est meilleur que les précédents, la radio annonce "Meilleur tour" au franchissement de la ligne

CONFIG RACE

NB tours	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Il s'agit bien entendu du nombre de tours que vous souhaitez chronométrétiser. Oui je sais ce n'est pas français, mais faut bien meubler un peu, car qui aurait imaginé qu'il puisse s'agir d'autre chose ?

DELAI (de validation entre deux tours)	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
En paramétrant un délai un peu en dessous du meilleur temps dont vous êtes capable, cela permet d'éviter d'avoir un déclenchement RSSI intempestif à un point intermédiaire du circuit. En effet, comme la force du signal RSSi peut être au seuil à plusieurs endroits, selon votre altitude, l'humidité dans l'air, le sens du vent, ou encore la manière dont vous tenez votre radio ... et compte tenu qu'on a pas intérêt à canaliser ce signal, fallait bien essayer qq chose ! Donc vous n'avez pas le choix, soyez régulier dans vos tours !!!  

SEUIL RSSI	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Valeur au delà de laquelle l'inter logique du RSSI provoquera la validation du tour.
Vous pouvez ajuster le seuil dans les écrans de config, mais aussi en dynamique, il n'y a que lorsqu'il y a des temps à consulter que le molette ou les touches [+] et [-] ne modifient pas le seuil. 

Désactiver la validation RSSI : montez le seuil à 100 => "Off" est affiché sur les écrans de race et de config pour signifier la désactivation. 

SEUIL GAZ (ou seuil de décollage)	[ENT] puis levez le manche jusqu'à la position où le décollage est valide puis [ENT]
Le Chrono a besoin de savoir quand vous décollez, soit pour être déclenché, soit pour attendre le premier passage au point de validation (voir les Modes de départ) 
"-500" paraît être une bonne valeur, dès que vous êtes au premier quart de la course du manche, le script considère que vous avez décollé.

MODES de DEPART	 [ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Départ lancé ou arrêté, le chrono démarre 
* arrêté = dès que le manche des gaz est levé 
* lancé  = dès que vous franchissez une première fois le point de validation, des bips signalent l'attente du point de passage

CONFIG INTERS

ARMEMENT (inter d')	[ENT] puis actionnez l'inter d'armement, il est aussitôt pris en compte
Il s'agit de l'inter avec lequel vous armez le quad. Selon les habitudes des uns et des autres, des radios, il était souhaitable que vous puissiez le choisir.

OFF (ARMEMENT)	 [ENT] puis positionnez l'inter en mode désarmé puis [ENT]
La plupart du temps cette valeur est "-1024" mais selon la configuration de votre radio, si l'inter est à 3 ou 2 positions ... bref, le mieux est d'éditer le paramètre de mettre l'inter dans sa position "Off" et de refaire [ENT] pour que le paramètre capture cette valeur 

VALID TOUR (Inter de)	 [ENT] puis actionnez l'inter de validation manuelle du tour, il est aussitôt pris en compte 
Généralement "SH" sur la X9D et la QX7 car c'est le seul inter à retour.
Si vous êtes assez doué et précis, vous pourrez valider vos temps grâce à lui.
Mais comme on est bpc à n'être pas bon à ce point, on a essayé de faire un truc avec le RSSI  

RSSI (Inter logique de détection du)	[ENT] puis molette (QX7) ou touche +/- (X9D) puis [ENT]
Au point "3" de l'installation, nous vous présentions les paramètres de réglages d'un inter logique sur la force du signal RSSI.
Vous devez reporter le nom de cet inter logique dans ce paramètre.

RESET (Inter de RAZ des temps)	[ENT] puis actionnez l'inter de RAZ des compteurs, il est aussitôt pris en compte 
Beaucoup mettront le "SH" pour la remise à zéro avant une nouvelle course, il n'agira que lorsque vous êtes désarmé, donc pas de risque de RAZ pendant une course.
Mais, si comme moi, votre "SH" vous sert aussi à déclamer le voltage de votre lipo, alors vous apprécierez de pouvoir mettre le RAZ sur un autre inter. 

ON (RESET) position RAZ	[ENT] puis positionnez l'inter en mode RAZ puis [ENT]
Pour convenir à chaque cas, définissez ici à quelle valeur de cet inter la RAZ doit être effectuée 

TEST (Inter de mise en route du mode TEST)	[ENT] puis actionnez l'inter de mode TEST, il est aussitôt pris en compte 
Cet inter vous permet d'enclencher le mode test pour ajuster le seuil de détection du RSSI. Des fois que vous ayez un sbire à envoyer sur le terrain pour tester le quad en main ... c’est inutile !!! ça marche aussi en vol :P 
Vous pouvez même faire la course en mode Test (woua, ça, ça n'était pas prévu, mais après tout ...)

ON (TEST)  déclenchement du mode TEST	[ENT] puis positionnez l'inter en mode RAZ puis [ENT]
Une fois choisi l'inter, définissez dans quelle position il doit déclencher le mode test. Bien entendu, le mode TEST s'arrêtera dès que l'inter ne sera plus dans cette position. 
On enfonce des portes ouvertes, mais au moins ça à le mérite d'être clair.
BUGS & AMELIORATIONS

Double seuil RSSI
  Seuil haut = prise en compte lorsqu'on dépasse le seuil par le haut
  Seuil bas  = prise en compte lorsqu'on franchit le seuil par le bas
  Dire lequel valide le tour : celui qui ne valide pas doit être franchit en premier. 
Par exemple, je choisi le seuil bas comme seuil de validation
  - tant que le seuil haut n'est pas détecté, je ne peux valider le tour
  - une fois détecté, j'attends que le seuil bas soit franchit pour valider

HISTORIQUE

7.0 : Version Ok
Revisite ReadMe et diffusion
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.9 : Paramétres 
      "Top" devient "Mode" : Solo / A plusieurs / Starter
      "Pseudo"             : oui/non = annonce du pilote franchissant la ligne (Cpilot.wav)
      "Num Tour"           : oui/non = annonce du tour accompli
      "Temps"              : oui/non = annonce du temps effectué
      "Best"               : oui/non = annonce "meilleur tour" (Cbest.wav)
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.9b : Optimisation + petits bug
		Nom définitif du Script "CHRace", harmonisation des noms de fichiers 
		Pour ceux qui ont déjà installé les version précédentes :
		a/ Supprimer le répertoire "CHRONO" dans "SCRIPTS"
		b/ Supprimer le fichier "timer.lua" dans "SCRIPTS/TELEMETRY" 
		c/ Dans l'écran de "telemesure" associer le script "CHRace" et non plus "timer" 
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.9c : Bug affichage QX
	   bip d'attente validation seulement si Throttle up
	   temps vocal pouvant ne pas être identique à l'affichage (pb arrondi sur les centièmes)	
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.8 : Bug résolu : Reset ou Faux départ ne rejouaient plus le top départ (Faux départ = aucun tour n'a été chronométré au désarmement)
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.7 : Reprise "Top Départ" trois choix
      - "Off"   = fonctionnement en solo, le top départ n'est pas joué, le nom du pilot n'est pas édicté à la validation du tour
      - "mast"  = jouer le top départ + nom du pilote à la validation du tour
      - "elev"  = le nom du pilote à la validation du tour
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.5 : Validation RSSI Off : monter le seuil à 100 
                            indication visuelle "Off" sur écran race et sur écran config
      Top oui/non plutot que 1/0 + repositionnement des options
      Redessine les champs en sortie d'édtion
      Logo Chronodrone
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.4 : retouche QX7 par Dom
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.3 : splash-screen de reset : Petit bug résolu sur affichage
                               Remonté le laps d'affichage de 20 à 30 
      réactivation des textes d'info sur les pages de config
      recentrage de la ligne de titre (race.lua ligne 157 : "(i_IsX9D and 67 or 40)"" jouer sur le "40" pour centrer et me donner la valeur 
      pour que je la mette dans le source avant qu'on ne la perde ;) 
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.2 : Ecrans de Config : Petit bug résolu sur choix inter et attente position 
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.1 : Les pages sont désormais compilées elles aussi par la radio, on est maintenant full luac ! résultat, on passe de 28ko à 20ko en standby 
        sur la page du chrono
      Test divers et variés et petites retouches de code (encore un peu de mémoire à gratter sur les pics), on est stable, aucun leak
        et pics à 47Ko max sur la radio.  
      Suppression des textes d'aide sur les options de config pour grignoter un peu plus de mémoire
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
6.0 : Refonte complète pour optimisation de la gestion de la mémoire
      Le moteur ne fait que charger et décharger les modules en fonction du besoin 
      La charge mémoire est réduite au minimum lorsqu'on va sur un autre script
      Le probème est l'occupation mémoire des autres scripts qui ne laisseront plus la place au chrono
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
5.3 : Bug résolu : bascule d'un écran de config à l'autre un peu laborieux
      Vérification expansion mémoire = stable, varie entre 41 et 47 KB, 41 KB au "repos"
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
5.2 : Bug résolu sur absence du capteur RSSI, affiche "OFF" si pas de capteur 
      Parametre "Top Départ" : son à l'armement pour lancer une séquence de bip pour donner le départ aux copains
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
5.1 : Bug sur BetsLap : ne prenait que les 4 premiers tous
	  Affichage "RESET" en gros sur tout l'écran ... si pas "SH" trop béta de laisser l'inter en position "RESET"	
	  nommenclature des variables pour les fichiers sons revue "snd_xxxxxxx", "sfile" renommé en "snd_start" 
	  Son quand meilleur temps "snd_best"
	  pour éviter de reparamétrer les fichier sons à chaque nouvelle version, possibilité de les modifier dans "chrono.cfg" 
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
5.0 : Seuil RSSI : se règle désormais dans les paramètres "RACE"
				   MAIS s'ajuste aussi en dynamique 
				   - en mode TEST avec la molette (QX7) les touches "+" & "-" (X9D) + annonce vocale de la valeur de seuil
				   - avant la course, dans ce cas, ça fait juste bip plus ou moins aigu selon la valeur du seuil
				   - pendant la course, mais aller chercher les boutons vous fera certainement faire un temps minable, voire pas de temps du tout 
	  Affichage "Mode TEST" qaund l'inter est engagé
	  Consultation temps ([+][-] ou molette) : seulement quand 
	  	- désarmé
	  	- pas en mode test
	  	- qu'il y a au moins un temps dans le tableau
	  	le reste du temps, ces commandes sont dédièes au réglage du seuil

	BUG : Si on fait [EXIT] depuis un écran de config qui attend la manipuation d'un inter, alors on revient sur cet écran au retour sur la config
		 > sortir du mode Edit
		 Ok, comment je te l'ai mis kaput le bug !
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
4.8 : Paramétrage de la valeur de l'inter de Reset
	  info tours consultés
	  bip quand premier ou dernier tour atteint en consultation
	  mise en forme temps au tour non bouclés (mise en évidence des tours non courus)
	  reprise des infos paramètres (viré les accents)
	  bug affichage sur quitte écran télémétrie en cours de course 
	  bug affichage "Mode départ"
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
4.7 : rectif bug bornage "start_mode" ne peut plus prendre une valeur autre que 0 ou 1
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
4.6 : rectif bug reconaissance molette QX7 / + et - X9D
	  paramètre de config, position "On" de l'inter de Test	
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
4.5 : Naviguer dans le tableau des temps (après désarmement) avec touches + et - (ou molette sur QX7)
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
4.0 : Paramétrages persistents (fichier "/SCRIPTS/CHRONO/chrono.cfg" sur SDCard)
	  Ecrans de menu "Config Race" et "Config Inters"
	  Réglage du nombre de tours et défilement du tableau des temps durant la course
	  Délai de validations entre deux tours paramétrable en secondes
	  Cmmentaire sur les paramétrages dans le abse de l'écran
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
3.5 : Dessins d'écran adapté au type de radio (QX7/ X9D)
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
3.0 : Modes de départ, lancé ou arrêté
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
2.5 : Mode test = vérifier où le RSSI déclenche pour pouvoir ajuster le potar en vol
	  Amélioration RSSI (inter logique)
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
2.0 : Essais RSSI
	  Reglage de seuil RSSI
	  Plage de détection (abandonné par la suite)
- - - - - - - -- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1.0 : Premier jet, Table des chonos, chronos, délai ...
------------------------------------------------------------------------------------------------------------------------------------------------


VOILA VOUS SAVEZ TOUT MAINTENANT !!!!!!!

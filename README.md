# MonitoringActivite
 
Nous vous invitons à lire "rapport-MonitoringActivite.pdf" dans le dossier "rapport".
 
<b>Remarque :</b> la documentation utilisateur pour le site "Monitoring d'activité" se trouve dans le répertoire "User-Doc".
 
## 1) Machines utilisées

Voici l'ensemble des informations liées aux machines / adresses IP utilisées pour la version du projet déjà déployée dans le LaboVision.

1) Deux machines virtuelles ont été utilisées (Ubuntu 16.04, 10GB d'espace disque, 2048 Mo de RAM).
	
2) Informations concernant le site du "Monitoring d'activité" :
    -	Site hébergé sur la machine n°1
    -	Site accessible à l'adresse [<i>adresse IP machine n°1</i>]/monitoring_activite/

3) Informations concernant BDD (base de données) :
    -	BDD hébergée sur la machine n°1
    - Utilisateur créé spécifiquement pour la BDD du projet
 
4) Quatre programmes Qt ont été développés (codes sources dans le répertoire "Programmes-Qt") :
 
    - BruitLabo : détecte les anomalies sonores et envoie les données via WebSocket (port 4420)
    - EnregTV : détecte une activité de visionnage TV et envoie les données via WebSocket (port 4430)
    - DetectZone : détecte les déplacements dans le LaboVision et envoie les données via WebSocket (port 4440)
    - WSLitener : reçoie ces données WebSocket et les communiquent aux fichiers PHP du site pour l'insertion en BDD

## 2) Déploiement du projet

1) Créer une BDD MySQL avec comme nom de BDD : monitoring_activite.
 
2) Une fois connectée à la BDD, créer l'ensemble des tables grâce au fichier "BDD/monitoring_activite_bdd_init.sql" présent dans ce dossier de rendu.

3) Copier-coller le répertoire "monitoring_activite" présent dans ce dossier de rendu sur votre serveur web.
	
4) Modifier le fichier "monitoring_activite/utils/bdd_connection.php" pour modifier les constantes de connexion afin que le site accède à la BDD créée à l'étape n°1.
  
5) OPTIONNEL : connecté à la BDD, importer le fichier "BDD/INSERT-example.sql" présent dans ce dossier de rendu afin d'avoir des données à tester (penser à mettre ces données à la date du jour pour voir les informations s'afficher sur la page d'accueil du monitoring).
	
6) Si nécessaire, penser à modifier :

    - l'adresse de la caméra dans les fichiers "zonetracker.cpp" (programme DetectZone) et "tvtracker.cpp" (programme EnregTV) dans la méthode tracking().
    - l'adresse IP fournie à l'initialisation du membre "m_network" dans le constructeur du fichier "listeconfanomaliesonore.cpp" (programme BruitLabo). L'adresse IP doit être celle de la machine où se trouve le site déployé à l'étape n°4.
		- l'adresse IP fournie à l'initialisation du membre "m_network" dans le constructeur du fichier "detect.cpp" (programme WSLitener). L'adresse IP doit être celle de la machine où se trouve le site déployé à l'étape n°4.
		  
7) Compiler les 4 programmes sous Qt et les placer sur les machines désirées.

    
<b>Attention :</b> si vous déployez les programmes sur des machines différentes que celle de la verison actuellement en production, pensez à modifier le fichier "run.sh" pour le lancement du programme "WSListener" (ces adresses correspondent aux machines hébergeant les programmes. Adresses utilisées pour les communications WebSockets).

GitHub / GitLab (service hébergement de code).

Utilise Git pour pouvoir communiquer mon code avec GitHub/Lab.


Pour cloner un projet (HTTPS) : plus lent dû au fait de nécessité de taper un mdp au changement de version/repertoire.

	- Dans GitHub copier le lien HTTPS dans Code.
	- Dans le terminale se placer dans le répertoire ou l'on veut mettre le projet.
	- Ecrire git clone "le lien coller" ("nouveau nom du dossier" optionnel).

Connexion par clé SSH : permet de sécurisé la communication et ainsi pas taper de mdp tt le tps.

	- Dans le terminal depuis n'importe quel répertoire taper la commande :

		ssh-keygen : 	-t <type : rsa, ecdsa, ed25519>; 
				-b <bits : [2048, 4096], 521>; 
				-f <filename>;
 				-C <commentaire>;
				-N <passphrase>;
				-p<modif la passphrase>;
				-l<empreinte clé publique>;
				-y<genere cle publique>;
				-q <mode silencieux>;

	- Elle créer une clé privée et une publique du type choisi dans le repertoire user/moi/.ssh.
	- faire la commande cat sur la clé publique et la copier.
	- Aller dans les settings de GitHub categories SSH and GPG keys.
	- cliquer sur new SSH keys : donner un nom dans title puis coller la clé dans key.


Pour cloner un projet (SSH) :
	
	- Avoir paramétré une clé SSH au préalable.
	- Dans GitHub copier le lien SSH dans Code.
	- Dans le terminale se placer dans le répertoire ou l'on veut mettre le projet.
	- Taper git clone "le lien coller" ("nouveau nom de dossier" optionnel).



Pour push un repertoire :

	- Taper git init dans le dossier de projet concerné.
	- Taper git remote add origin "url du projet GitHub".

	- On peut faire un git status pour voir l'état actuel des fichiers.

	- Pour chaque modif par fichier faire git add "nom du ficher" (on peut enchainer les noms de fichiers pour en mettre plusieurs en une commande).
	- Pour annuler un add il faut faire un git restore --staged "nom du fichier".	

	- Puis faire la commande :

		git commit :	-m <message>;
				-a <fichier suivi : évite de faire le add>;
				-amend <modif le dernier commit>;
				--allow-empty <permet de faire un commit sans aucune modif sur le code>;
				--squash <combine des commit entre eux>;
				-v <montre ce qui sera commit>;
				--dry-run <simule l'execution du commit>;
	
	- Si on ne met pas de -m on entre dans un interface ou décrire notre commit ce qui permet d'être plus précis que seulement un titre.
	- Pour naviguer dans l'interface il faut taper i pour insérer puis echap pour en sortir et taper wq pour write et sortir de l'interface. 

	- Faire un git push origin main pour envoyer sur GitHub.


Lister les commits :
	
	- On peut taper git log (liste tous les commit qui ont été fait).
	- On peut aller sur GitHub pour avoir la liste des commits.



Fonctionnement des branches:

	- Branche main : programme principale fonctionnel, chaque commit équivaut à une nouvelle version du programme.
 
	- Branche développement : découle de main où l'on rajoute les fonctionnalités qui fonctionnent, chaque commit rajoute une fonctionnalité, une fois qu'elles sont toutes faites merge avec main.

	- Branche features : découle de dev, branche ou l'on code les fonctionnalités ou on résout un bug, une fois la fonctionnalité fonctionnel, on merge avec dev.
	
	- Branche hotfixes : découle de main qui est une branche d'urgence pour résoudre un bug de manière rapide et précise puis le renvoyer dans main et dev en même temps.



Créer des branches :

	- Commande git branch : donne liste des branches sur le projet.


	- Utilisation de la commande :

	 	git checkout :	"nom de branche" <changement de branche>;
				-b <création d'une nouvelle branche et changement>;
				-- fichier.txt <restaure un fichier au dernier commit>;
				nom_commit -- fichier.txt <restaure un fichier sur un commit spécifique>;
				nom_commit <permet de visualiser le projet depuis un certain commit mais détache de la branche actuelle ne liant pas les modifs a la branche>;
				--track <configure un suivi automatique sur une branche>;
				-f <force le changement de branche sans validé les modifs>;

	
Merge les branches :
	
	- Git utilise plusieurs stratégies de fusions: 
		- fast-forward : si la branche qui reçoit le code n'a pas été modifier depuis la création de l'autre branche, copie directement le code manquant.
		- three-way : sinon créer un commit de fusion pour combiner les changements ensemble.

	- Manière sale à utiliser pour soi-même pas en travaux de groupe:
		- On peut utiliser la commande git merge:(problème de conflit a résoudre manuellement si la même partie de code est modifié dans les deux branches)

			git merge:	"nom de branche" <fusionne la branche avec l'actuelle>;
					--no-ff <empêche la fusion en fast-forward pour obtenir un historique>;
					--squash <combine les commits de la branche qui fusionne en un seul reçu sur l'autre branche>;
					--abort <en cas de conflit annule la tentative de fusion>;
					--no-commit <empeche de commit automatiquement après la fusion>;
					-m <message>;
	
	-façon plus orthodoxe :
		- On va faire une pull request.
		- Pour se faire il faut au préalable push la branche que l'on va fusionner.
		- Une fois sur GitHub aller sur l'onglet Pull Requests 
		- On créer une nouvelle pull request et choisi la branche qui reçoit la fusion et celle fusionné
		- Ainsi un autre developper qui va review la request et peux la merge depuis GitHub.
	

Gerer les conflits :
	
	- Si il y a un conflit il faut git merge la branche qui reçoit sur celle que l'on va fusionner pour detecter le conflit.
	- Résoudre le conflit par soi-même selon le contexte.
			
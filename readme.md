### Déploiement en local du projet ###

<a href="https://github.com/enLussi/diet-coupart">Lien vers le code du projet</a>

# Cloner le projet #
cloner le projet
	git clone https://github.com/enLussi/diet-coupart.git

dupliquer le fichier .env.dist et modifier le données 
pour une connexion à une base de données local

# Composer #
Si composer est déjà installer faire
	composer install

ou installer composer au préalable

# Base de données #
Créer la base de données avec
	symfony console doctrine:database:create

ou si la commande symfony n'est pas installée
	php bin/console doctrine:database:create
php bin/console remplace symfony console


Faire les migrations de la base de données
	symfony console make:migration
	symfony console doctrine:migrations:migrate

# Fixtures #
Avant de peupler la base de données assurez-vous que les
identifiants de l'admin sont paramétrer à votre convenance

Vous pouvez éditer le fichier newAdmin.json pour paramétrer
1 SEUL admin

Les paramètres de base sont admin@admin.fr pour l'email
et admin pour le mot de passe.

Pour faire les fixtures utiliser la commande
	symfony console doctrine:fixtures:load
Créant les données de base dans la base de données
(Ingrédients, patients(basique pour les tests), régimes, allergènes, et admin)

# Compte admin supplémentaire #
Pour ajouter un SEUL compte administrateur, éditez le fichier 
newAdmin.json à la racine du projet avec les nouveaux paramètres.

Puis utiliser la commande
	symfony console doctrine:fixtures:load --group=admin --append

Qui lancera l'exécution des fixtures du group admin en les ajoutant au
données existantes dans la base de données (sans purge)






### Déploiement distant du projet ###

On considère qu'une connexion en ssh est possible vers le serveur distant
et que git y est préinstaller

# Cloner le projet #
cloner le projet
	git clone https://github.com/enLussi/diet-coupart.git

dupliquer le fichier .env.dist et modifier le données 
pour une connexion à la base de données associées au serveur

# Composer #
Installer composer s'il n'est pas préinstaller

Pour un serveur tournant sous Linux (Hébergeur Ionos)
installez composer avec la commande
	curl -sS https://getcomposer.org/installer | usr/bin/php8.1-cli

changez la version de php au besoin

Pour la première utilisation 
	/usr/bin/php8.1-cli composer.phar

Et lancez l'installation des dépendances 
	/usr/bin/php8.1-cli composer.phar install

# Base de données #

Certains hébergeur permettent de créer une base de données depuis leur
interface utilisateur. Au besoin créer la base de données avec doctrine
(comme en local) puis faites les migrations
	/usr/bin/php8.1-cli bin/console make:migration
	/usr/bin/php8.1-cli bin/console doctrine:migrations:migrate
	
# Fixtures #
Avant de peupler la base de données assurez-vous que les
identifiants de l'admin sont paramétrer à votre convenance

Vous pouvez éditer le fichier newAdmin.json pour paramétrer
1 SEUL admin

Les paramètres de base sont admin@admin.fr pour l'email
et admin pour le mot de passe.

Pour faire les fixtures utiliser la commande
	/usr/bin/php8.1-cli bin/console doctrine:fixtures:load
Créant les données de base dans la base de données
(Ingrédients, patients(basique pour les tests), régimes, allergènes, et admin)

# Compte admin supplémentaire #
Pour ajouter un SEUL compte administrateur, éditez le fichier 
newAdmin.json à la racine du projet avec les nouveaux paramètres.

Puis utiliser la commande
	/usr/bin/php8.1-cli bin/console doctrine:fixtures:load --group=admin --append

Qui lancera l'exécution des fixtures du group admin en les ajoutant au
données existantes dans la base de données (sans purge)

# Environnement #
Ne pas oublier de passer l'environnement de dev à prod

# Mis à jour #
Si des mises à jour sont à apporté et ne concernant pas la base de données ne 
pas oublier de vider le cache de symfony
	usr/bin/php8.1-cli bin/console cache:clear

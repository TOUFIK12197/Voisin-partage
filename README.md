# VoisinPartage

VoisinPartage est une application web de partage entre voisins. Elle permet de publier des objets à prêter ou à donner, de parcourir les annonces locales et d’organiser les échanges avec les autres membres.

## Fonctionnalités

- Création de compte, connexion et gestion du profil
- Publication, modification et suppression d’annonces de prêt ou de don
- Recherche et filtrage des annonces par catégorie et par type
- Demandes d’emprunt avec suivi de leur statut
- Messagerie privée entre utilisateurs
- Espace d’administration pour consulter les statistiques, gérer les utilisateurs et modérer les annonces
- Ajout de photos aux annonces et aux profils

## Technologies

- PHP 8.0 ou supérieur
- MySQL ou MariaDB
- HTML, CSS et JavaScript
- Font Awesome 6 pour les icônes (chargé depuis CDN)

## Prérequis

- Un serveur web compatible PHP (Apache, par exemple)
- PHP avec les extensions `pdo_mysql`, `mbstring` et `fileinfo`
- MySQL ou MariaDB
- Les sessions PHP et le téléversement de fichiers activés

## Installation locale

1. Placez le projet dans le dossier servi par votre serveur web, sous le nom `voisinpartage`. Avec XAMPP, par exemple, le chemin peut être `htdocs/voisinpartage`.
2. Créez le schéma et les tables en important `sql/creation.sql` dans MySQL. Par exemple, depuis la racine du projet :

   ```bash
   mysql -u root -p < sql/creation.sql
   ```

3. Configurez la connexion à la base de données dans `config/database.php` : hôte, nom de base, utilisateur et mot de passe. La configuration fournie cible une base locale nommée `voisinpartage` et un utilisateur `root` sans mot de passe ; adaptez-la à votre environnement.
4. Pour remplir la base avec des catégories et des comptes de démonstration, importez éventuellement `sql/donnees_test.sql` :

   ```bash
   mysql -u root -p voisinpartage < sql/donnees_test.sql
   ```

   **Attention :** ce script vide les tables concernées avant d’insérer les données de démonstration. Ne l’exécutez pas sur une base contenant des données à conserver ni en production. Les comptes créés par ce script sont réservés au développement ; ils partagent le mot de passe `password123`.

5. Ouvrez [`http://localhost/voisinpartage/`](http://localhost/voisinpartage/) dans votre navigateur.

Les fichiers envoyés par les utilisateurs sont enregistrés sous `assets/images/uploads/`. Le serveur web doit pouvoir écrire dans ce dossier.

Les photos téléversées sont des fichiers locaux et ne doivent pas être versionnées. Le `.gitignore` conserve l’avatar par défaut et ignore les photos de profils et d’annonces.

## Structure du projet

```text
.
├── admin/                 # Administration et modération
├── annonces/              # Consultation et gestion des annonces
├── assets/
│   ├── css/               # Feuille de style
│   ├── js/                # Scripts du navigateur
│   └── images/            # Images par défaut et fichiers téléversés
├── config/                # Configuration de la base de données
├── demandes_emprunt/      # Traitement des demandes
├── includes/              # Fonctions et gabarits partagés
├── messages/              # Messagerie
├── profil/                # Profil utilisateur
├── sql/                   # Création du schéma et données de démonstration
├── connexion.php
├── deconnexion.php
├── index.php
└── inscription.php
```

## Configuration du chemin d’accès

Les liens vers les ressources et les pages partagées sont actuellement construits pour une installation à l’adresse `/voisinpartage/`. Si vous installez le projet à la racine du domaine ou sous un autre nom de dossier, adaptez notamment le préfixe de chemin dans `includes/header.php` et `includes/footer.php`.

## Avant de publier ou de déployer

- Remplacez les identifiants de base de données par des identifiants locaux ou de déploiement appropriés. N’utilisez pas le compte MySQL `root` en production.
- N’importez pas les données de démonstration dans une base réelle.
- Vérifiez les fichiers présents dans `assets/images/uploads/` et ne publiez pas de photos ou de données personnelles sans autorisation.
- Les documents de conception (`Diagramme_de_Cas_Classes_et_Séquences.pdf` et `cahier_de_charge.pdf`) ne sont pas inclus dans le dépôt Git ; ils ne sont pas nécessaires au fonctionnement de l’application.
- Les comptes de démonstration et leur mot de passe commun ne doivent jamais être utilisés sur un site accessible publiquement.
- Le dépôt ne précise pas de licence : ajoutez-en une si vous souhaitez définir les conditions de réutilisation du code.

## Licence

Aucune licence n’est spécifiée pour le moment.

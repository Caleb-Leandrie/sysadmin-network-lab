# Stack de supervision et d'administration Docker

## Présentation

Ce projet consiste à préparer une infrastructure composée de plusieurs conteneurs Docker pour la supervision et l'administration d'une base de données.

## Architecture

| Service | Rôle | Port |
|---|---|---|
| Grafana | Visualisation et supervision | 3000 |
| MySQL | Stockage des données | 3306 dans le conteneur |
| Adminer | Administration de la base de données | 8081 |

Les données persistantes sont stockées dans des volumes Docker nommés.

## Technologies

- Linux
- Docker
- Docker Compose
- Grafana
- MySQL
- Adminer
- Git et GitHub

## Sécurité

- Les mots de passe sont fournis par des variables d'environnement.
- Les données sont conservées dans des volumes persistants.
- Le port MySQL n'est pas publié directement sur l'hôte dans la configuration initiale.

## Déploiement

1. Installer Docker et le plugin Docker Compose.
2. Configurer les variables d'environnement requises.
3. Vérifier la configuration Compose.
4. Démarrer les services lorsque les ports nécessaires sont disponibles.
5. Vérifier l'état des conteneurs et consulter leurs journaux.

## État du projet

Configuration initiale et documentation en cours. Les tests de démarrage, de persistance et de fonctionnement seront ajoutés après validation dans l'environnement local.

## Captures d'écran et preuves

Les captures d'écran seront ajoutées après les tests pratiques.

### 1. Architecture des conteneurs

<!-- Capture à ajouter : architecture de la stack Docker -->

### 2. État des services

<!-- Capture à ajouter : résultat de docker compose ps -->

### 3. Supervision Grafana

<!-- Capture à ajouter : interface Grafana fonctionnelle -->

### 4. Administration MySQL avec Adminer

<!-- Capture à ajouter : connexion et consultation de la base de données -->

### 5. Persistance des données

<!-- Capture à ajouter : vérification après redémarrage des conteneurs -->

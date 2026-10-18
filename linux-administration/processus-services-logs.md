# Gestion des processus, des services et des logs Linux

## Objectif

Apprendre à :
- Afficher les processus en cours d'exécution.
- Vérifier l'état d'un service Linux.
- Consulter les journaux système.
- Tester le fonctionnement d'un serveur HTTP.

## Gestion des processus

### Commande utilisée

```bash
ps aux
```

Cette commande affiche les processus en cours d'exécution sur le système.

Informations importantes :
- `USER` : utilisateur qui exécute le processus.
- `PID` : identifiant unique du processus.
- `%CPU` : pourcentage d'utilisation du processeur.
- `%MEM` : pourcentage d'utilisation de la mémoire.
- `STAT` : état du processus.
- `COMMAND` : commande associée au processus.

Pour examiner un processus précis :

```bash
ps -p 1490 -o pid,user,stat,cmd
```

Cette commande affiche les informations du processus dont le PID est `1490`.

## Gestion des services avec systemd

### Vérifier l'état d'Apache2

```bash
systemctl status apache2
```

Cette commande permet de vérifier si le service fonctionne et s'il est configuré pour démarrer automatiquement.

- `active (running)` : le service est en cours d'exécution.
- `enabled` : le service est configuré pour démarrer automatiquement au démarrage du système.

### Commandes principales

```bash
sudo systemctl start apache2
sudo systemctl stop apache2
sudo systemctl restart apache2
sudo systemctl enable apache2
sudo systemctl disable apache2
```

- `start` : démarre le service.
- `stop` : arrête le service.
- `restart` : redémarre le service.
- `enable` : active le démarrage automatique.
- `disable` : désactive le démarrage automatique.

## Consultation des journaux

### Commande utilisée

```bash
sudo journalctl -u apache2 --no-pager -n 10
```

Cette commande affiche les dix dernières lignes des journaux d'Apache2.

Les journaux permettent notamment de :
- Comprendre les événements du service.
- Repérer les avertissements et les erreurs.
- Vérifier les démarrages et les arrêts du service.

Pendant le test, un avertissement `AH00558` concernant la directive `ServerName` est apparu. Apache2 a néanmoins démarré avec succès.

## Test du serveur HTTP

### Commande utilisée

```bash
curl -I http://localhost
```

Cette commande envoie une requête HTTP au serveur local et affiche les en-têtes de la réponse.

Résultat obtenu :

```text
HTTP/1.1 200 OK
Server: Apache/2.4.68 (Debian)
Content-Type: text/html
```

Le code `200 OK` indique que la requête HTTP a réussi.

## Conclusion

Ce TP m'a permis de découvrir les commandes de base pour examiner les processus Linux, gérer un service avec `systemctl`, consulter les journaux avec `journalctl` et tester un serveur HTTP avec `curl`.

Ces commandes constituent une première base pour le diagnostic et l'administration d'un système Linux.
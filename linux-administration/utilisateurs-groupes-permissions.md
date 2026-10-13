# TP 02 — Gestion des utilisateurs, groupes et permissions sous Linux

## Objectif

Ce TP a pour objectif de comprendre et de pratiquer la gestion des utilisateurs, des groupes et des permissions sous Linux.

Les manipulations réalisées permettent de :

- Créer un utilisateur et un groupe.
- Ajouter un utilisateur à un groupe.
- Comprendre les permissions de fichiers et de répertoires.
- Modifier les permissions avec `chmod`.
- Modifier le groupe propriétaire avec `chgrp`.
- Utiliser le bit SGID pour faciliter le partage de fichiers dans un répertoire commun.

## Création d'un groupe et d'un utilisateur

### Création du groupe

La commande suivante permet de créer un groupe nommé `techniciens` :

```bash
sudo groupadd techniciens
```

Vérification du groupe :

```bash
getent group techniciens
```

### Création de l'utilisateur

La commande suivante permet de créer un utilisateur nommé `stagiaire` :

```bash
sudo adduser stagiaire
```

Vérification du compte utilisateur :

```bash
id stagiaire
```

### Ajout de l'utilisateur au groupe

Pour ajouter `stagiaire` au groupe `techniciens` sans supprimer ses autres appartenances, on utilise :

```bash
sudo usermod -aG techniciens stagiaire
```

Vérification :

```bash
getent group techniciens
```

## Compréhension des permissions Linux

Sous Linux, les permissions déterminent les actions autorisées sur un fichier ou un répertoire.

Il existe trois types de permissions :

| Permission | Signification         |
|------------|-----------------------|
| `r`        | Lecture (*read*)      |
| `w`        | Écriture (*write*)    |
| `x`        | Exécution (*execute*) |

Les permissions s'appliquent à trois catégories :

- **Propriétaire** : utilisateur qui possède le fichier ou le répertoire.
- **Groupe** : groupe propriétaire du fichier ou du répertoire.
- **Autres** : tous les autres utilisateurs.

### Exemple

```bash
ls -ld /srv/techniciens
```

Résultat obtenu :

```text
drwxrwxr-x
```

Interprétation :

- `d` : il s'agit d'un répertoire.
- `rwx` : le propriétaire peut lire, écrire et accéder au répertoire.
- `rwx` : les membres du groupe peuvent lire, écrire et accéder au répertoire.
- `r-x` : les autres utilisateurs peuvent lire et accéder au répertoire, mais ne peuvent pas y créer de fichiers.

## Modification des permissions avec `chmod`

La commande `chmod` permet de modifier les permissions d'un fichier ou d'un répertoire.

### Utilisation des symboles

Exemple :

```bash
chmod o-x ~/test-permissions
```

Cette commande retire le droit d'exécution (`x`) à la catégorie des autres utilisateurs (`o`).

### Utilisation de la notation numérique

Les permissions peuvent également être représentées par des chiffres :

- `r = 4` : lecture
- `w = 2` : écriture
- `x = 1` : exécution

Exemple :

```bash
chmod 750 ~/test-permissions
```

Interprétation :

- `7 = 4 + 2 + 1` : `rwx` pour le propriétaire.
- `5 = 4 + 1` : `r-x` pour le groupe.
- `0` : aucun droit pour les autres utilisateurs.

Vérification des permissions :

```bash
ls -ld ~/test-permissions
```

## Création d'un répertoire partagé

### Création du répertoire

On crée un répertoire destiné au partage de fichiers entre les techniciens :

```bash
sudo mkdir /srv/techniciens
```

### Modification du groupe propriétaire

On attribue le répertoire au groupe `techniciens` :

```bash
sudo chgrp techniciens /srv/techniciens
```

### Attribution des permissions

On autorise le propriétaire et le groupe à lire, écrire et accéder au répertoire :

```bash
sudo chmod 775 /srv/techniciens
```

Vérification :

```bash
ls -ld /srv/techniciens
```

Le répertoire appartient à `root` et au groupe `techniciens`. Avec les permissions `775`, le propriétaire et le groupe disposent des droits `rwx`, tandis que les autres utilisateurs disposent des droits `r-x`.

## Utilisation du bit SGID

### Problème rencontré

Lorsqu'un utilisateur crée un fichier dans `/srv/techniciens`, le groupe propriétaire du fichier peut être différent de celui du répertoire partagé.

Cela peut compliquer la collaboration entre les membres du groupe `techniciens`.

### Activation du SGID

On active le bit SGID sur le répertoire partagé :

```bash
sudo chmod g+s /srv/techniciens
```

Vérification :

```bash
ls -ld /srv/techniciens
```

La présence de `s` à la place du `x` dans les permissions du groupe indique que le bit SGID est activé.

### Résultat observé

Après l'activation du SGID, les nouveaux fichiers créés dans ce répertoire héritent du groupe propriétaire `techniciens`.

Ce mécanisme facilite le partage des fichiers entre les membres du groupe.

**Remarque :** le SGID ne donne pas automatiquement le droit de modifier tous les fichiers. Les permissions du fichier restent importantes.
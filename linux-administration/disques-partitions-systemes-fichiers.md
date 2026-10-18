# Gestion des disques, partitions et systèmes de fichiers Linux

## Objectif

Apprendre à :
- Identifier les disques et les partitions.
- Vérifier l'espace utilisé et disponible.
- Identifier les systèmes de fichiers.
- Lire la table des partitions d'un disque.

## Identifier les disques et les partitions

### Commande utilisée

```bash
lsblk
```

Cette commande affiche les disques, leurs partitions, leurs tailles et leurs points de montage.

Notions importantes :
- `disk` : disque complet.
- `part` : partition d'un disque.
- `MOUNTPOINTS` : emplacement où le système de fichiers est accessible.

## Vérifier l'espace disque

### Commande utilisée

```bash
df -h
```

Cette commande affiche la taille des systèmes de fichiers, l'espace utilisé et l'espace disponible.

L'option `-h` présente les tailles dans un format lisible, comme Go et Mo.

Informations importantes :
- `Taille` : capacité totale.
- `Utilisé` : espace occupé.
- `Dispo` : espace disponible.
- `Uti%` : pourcentage d'espace utilisé.
- `Monté sur` : point de montage.

## Identifier les systèmes de fichiers

### Commande utilisée

```bash
lsblk -f
```

Cette commande affiche les systèmes de fichiers, leurs labels et leurs UUID.

Exemples de systèmes de fichiers :
- `ext4` : couramment utilisé sous Linux.
- `vfat` / `FAT32` : utilisé notamment pour les partitions de démarrage UEFI.
- `NTFS` : couramment utilisé sous Windows.

Le label est un nom attribué à un système de fichiers. L'UUID est un identifiant qui permet de l'identifier.

## Examiner la table des partitions

### Commande utilisée

```bash
sudo fdisk -l /dev/sda
```

Cette commande affiche les informations de partitionnement du disque sans modifier les partitions.

Notions importantes :
- `Disklabel type: dos` : indique une table de partitions de type MBR.
- `Linux` : type de partition indiqué pour la partition principale Linux.
- `Extended` : partition étendue pouvant contenir des partitions logiques.
- `NTFS` : type indiqué pour la partition logique de données.

Dans le partitionnement MBR, une partition étendue permet d'organiser des partitions logiques supplémentaires.

## Précautions d'administration

Avant toute opération de modification d'un disque ou d'une partition :
- Identifier précisément le disque concerné.
- Vérifier les partitions et leurs points de montage.
- Sauvegarder les données importantes.
- Ne pas lancer de commande de formatage ou de modification sans comprendre ses effets.

## Conclusion

Ce TP m'a permis de découvrir les commandes `lsblk`, `df -h`, `lsblk -f` et `fdisk -l` pour examiner les disques, les partitions, l'espace disponible et les systèmes de fichiers Linux.

Ces commandes constituent une base importante pour l'administration et le diagnostic du stockage sous Linux.
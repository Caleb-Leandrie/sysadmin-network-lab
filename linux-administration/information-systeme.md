# TP 01 — Informations système sous Linux

## Objectif

L'objectif de ce travail pratique est d'apprendre à consulter les informations essentielles d'un système Linux : le système d'exploitation, la mémoire, l'espace disque et la configuration réseau.

## Environnement de travail

- **Système d'exploitation :** Parrot Security 7.4
- **Noyau Linux :** 7.1.13+parrot7-amd64
- **Architecture :** x86-64
- **Matériel :** ASUS N551JK

## Commandes utilisées

### Informations système

```bash
hostnamectl
```

Cette commande affiche le nom de la machine, le système d'exploitation, la version du noyau et l'architecture.

### Mémoire RAM

```bash
free -h
```

Cette commande affiche la mémoire totale, la mémoire utilisée, la mémoire disponible et l'espace swap.

### Espace disque

```bash
df -h
```

Cette commande permet de vérifier l'espace disque total, utilisé et disponible sur les systèmes de fichiers.

### Interfaces réseau

```bash
ip -br addr
```

Cette commande affiche les interfaces réseau et leurs adresses IP de manière concise.

### Table de routage

```bash
ip route
```

Cette commande affiche les routes réseau et la passerelle par défaut.


## Conclusion

Ce travail pratique m'a permis de découvrir plusieurs commandes essentielles pour examiner un système Linux et vérifier ses ressources matérielles ainsi que sa configuration réseau.

Ces commandes constituent une première étape dans l'apprentissage de l'administration système Linux.
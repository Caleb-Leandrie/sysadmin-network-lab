# Diagnostic réseau sous Linux

## Objectif

L’objectif de ce TP est de vérifier la configuration réseau d’un système Linux, la connectivité avec la passerelle, la résolution DNS et l’accès aux services web HTTP/HTTPS.

## Identification des interfaces réseau

**Commande :**

```bash
ip -br a
```

Cette commande permet d’afficher les interfaces réseau, leur état et leurs adresses IP.

**Résultats observés :**
- `wlp4s0` : interface Wi-Fi active, adresse IPv4 `10.25.204.74/24`.
- `enp5s0f1` : interface Ethernet inactive.
- `docker0` : interface virtuelle utilisée par Docker.
- `vboxnet0` : interface réseau Host-Only de VirtualBox, actuellement inactive.

## Analyse de la table de routage

**Commande :**

```bash
ip route
```

La route par défaut utilise la passerelle `10.25.204.94` via l’interface `wlp4s0`.

Le réseau Wi-Fi est `10.25.204.0/24`.

## Vérification de la passerelle

**Commande :**

```bash
ping -c 4 10.25.204.94
```

**Résultat :**
- 4 paquets transmis.
- 4 paquets reçus.
- 0 % de perte.
- Temps moyen : 5,961 ms.

**Conclusion :** la passerelle répond aux requêtes ICMP pendant le test.

## Vérification de la résolution DNS

**Commande :**

```bash
getent hosts debian.org
```

Le système a retourné plusieurs adresses IPv6 associées au nom `debian.org`.

**Conclusion :** la résolution du nom de domaine a fonctionné pour cette requête.

## Vérification de HTTP

**Commande :**

```bash
curl -I --max-time 10 http://debian.org
```

**Résultat :** `HTTP/1.1 302 Found`

La réponse indique une redirection vers `https://www.debian.org/`.

## Vérification de HTTPS

**Commande :**

```bash
curl -I --max-time 10 https://www.debian.org/
```

**Résultat :** `HTTP/2 200`

Le serveur a répondu avec le code HTTP 200, indiquant que la requête a réussi. La réponse déclare également `text/html` comme type de contenu et Apache comme serveur web.

## Conclusion générale

Les tests effectués ont permis de vérifier les interfaces réseau, la route par défaut, la connectivité avec la passerelle, la résolution DNS et l’accès à un serveur web en HTTP et HTTPS.

Ces résultats décrivent uniquement les tests réalisés au moment du diagnostic. Ils ne garantissent pas à eux seuls le bon fonctionnement permanent de l’ensemble du réseau ni la sécurité complète des communications.
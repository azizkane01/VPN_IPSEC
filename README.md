
#  VPN IPsec Site-à-Site Cisco avec services inter-sites

Ce projet démontre la mise en place d’un VPN IPsec **site-à-site** entre deux sites distants simulés dans **GNS3**, en utilisant des **routeurs Cisco**, afin de sécuriser les échanges et tester des services interconnectés.

##  Architecture réseau

* **Site A** : 192.168.2.0/24 – héberge un **serveur web (Apache2)**
* **Site B** : 192.168.3.0/24 – héberge une **base de données (PostgreSQL)** via Docker
* **Lien inter-site** : 10.1.1.0/24 entre les routeurs R1 et R2

##  Configuration

* Configuration des interfaces réseau sur R1 et R2
* Mise en place d’un tunnel VPN avec :

  * Politique ISAKMP (phase 1)
  * Transform-set IPSec (phase 2)
  * Crypto map avec ACL
* Tests de connectivité avec `ping`, `show crypto isakmp sa` et `show crypto ipsec sa`

##  Services déployés

* Serveur Web (Apache2) sur Site A avec une page HTML simple
* PostgreSQL sur Site B via Docker :

  * Création d’une base `securite`
  * Création d’un utilisateur `aziz`
  * Deux tables : `utilisateurs` (avec mot de passe hashé) et `utilisateurs_clair` (mots de passe en clair pour test)

##  Tests de sécurité

Deux scénarios sont testés pour analyser la sécurité des échanges :

1. **VPN actif + mot de passe hashé** : communication sécurisée
2. **VPN inactif + mot de passe en clair** : vulnérabilité à l’interception

> Wireshark a été utilisé pour observer les différences entre les deux cas.

##  Accès inter-sites

* Ping et communication HTTP/SQL entre les deux sites validés
* Accès base de données PostgreSQL depuis le serveur Web distant

##  Fonctionnement du protocole ESP (IPsec)

* **Chiffrement** de la charge utile
* **Authentification** optionnelle
* **Intégrité** des données + protection anti-rejeu
* **Encapsulation** totale du paquet IP (mode tunnel)

##  Limites de HTTP seul

* HTTP n’offre aucun chiffrement : données interceptables
* Importance du VPN ou d’un protocole sécurisé comme HTTPS

##  Conclusion

Ce projet prouve l’efficacité d’un VPN IPsec pour :

* Protéger les échanges entre sites distants
* Préserver la **confidentialité**, **intégrité**, et **authenticité** des données
* Assurer une **infrastructure réseau sécurisée** sur Internet


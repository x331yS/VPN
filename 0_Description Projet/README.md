# OpenVPN

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Description Projet

### _Offrir un accès à l’intranet depuis l’extérieur._

#### - Accès distant
- Via SSH

#### - Utilisation d’une vrai IP publique 
- Derrière votre box  
- Location de serveur

#### - Gestion firewall pour autoriser l’accès extérieur

#### - Sécurité 
- redondance du serveur VPN
- Authentification des utilisateurs
- Attribution d’une IP fixe à chacun des utilisateurs (pour pouvoir tracer leurs actions avec leur IP)
- Logs
- Gestion de certificats

### _Maquette attendue_
- Documentation utilisateur (une procédure qu’on peut donner à un nouvel employé pour qu’il puisse se connecter au VPN)
- Une machine qui sert de serveur VPN, de préférence à domicile pour avoir une IP publique
- Un client qui se connecte avec succès au VPN
- Gestion des logs de connexion (rétention, archivage, purge)

> Idées Technos possibles (non exhaustif)•OpenVPN, OpenSwan, StrongSwan, etc.


### _Description Outil Utilisé_

- Ubuntu pour lma machine virtuelle.
- OpenVPN, il s'agit d'un logiciel libre permettant de créer un réseau privé virtuel (VPN).
- Serveur DigitalOcean distant.



# Installation et configuration d'OpenVPN


[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Il faut tout d'abord télécharger le package OpenVPN

![img.png](img.png)

Allez dans **Wizards** -> **VPN** -> **OpenVPN**

- **Type of server** : Local User Access
![img_1.png](img_1.png)

- **Certificate Authority** : pfSense FireWall
![img_2.png](img_2.png)

- **Certificate** : pfSense OpenVPN
![img_3.png](img_3.png)

![img_5.png](img_5.png)

## Tunnel Settings

- **Tunnel Network** : 192.168.30.0/24
- Cochez la case **Inter-Client Communication**

![img_6.png](img_6.png)

## Client Settings

![img_7.png](img_7.png)

Il faut ensuite retourner dans **VPN** -> **OpenVPN** -> **Servers** pour modifier l'interface
![img_4.png](img_4.png)

- **Server Mode** : Remote Access (SSL/TLS + User Auth)
- **Interface** : CARP WAN

![img_8.png](img_8.png)

Vous avez maintenant accès à de nouvelles options.
- Cochez la case **Redirect IPv4 Gateway** dans **Tunnel Settings**

Pour finir, il faut télécharger le fichier de configuration. Pour cela, allez dans **VPN** -> **OpenVpn** -> **Client Export**.

**Host Name Resolution** -> **Interface IP Address**

Il faut maintenant exporter le **Most Clients** et y mettre l'adresse IP de votre machine server.

![img_9.png](img_9.png)

Pour finir, dans les paramètres de votre box internet, il faut y ajouter les règles suivantes.

![img_10.png](img_10.png)

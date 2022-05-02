# OpenVPN

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Démarrage d’OpenVPN

````shell
sudo systemctl start openvpn@server
````

Vous pouvez vérifier le status du service avec cette commande

````shell
sudo systemctl status openvpn@server
````

Configurez maintenant le service pour qu’il se lance à chaque démarrage du système

````shell
sudo systemctl enable openvpn@server
````


# OpenVPN

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Infrastructure de configuration du client

#### _Pour la fin de l'installation, il suffit de s'occuper de la configuration client._


On va tout d’abord créé un nouveau dossier qui va contenir les fichiers de configuration du client.

````shell
mkdir -p ~/client-configs/files
````
On va maintenant copier un exemple de fichier de configuration afin d’avoir une base. On va ensuite l’éditer

````shell
cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf ~/client-configs/base.conf
nano ~/client-configs/base.conf
````

Il faut mettre l’IP de votre serveur à la ligne remote

![Remote](remote.png)

> Vérifier que le protocole utilisé est bien l’UDP

![Udp](udp.png)

Il faut également décommenter les lignes user et group

![Uncomment](uncomment.png)

Commentez les directives ca, cert et key car on ajoutera les certificats et les clés dans le dossier lui-même

![Comment](comment.png)

Faire de même pour ``tls-auth``

![Tls-auth](tls-auth.png)

Utilisez les mêmes paramètres ``cypher`` et ``auth`` que ceux que vous avez définis dans le fichier ``/etc/openvpn/server.conf``

![CypherxAuth](cypherxauth.png)

Il faut ensuite ajouté key-direction n’importe où dans le fichier et régler le paramètre sur 1
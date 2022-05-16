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

![KeyDirection](key-direction.png)

Rajoutez ces lignes là à la fin du fichier

````shell
# script-security 2
# up /etc/openvpn/update-resolv-conf
# down /etc/openvpn/update-resolv-conf
````

>Vous décommenterez ces lignes si le client possède une machine sous Linux et qu’il possède un fichier ``/etc/openvpn/update-resolv-conf``

### Compilation du fichier de configuration de base avec les différents fichiers de certificat

````shell
nano ~/client-configs/make_config.sh
````

_Voici le contenu du script :_

````shell
#!/bin/bash

# First argument: Client identifier

KEY_DIR=~/client-configs/keys
OUTPUT_DIR=~/client-configs/files
BASE_CONFIG=~/client-configs/base.conf

cat ${BASE_CONFIG} \
    <(echo -e '<ca>') \
    ${KEY_DIR}/ca.crt \
    <(echo -e '</ca>\n<cert>') \
    ${KEY_DIR}/${1}.crt \
    <(echo -e '</cert>\n<key>') \
    ${KEY_DIR}/${1}.key \
    <(echo -e '</key>\n<tls-auth>') \
    ${KEY_DIR}/ta.key \
    <(echo -e '</tls-auth>') \
    > ${OUTPUT_DIR}/${1}.ovpn
````

Rendez le fichier exécutable en changeant les droits

````shell
chmod 700 ~/client-configs/make_config.sh
````

Déplacez les fichier ``client_name.crt`` et ``client_name.key`` dans le dossier ``~/client-configs`` puis éxécuter le script.

````shell
cd ~/client-configs
sudo ./make_config.sh client_name
````

Un fichier a maintenant été créé dans le dossiers ``files``

````shell
ls ~/client-configs/files

[Output]
client_name.ovpn
````

Déplacez maintenant ce fichier sur votre machine qui souhaitera utiliser le VPN

````shell
sftp root@157.245.45.81:client-configs/files/client_name.ovpn ~/
````


### Installation de la configuration client

### _MacOS_

Téléchargez [https://tunnelblick.net/](https://tunnelblick.net/), ce client openVPN est gratuit et opensource

À la fin du téléchargement, tunneblick vous demandera si vous avez des fichiers de configurations, répondez que oui.

![Mac](mac.png)

Ouvrez ensuite le Finder et double cliquez sur le fichier .ovpn

### _Windows_

Téléchargez l’application client OpenVPN pour Windows depuis la page de téléchargement d’[OpenVPN](https://openvpn.net/community-downloads/).
Choisissez la version d’installation appropriée pour votre version de Windows.

Après avoir installé OpenVPN, copiez le fichier .ovpn dans ``C:\Program Files\OpenVPN\config``

Lorsque vous lancez OpenVPN, il voit automatiquement le profil et le rend disponible.
Vous devez exécuter OpenVPN en tant qu’administrateur à chaque fois qu’il est utilisé, même par des comptes administratifs. Pour effectuer cette action sans avoir à cliquer sur le bouton droit de la souris et à sélectionner Exécuter en tant qu’administrateur chaque fois que vous utilisez le VPN, vous devez le pré-régler à partir d’un compte administratif. Cela signifie également que les utilisateurs standard devront entrer le mot de passe de l’administrateur pour utiliser OpenVPN. Les utilisateurs standard ne peuvent pas se connecter correctement au serveur à moins que l’application OpenVPN sur le client n’ait des droits d’administrateur, les privilèges élevés sont donc nécessaires.
Pour que l’application OpenVPN s’exécute toujours en tant qu’administrateur, cliquez avec le bouton droit de la souris sur son icône de raccourci et allez dans Propriétés. En bas de l’onglet Compatibilité, cliquez sur le bouton Modifier les paramètres pour tous les utilisateurs. Dans la nouvelle fenêtre, cochez Exécuter ce programme en tant qu’administrateur.

#### _Connexion_

À chaque fois que vous lancez l’interface graphique d’OpenVPN, Windows vous demande si vous souhaitez autoriser le programme à apporter des modifications à votre ordinateur. Cliquez sur Oui. Le lancement de l’application client OpenVPN ne fait que placer l’applet dans la barre d’état système afin que vous puissiez connecter et déconnecter le VPN selon vos besoins : il n’établit pas réellement la connexion VPN.

Une fois qu’OpenVPN est lancé, initiez une connexion en vous rendant dans l’applet de la barre d’état système et en cliquant avec le bouton droit de la souris sur l’icône de l’applet OpenVPN. Cela ouvre le menu contextuel. Sélectionnez client1 en haut du menu (c’est votre profil client1.ovpn) et choisissez Connecter.

Une fenêtre d’état s’ouvrira, montrant la sortie du journal pendant que la connexion est établie, et un message s’affichera une fois que le client sera connecté.

Déconnectez-vous du VPN de la même manière : allez dans l’applet de la barre d’état système, cliquez avec le bouton droit de la souris sur l’icône de l’applet OpenVPN, sélectionnez le profil du client et cliquez sur Déconnecter.
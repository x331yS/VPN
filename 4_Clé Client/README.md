# OpenVPN

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Création d’une paire certificat/clé client

>Attention beaucoup de changement entre Serveur VPN et Machine AC à effectuer

### Serveur VPN

````shell
mkdir -p ~/client-configs/keys
chmod -R 700 ~/client-configs
cd ~/EasyRSA-3.0.4/
./easyrsa gen-req client_name nopass
````

Copiez le fichier ``client_name.key`` dans le répertoire``/client-configs/keys/``

````shell
cp pki/private/client_name.key ~/client-configs/keys/
````

Il faut ensuite transférer le fichier .req sur la machine AC

````shell
scp pki/reqs/client_name.req root@138.68.156.246:/tmp
````

#### Machine AC

Il faut ensuite importer la demande de certificat

````shell
cd EasyRSA-3.0.4/
./easyrsa import-req /tmp/client_name.req client_name
````

Il faut ensuite signer la demande du client

````shell
./easyrsa sign-req client client_name
````

Un fichier de certificat client nommé ``client_name.crt`` a été créé, il faut le transférer sur la machine qui sert de VPN.

````shell
scp pki/issued/client_name.crt root@157.245.45.81:/tmp
````

### Serveur VPN

Copiez le certificat dans le répertoire suivant

````shell
cp /tmp/client_name.crt ~/client-configs/keys/
````

Copiez également les fichiers ``ca.crt`` et ``ca.key``

````shell
cp ~/EasyRSA-3.0.4/ta.key ~/client-configs/keys/
sudo cp /etc/openvpn/ca.crt ~/client-configs/keys/
````
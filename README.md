# Tutoriel Bluetooth - Échanger des fichiers via Bluetooth avec `bluetoothctl`, `hcitool` et `obexftp` + hacking

Ce tutoriel explique **toutes les commandes nécessaires** pour se connecter à des appareils via Bluetooth et échanger des fichiers, en utilisant les outils `bluetoothctl`, `hcitool` et `obexftp`.

## Prérequis

- Un adaptateur Bluetooth sur le PC + Debian 13
- Un téléphone Android avec Bluetooth activé.
- Paquets nécessaires :
  - `bluetoothctl` pour gérer les connexions Bluetooth.
  - `hcitool` pour scanner les appareils Bluetooth.
  - `obexftp` pour envoyer et recevoir des fichiers via Bluetooth.

## 1. Outil hcitool

**Vous devez activer le bluetooth sur votre ordinateur pour commencer et activer l'appairage sur le téléphone pour le repérer.**

Pour scanner le Bluetooth, saisir dans un terminal la commande suivante :
```
hcitool scan
```
[INSERER CAPTURE]

Cette commande va permettre de repérer tous les appareils bluetooth à proximité.

## 2. Outil bluetoothctl 
### Commandes de bases

Pour ouvrir Bluetoothctl, saisir la commande suivante dans le terminal : 
```
bluetoothctl
```
Pour activer l'agent bluetooth, saisir la commande : 
```
agent-on
```
Puis : 
```
default-agent
```
Pour passer en mode découvrable : 
```
discoverable on
```
Pour autoriser l'appreillement : 
```
pairable on
```
Pour lancer un scan : 
```
scan on
```

### Appareillement téléphone portable

Pour s'appareiller avec un téléphone portable, mettre le téléphone en mode "pairable" et une fois l'adresse MAC de celui-ci détectée, la ressaisir à la place des "XX.XX.XX.XX.XX.XX" : 
```
pair XX.XX.XX.XX.XX.XX
```
Puis, confirmer le passkey entre les 2 appareils pour la connexion en saisissant "yes" dans le terminal bluetoothctl.

Une fois l'appareillement effectué, vous pouvez vous connecter à l'appareil : 
```
connect XX.XX.XX.XX.XX.XX
```
### Envoyer un fichier sur le téléphone portable

Pour envoyer un fichier sur un téléphone portable, utiliser la commande obexftp suivante : 
```
obexftp --nopath --noconn --uuid none --bluetooth XX.XX.XX.XX.XX.XX --channel 12 --put <chemin_du_fichier>
```
_Note : Sur le téléphone portable vous pourrez choisir d'accepter ou de refuser la réception d'un fichier._

### Envoyer un fichier sur un ordinateur

Pour envoyer un fichier sur un ordinateur, utiliser la même commande mais en changeant le channel :

```
obexftp --nopath --noconn --uuid none --bluetooth XX.XX.XX.XX.XX.XX --channel 9 --put <chemin_du_fichier>
```
`--nopath` va permettre de ...

`--noconn` va permettre de ...

`--uuid none` va permettre de ...

`--bluetooth XX.XX.XX.XX.XX.XX` va permettre de ...

`--channel` va permettre de ...

`--put` permet d'envoyer le fichier

_Note : Selon le type d'appareil les channels peuvent varier._

# Guide-piratage-Bluetooth

## 1. BlueDucky

BlueDucky est un outil open-source qui automatise l'exploitation d'une vulnérabilité Bluetooth critique, identifiée sous CVE-2023-45866.

Elle permet à un attaquant non authentifié, en proximité Bluetooth, d'envoyer des paquets forgés pour contourner l'authentification et se faire passer pour un clavier HID sans confirmation utilisateur. Cela exploite un bogue dans la machine d'état Bluetooth, où l'hôte accepte une connexion chiffrée et injecte des frappes clavier arbitraires, comme installer des apps ou exécuter des commandes.

Cet outil fonctionne grâce à un simple script Python exécutable sous linux et/ou Raspberry Pi

Lien Github BlueDucky : https://github.com/pentestfunctions/BlueDucky/blob/main/utils/menu_functions.py

Note : Des mises à jours seront à effectuer sur le code Python :

Ligne 107 dans la fonction **BlueDucky.py** : ssp_command = ["sudo", "hciconfig", self.iface, "sspmode"]

Ligne 46 dans la fonction **menu_functions.py** : time.sleep(5)

## 2. Bluebugger

Bluebugger est un outil open-source de pentesting Bluetooth, similaire à BlueDucky mais axé sur l'exploitation de vulnérabilités plus anciennes comme le bluebugging.

Celui-ci demande d'être déjà appairé avec l'appareil (peut être possible en utilisant l'outil précédent)
Cet outil va permettre d'afficher directement les contacts de l'appareil ciblé contenant les noms et les numéros de téléphones. 
Il va également permettre d'afficher les informations sur l'appareil ciblé.

Lien Github Bluebugger : https://github.com/webdragon63/Bluebugger


## 3. mapAccountHijack

Celui-ci demande aussi d'être déjà appairé avec l'appareil (peut être possible en utilisant l'outil précédent)
Cet outil va permettre d'envoyer directement des messages à la place de la cible à n'importe quel numéro directement sur le téléphone de la cible. Le message est de plus éditable.

Lien Github utilisé mapAccountHijack : https://github.com/sgxgsx/mapAccountHijack

### (Facultatif) Prérequis pour utiliser cet outil : **Python 3.10.10**
Python 3 peut aussi suffir pour cet outil

### Installation Python 3.10.10 (facultatif)

Récupération du fichier .tgz sur le site officiel de Python :
```
wget https://www.python.org/ftp/python/3.10.10/Python-3.10.10.tgz
```
Extraction du fichier : 
```
tar -xvf Python-3.10.10.tgz
```
Se diriger dans le répertoire extrait : 
```
cd Python-3.10.10
```
```
./configure --enable-optimizations
```
```
make
```
```
sudo make altinstall
```
```
python3.10 -m ensurepip --upgrade
```
### Installation de l'outil (Python 3.10)

Téléchargement du github utilisé :
```
git clone https://github.com/sgxgsx/mapAccountHijack.git
```
Se diriger dans le répertoire du git téléchargé précédemment : 
```
cd mapAccountHijack
```
Créer un environnement virtuel : 
```
python3.10 -m venv .venv
```
Accéder à l'environnement virtuel : 
```
source .venv/bin/activate
```
Éditer le fichier d'installation **install.sh** pour le mettre en **Python3.10**
```
nano install.sh
```
Ajouter le droit d'exécution au fichier pour tous les utilisateurs : 
```
chmod +x install.sh
```
Exécution du fichier d'installation : 
```
sudo ./install.sh
```
[INSTRUCTIONS A VOIR SUR LE GITHUB]

Redémarrage des services :

```
sudo service bluetooth stop
sudo systemctl daemon-reload
sudo service bluetooth start
sudo hciconfig -a hci0 reset
```

Se diriger dans le répertoire nOBEX pour refaire la direction des répertoires pour Python : 
```
cd nOBEX/nOBEX
```
Déplacer tous les fichier dans ce répertoire dans le répertoire précédent : 
```
sudo mv * ../
```
Revenir ensuite en arrière dans le répertoire principal : 
```
cd ../..
```
Installer aiohttp : 
```
pip install aiohttp
```
Vous avez terminé !
Pour tester vous pouvez exécuter la commande suivante : 
```
python3.10 mapAccountHijack.py --help
```

### Installation du github (Python 3)

Téléchargement du github utilisé :
```
git clone https://github.com/sgxgsx/mapAccountHijack.git
```
Se diriger dans le répertoire du git téléchargé précédemment : 
```
cd mapAccountHijack
```
Créer un environnement virtuel : 
```
python3 -m venv .venv
```
Accéder à l'environnement virtuel : 
```
source .venv/bin/activate
```
Ajouter le droit d'exécution au fichier pour tous les utilisateurs : 
```
chmod +x install.sh
```
Exécution du fichier d'installation : 
```
sudo ./install.sh
```
[INSTRUCTIONS A VOIR SUR LE GITHUB]

Redémarrage des services :

```
sudo service bluetooth stop
sudo systemctl daemon-reload
sudo service bluetooth start
sudo hciconfig -a hci0 reset
```

Se diriger dans le répertoire nOBEX pour refaire la direction des répertoires pour Python : 
```
cd nOBEX/nOBEX
```
Déplacer tous les fichier dans ce répertoire dans le répertoire précédent : 
```
sudo mv * ../
```
Revenir ensuite en arrière dans le répertoire principal : 
```
cd ../..
```
Installer aiohttp : 
```
pip install aiohttp
```
Vous avez terminé !
Pour tester vous pouvez exécuter la commande suivante : 
```
python3 mapAccountHijack.py --help
```



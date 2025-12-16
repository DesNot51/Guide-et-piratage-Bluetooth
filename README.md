# Guide-piratage-Bluetooth

## 1. BlueDucky

BlueDucky est un outil open-source qui automatise l'exploitation d'une vulnérabilité Bluetooth critique, identifiée sous CVE-2023-45866.

Elle permet à un attaquant non authentifié, en proximité Bluetooth, d'envoyer des paquets forgés pour contourner l'authentification et se faire passer pour un clavier HID sans confirmation utilisateur. Cela exploite un bogue dans la machine d'état Bluetooth, où l'hôte accepte une connexion chiffrée et injecte des frappes clavier arbitraires, comme installer des apps ou exécuter des commandes.

Cet outil fonctionne grâce à un simple script Python exécutable sous linux et/ou Raspberry Pi

[EXPLIQUER DAVANTAGE LE FONCTIONNEMENT]

Lien Github BlueDucky : https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/pentestfunctions/BlueDucky&ved=2ahUKEwj_-fOkycCRAxW_RKQEHY7RMXAQFnoECCAQAQ&usg=AOvVaw0ofba09WYb8Ah1-BWZAqog

Note : Des mises à jours seront à effectuer sur le code Python :

Ligne 107 dans la fonction **BlueDucky.py** : ssp_command = ["sudo", "hciconfig", self.iface, "sspmode"]
Ligne 46 dans la fonction **menu_functions.py** : time.sleep(5)

## 2. Bluebugger

Bluebugger est un outil open-source de pentesting Bluetooth, similaire à BlueDucky mais axé sur l'exploitation de vulnérabilités plus anciennes comme le bluebugging.

Celui-ci demande d'être déjà appairé avec l'appareil (peut être possible en utilisant l'outil précédent)
Cet outil va permettre d'afficher directement les contacts de l'appareil ciblé contenant les noms et les numéros de téléphones. 
Il va également permettre d'afficher les informations sur l'appareil ciblé.

Lien Github Bluebugger : https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/webdragon63/Bluebugger&ved=2ahUKEwi99LnSy8CRAxUkK_sDHSrsG1IQFnoECA0QAQ&usg=AOvVaw12qGAG9L2QzrwEg0vpzhbf

## 3. Outil 3

Celui-ci demande aussi d'être déjà appairé avec l'appareil (peut être possible en utilisant l'outil précédent)
Cet outil va permettre d'envoyer directement des messages à la place de la cible à n'importe quel numéro directement sur le téléphone de la cible. Le message est de plus éditable.

Lien Github Outil 3 : 

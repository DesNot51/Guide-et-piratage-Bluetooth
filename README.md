# Guide-piratage-Bluetooth

## 1. BlueDucky

BlueDucky est un outil open-source qui automatise l'exploitation d'une vulnérabilité Bluetooth critique, identifiée sous CVE-2023-45866.

Elle permet à un attaquant non authentifié, en proximité Bluetooth, d'envoyer des paquets forgés pour contourner l'authentification et se faire passer pour un clavier HID sans confirmation utilisateur. Cela exploite un bogue dans la machine d'état Bluetooth, où l'hôte accepte une connexion chiffrée et injecte des frappes clavier arbitraires, comme installer des apps ou exécuter des commandes.

Cet outil fonctionne grâce à un simple script Python exécutable sous linux et/ou Raspberry Pi

[EXPLIQUER DAVANTAGE LE FONCTIONNEMENT]

Lien Github BlueDucky : https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://github.com/pentestfunctions/BlueDucky&ved=2ahUKEwj_-fOkycCRAxW_RKQEHY7RMXAQFnoECCAQAQ&usg=AOvVaw0ofba09WYb8Ah1-BWZAqog

## Note : Des mises à jours sont à effectuer sur le code Python en remplaçant certains caractères par d'autres notamment des suppressions de guillemets et un sleep time dans les fonctions mains.




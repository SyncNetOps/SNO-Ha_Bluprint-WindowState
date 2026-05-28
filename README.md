# 🪟 SNO WindowState - Blueprint für Home Assistant

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2FSyncNetOps%2FSNO-Ha_Bluprint-WindowState%2Fmain%2Fsno_windowstate.yaml)

**SNO WindowState** ist eine hochprofessionelle, fehlertolerante Schaltzentrale für dein Smart Home. Sie überwacht alle Fenster, Dachfenster und Türen, generiert formatierten Text für dein Dashboard und warnt dich proaktiv vor Regen bei offenen Fenstern.

## ✨ Features
* **Dashboard-Ready:** Generiert automatisch formatierte, saubere Listen (inkl. Emojis) deiner offenen Fenster für `input_text` Helfer. Umgeht das 255-Zeichen Limit von Home Assistant durch eine intelligente Split-Architektur.
* **Smarte Regenwarnung:** Überwacht das Wetter und sendet Push-Nachrichten an bis zu 3 Smartphones, wenn Dachfenster bei Regen offenstehen.
* **Erweiterte Automatisierungen:** Stellt globale Sperrsignale (`input_boolean`) bereit, z. B. um das Scharfschalten einer Alarmanlage zu verhindern oder die Heizung beim Lüften abzuschalten.
* **Power-User Ready:** Unterstützt komplexe Zusatz-Aktionen (z. B. Skripte, Sprachausgaben, NS Panel Warnungen) über integrierte Action-Blöcke.

## 🛠️ Voraussetzungen
Du benötigst in Home Assistant lediglich deine normalen Fenster- und Tür-Kontakte (Sensoren). Um die Daten auf dem Dashboard anzuzeigen, musst du vorab sogenannte "Helfer" anlegen. Eine genaue Schritt-für-Schritt Anleitung findest du in der ausführlichen Dokumentation.

## 🔗 Links
* **[Hilfe & FAQ](https://sno.mb222.de/es-faq/)**
* **[Fehler auf GitHub melden (Issues)](https://github.com/SyncNetOps/SNO-Ha_Bluprint-WindowState)**

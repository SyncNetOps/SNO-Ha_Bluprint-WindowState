# 📘 Benutzerhandbuch: SNO WindowState (Blueprint)

Herzlich willkommen! Diese Anleitung führt dich Schritt für Schritt durch die Installation und Einrichtung. Auch wenn du noch nie mit Helfern in Home Assistant gearbeitet hast, wirst du am Ende eine perfekte Automation besitzen.

---

## Schritt 1: Die Helfer anlegen (Zwingend erforderlich!)
Ein Blueprint kann Texte nicht direkt auf ein Dashboard zaubern – er braucht einen "Speicherort". Dafür nutzen wir Helfer. 

Gehe in Home Assistant auf **Einstellungen ➔ Geräte & Dienste ➔ Helfer** und klicke unten rechts auf **+ Helfer erstellen**. Erstelle exakt diese Helfer:

### 📝 Text-Helfer (Typ: "Text" / `input_text`)
Erstelle diese vier Helfer. 
> ⚠️ **WICHTIGER ZWISCHENSCHRITT:** Klicke nach dem Erstellen auf das Zahnrad-Symbol jedes Text-Helfers und setze die **"Maximale Länge" zwingend auf 255**!
1. Name: `fenster_offen_anzahl`
2. Name: `fenster_offen_kritisch`
3. Name: `fenster_info`
4. Name: `turen_offen_name`

### 🔘 Schalter-Helfer (Typ: "Schalter" / `input_boolean`)
5. Name: `warnung_schalter_kritisch_fenster_turen_offen`
6. Name: `warnung_schalter_gesamt_fenster_turen_offen`

---

## Schritt 2: Blueprint importieren
Klicke in unserer [GitHub Readme](https://github.com/SyncNetOps/SNO-Ha_Bluprint-WindowState) auf den blauen "Import Blueprint" Button oder lade dir die Datei `SyncNetOps/SNO_WindowState.yaml` manuell in deinen Home Assistant `blueprints` Ordner.

Gehe anschließend auf **Einstellungen ➔ Automatisierungen** und erstelle eine neue Automatisierung basierend auf dem "SNO WindowState" Blueprint.

---

## Schritt 3: Die Automatisierung konfigurieren
Hier erkläre ich dir jedes Feld des Blueprints. Felder mit *(Optional)* kannst du einfach leer lassen, wenn du sie nicht brauchst.

### 🪟 / 🪜 / 🚪 Basis-Entitäten (Fenster, Dachfenster, Türen)
* **Was tun:** Wähle hier die Kontaktsensoren deines Hauses in der jeweiligen Kategorie aus.
* **Beispiel:** Wähle unter "Dachfenster" dein `Badfenster OG`. Der Blueprint weiß nun: Dies ist ein Dachfenster. Wenn es regnet, muss hier gewarnt werden!

### ⚠️ Kritische Überwachung
* **Was tun:** Wähle Sensoren aus, die sicherheitsrelevant sind. (Du darfst hier Sensoren wählen, die du oben schon gewählt hast!).
* **Beispiel:** Die `Haustür` oder das `Wohnzimmerfenster (Erdgeschoss)`. Sind diese offen, schlägt das System Alarm.

### 🌧️ Wetter & Aktionen bei Regen
* **Regensensor / Wetterdienst:** Wähle dein lokales Wetter (z.B. `weather.zuhause`) oder einen physischen Regensensor auf dem Dach.
* **Smartphones 1-3:** Wähle die Handys deiner Familie. Fängt es an zu regnen und ein Dachfenster ist noch auf, erhalten diese Geräte eine sofortige Warn-Pushnachricht.
* **Komplexe Aktion 1 & 2:** Für fortgeschrittene Nutzer. Hier kannst du z.B. eintragen, dass Alexa einen Warnsatz spricht oder dein NS-Panel am Eingang aufleuchtet.

### 💾 Text-Ausgabe (für Dashboard)
Hier verknüpfst du die in **Schritt 1** erstellten Helfer mit dem Blueprint:
* Wähle bei *Haupt-Status* deinen Helfer: `fenster_offen_anzahl`
* Wähle bei *Details Kritisch* deinen Helfer: `fenster_offen_kritisch`
* Wähle bei *Details Fenster* deinen Helfer: `fenster_info`
* Wähle bei *Details Türen* deinen Helfer: `turen_offen_name`

### ⚙️ Erweiterte Helfer (Blocker & Zähler)
Hier verknüpfst du die in **Schritt 1** erstellten Schalter:
* Wähle bei *Blocker: Kritisch* deinen Helfer: `warnung_schalter_kritisch_fenster_turen_offen`
* Wähle bei *Blocker: Gesamt* deinen Helfer: `warnung_schalter_gesamt_fenster_turen_offen`

**Klicke auf Speichern! Deine Fenster-Überwachung läuft nun vollautomatisch im Hintergrund.**

---

## 🙋 Häufig gestellte Fragen (FAQ)
*Für tiefgreifende Antworten besuche bitte unsere Webseite: [sno.mb222.de/es-faq/](https://sno.mb222.de/es-faq/)*

1. **Was genau macht SNO WindowState?** Er sammelt die Zustände all deiner Fenster/Türen, bereitet diese formatiert als Text auf und steuert Regen-Warnungen sowie Sperrsignale für andere Automationen.
2. **Warum brauche ich Text-Helfer?** Der Blueprint berechnet die Texte, aber er benötigt die Helfer als "Gefäß", um diese Texte für das Dashboard abzuspeichern.
3. **Warum muss ich das Limit auf 255 Zeichen setzen?** Home Assistant erlaubt standardmäßig nur 100 Zeichen in einem Text-Helfer. Da wir viele Fenster detailliert auflisten, würde das System ohne diese Erhöhung einen Fehler auswerfen.
4. **Stürzt das System ab, wenn ich 30 offene Fenster habe?** Nein. Der Blueprint hat einen Schutz eingebaut. Er schneidet den Text bei 240 Zeichen elegant mit `...` ab, um Abstürze zu 100 % zu verhindern.
5. **Wie reagiert die Regenwarnung?** Sobald dein Regensensor (z.B. Wetter-App oder echter Sensor) auf "Regen" springt, prüft das Skript, ob ein als "Dachfenster" markierter Sensor offen ist. Wenn ja, löst die Warnung aus.
6. **Muss ein Regensensor vom Typ "weather" sein?** Nein, es kann auch ein einfacher Wassermelder (`binary_sensor`) sein, der physisch nass wird.
7. **Warum gibt es "Kritische" Fenster?** Das dient deiner Sicherheit. Ein offenes Badfenster im 1. Stock ist harmlos. Eine offene Haustür ist kritisch. Das Dashboard wird kritische Warnungen rot markieren.
8. **Kann ein Fenster "Normal" und "Kritisch" zugleich sein?** Ja! Wähle es einfach in beiden Kategorien aus. Der Blueprint zählt es intern trotzdem nur als ein (1) offenes Fenster.
9. **Wofür sind die "Blocker" (input_boolean)?** Das sind virtuelle Schalter. Du kannst in Home Assistant sagen: "Wenn *Blocker_Gesamt* auf AN steht, schalte die Heizung aus".
10. **Wie binde ich NS Panels ein?** Unter "Komplexe Aktion 1" kannst du einen Call-Service Befehl hinterlegen, der bei Regen einen Alert an dein NS Panel im Flur schickt.
11. **Warum werden meine Aktionen nicht gespeichert?** Wenn du in den optionalen Feldern "Komplexe Aktion" etwas beginnst, musst du es fertigstellen. Leere Blöcke bitte über den Mülleimer löschen, sonst meckert Home Assistant.
12. **Meine Automation startet nicht, was tun?** Gehe auf *Entwicklerwerkzeuge ➔ YAML ➔ Automatisierungen neu laden*. Öffne danach kurz ein echtes Fenster, um das System aufzuwecken.
13. **Muss ich programmieren können?** Nein. Für die Standardfunktionen klickst du dir alles bequem in der Benutzeroberfläche zusammen.
14. **Sind die Dashboard-Karten Pflicht?** Nein, der Blueprint arbeitet völlig eigenständig im Hintergrund. Die Karten sind nur der optische Bonus!
15. **Wo finde ich Updates?** Auf unserem GitHub Repository oder auf unserer Webseite.

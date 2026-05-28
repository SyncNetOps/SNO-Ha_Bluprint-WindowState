# 📘 Ausführliche Benutzeranleitung: SNO WindowState

Herzlich willkommen! Diese Anleitung ist extra so geschrieben, dass auch Home Assistant Anfänger Schritt für Schritt zu einem perfekten Ergebnis und einem modernen Dashboard kommen.

---

## Schritt 1: Die Helfer anlegen (Wichtig!)
Damit der Blueprint die Namen der offenen Fenster für dein Dashboard speichern kann, müssen wir sogenannte "Helfer" erstellen. 
Gehe in Home Assistant auf **Einstellungen ➔ Geräte & Dienste ➔ Helfer** und klicke unten rechts auf **Helfer erstellen**.

Erstelle exakt diese Helfer mit genau diesen Namen (so passt der spätere Dashboard-Code perfekt!):

**Vier Text-Helfer (Typ: Text / `input_text`):**
1. Name: `fenster_offen_anzahl`
2. Name: `fenster_offen_kritisch`
3. Name: `fenster_info`
4. Name: `turen_offen_name`
*(⚠️ **WICHTIG:** Klicke nach dem Erstellen auf das Zahnrad-Symbol jedes Text-Helfers und setze die **"Maximale Länge" zwingend auf 255**!)*

**Zwei Schalter-Helfer (Typ: Schalter / `input_boolean`):**
5. Name: `warnung_schalter_kritisch_fenster_turen_offen`
6. Name: `warnung_schalter_gesamt_fenster_turen_offen`

---

## Schritt 2: Den Blueprint konfigurieren
Importiere den Blueprint (über den Button in der Readme) und erstelle eine neue Automatisierung. Hier ist die Erklärung, was du wo eintragen musst:

### 🪟 / 🪜 / 🚪 Basis-Entitäten (Fenster, Dachfenster, Türen)
Wähle hier alle Sensoren deines Hauses in der passenden Kategorie aus.
* *Beispiel:* Wähle bei Dachfenstern dein "Badfenster OG" aus. Der Blueprint weiß nun: Wenn es regnet und dieses Fenster offen ist, muss sofort eine Warnung gesendet werden!

### ⚠️ Kritische Überwachung
Hier wählst du Sensoren aus, die sicherheitsrelevant sind. Das können Sensoren sein, die du oben schon gewählt hast.
* *Beispiel:* Wähle hier die "Haustür" und "Balkontür". Wenn diese offen stehen, warnt das Dashboard in roter Farbe!

### 🌧️ Wetter & Aktionen bei Regen
* **Regensensor:** Wähle hier z. B. `weather.zuhause` (dein lokales Wetter) oder einen Regensensor vom Dach.
* **Smartphones 1-3:** Wähle bis zu drei Handys aus. Fängt es an zu regnen und ein Dachfenster ist offen, piepen diese Handys sofort.
* **Komplexe Aktionen (Optional):** Hier kannst du eigene Aktionen bauen. *Beispiel:* Lasse eine Wohnzimmerlampe rot blinken oder dein NS Panel warnen.

### 💾 Text-Ausgabe (für Dashboard)
Hier trägst du die Text-Helfer aus **Schritt 1** ein:
* 1️⃣ Haupt-Status: Wähle `fenster_offen_anzahl`
* 2️⃣ Details Kritisch: Wähle `fenster_offen_kritisch`
* 3️⃣ Details Fenster: Wähle `fenster_info`
* 4️⃣ Details Türen: Wähle `turen_offen_name`

### ⚙️ Erweiterte Helfer (Blocker & Zähler)
Hier trägst du die Schalter-Helfer aus **Schritt 1** ein:
* Blocker: Kritisch: Wähle `warnung_schalter_kritisch_fenster_turen_offen`
* Blocker: Gesamt: Wähle `warnung_schalter_gesamt_fenster_turen_offen`
*(Diese Schalter schalten sich nun wie von Geisterhand ein, sobald ein Fenster offen ist. Du kannst sie in anderen Automatisierungen nutzen, z. B.: "Wenn Blocker Gesamt = AN, dann schalte Heizung AUS".)*

Speichere die Automatisierung. Fertig!

---

## Schritt 3: Dein modernes Dashboard erstellen

Nun bringen wir die Daten wunderschön auf dein Dashboard. Wähle eine der drei Design-Optionen aus und kopiere den Code einfach in eine neue "Manuelle Karte" auf deinem Dashboard. Da wir in Schritt 1 die exakten Helfer-Namen verwendet haben, funktioniert der Code sofort!

### Option A: Standard Nativ (Empfohlen für Anfänger)
Keine Zusatz-Downloads nötig. Eine übersichtliche Karte, die je nach Zustand (Sicher, Offen, Kritisch) ihre Farbe von Grün über Gelb zu Rot ändert.

```yaml
type: markdown
title: 🏠 Fenster & Türen
content: >
  {% if states('input_boolean.warnung_schalter_kritisch_fenster_turen_offen') == 'on' %}
    <ha-alert alert-type="error">⚠️ **Gefahr:** Kritische Fenster offen!</ha-alert>
  {% elif states('input_boolean.warnung_schalter_gesamt_fenster_turen_offen') == 'on' %}
    <ha-alert alert-type="warning">🪟 Fenster oder Türen sind geöffnet.</ha-alert>
  {% else %}
    <ha-alert alert-type="success">🟢 Alles sicher und verschlossen.</ha-alert>
  {% endif %}

  ***

  **Status:** {{ states('input_text.fenster_offen_anzahl') }}

  {{ states('input_text.fenster_offen_kritisch') }}
  
  {{ states('input_text.fenster_info') }}
  
  {{ states('input_text.turen_offen_name') }}

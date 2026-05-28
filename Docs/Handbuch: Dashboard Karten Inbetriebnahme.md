# 🎨 Anleitung: Moderne Dashboard Karten einrichten

Die Daten sind dank des Blueprints nun vorhanden. Jetzt bringen wir sie in einem modernen "Dark/Glass"-Design auf dein Dashboard. Wir bieten dir drei Optionen, die du alle in unserem [GitHub Ordner "Dashboard"](https://github.com/SyncNetOps/SNO-Ha_Bluprint-WindowState/tree/main/Dashboard) findest.

**Grundregel für alle Karten:** Gehe auf dein Dashboard ➔ Oben rechts auf den Stift (Bearbeiten) ➔ Karte hinzufügen ➔ Wähle ganz unten **"Manuell"**. Lösche den dortigen Code und kopiere unseren Code hinein.

---

### Option 1: Native Karte (Empfohlen für Einsteiger)
* **Voraussetzungen:** Keine. Funktioniert sofort in jedem Home Assistant.
* **Code:** Du findest den Code unter *Option A* in der Hauptanleitung oder auf unserer Webseite.
* **Anpassung:** Du musst nichts anpassen, solange du die Helfer exakt so benannt hast wie in unserer Anleitung (`input_text.fenster_offen_anzahl`, etc.).

---

### Option 2: Mushroom Card
* **Voraussetzungen:** Du musst über HACS die Erweiterungen `Mushroom` und `card-mod` installiert haben.
* **Code:** Den Code findest du hier: [`Dashboard/Mushroom Card.yaml`](https://github.com/SyncNetOps/SNO-Ha_Bluprint-WindowState/blob/main/Dashboard/Mushroom%20Card.yaml)
* **Anpassung:** Kopiere den Code in die manuelle Karte. Die Karte erzeugt einen wunderschönen, leicht transparenten Milchglas-Effekt (durch `card_mod`) und färbt das Icon automatisch rot, sobald ein kritisches Fenster offen ist.

---

### Option 3: Bubble Card (High-End Pop-up)
* **Voraussetzungen:** Du musst über HACS die Erweiterung `Bubble Card` (Version 3.2.0 oder neuer!) installiert haben.
* **Konzept:** Diese Lösung besteht aus **ZWEI** Teilen. Einem Button (den du klickst) und einem Pop-up (das dann aufploppt). Beide werden als separate manuelle Karten auf deinem Dashboard platziert!

**Schritt 1: Der Trigger Button**
* Hole dir den Code hier: [`Dashboard/BubbleCard-Popup-Button.yaml`](https://github.com/SyncNetOps/SNO-Ha_Bluprint-WindowState/blob/main/Dashboard/BubbleCard-Popup-Button.yaml)
* Lege auf deinem Dashboard eine manuelle Karte an und füge diesen Code ein. Dies erzeugt den Button. Er zeigt live an, wie viele Fenster offen sind. Klickst du ihn an, leitet er (dank der `navigate` Aktion) auf den Hash `#fenster-details` weiter.

**Schritt 2: Das versteckte Pop-up**
* Hole dir den Code hier: [`Dashboard/BubbleCard-Popup.yaml`](https://github.com/SyncNetOps/SNO-Ha_Bluprint-WindowState/blob/main/Dashboard/BubbleCard-Popup.yaml)
* Lege auf dem *gleichen* Dashboard eine weitere manuelle Karte an und füge diesen Code ein. Im Bearbeitungsmodus siehst du diese Karte, aber sobald du das Dashboard speicherst, wird sie unsichtbar! Sie ploppt erst wunderschön abgedunkelt auf, wenn du auf den Button aus Schritt 1 klickst und zeigt dann alle Details der Text-Helfer.

> **Weitere Design-Tipps und Vorlagen findest du auf unserer Homepage: [sno.mb222.de/es-faq/](https://sno.mb222.de/es-faq/)**

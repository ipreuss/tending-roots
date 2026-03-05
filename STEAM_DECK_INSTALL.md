# Tending Roots auf dem Steam Deck installieren

Tending Roots läuft auf dem Steam Deck als AppImage — ohne zusätzliche Software.

## Kurzanleitung

1. AppImage von [GitHub Releases](https://github.com/ipreuss/tending-roots/releases/latest) herunterladen
2. Ausführbar machen (`chmod +x`)
3. Als Nicht-Steam-Spiel hinzufügen
4. Im Gaming Mode spielen

---

## Schritt-für-Schritt-Anleitung

### 1. In den Desktop Mode wechseln

- **Steam-Taste** drücken → **Ein/Aus** → **Zum Desktop wechseln**

### 2. AppImage herunterladen

- Im Desktop Mode den **Browser** öffnen (Firefox ist vorinstalliert)
- Zu den [Tending Roots Releases](https://github.com/ipreuss/tending-roots/releases/latest) navigieren
- `TendingRoots.AppImage` herunterladen
- Die Datei landet standardmäßig in `~/Downloads/`

### 3. Ausführbar machen

**Option A: Per Dateimanager (Dolphin)**

1. Dolphin öffnen → zu `Downloads` navigieren
2. Rechtsklick auf `TendingRoots.AppImage` → **Eigenschaften**
3. Reiter **Berechtigungen** → Haken bei **Ist ausführbar** setzen
4. Schließen

**Option B: Per Terminal (Konsole)**

```bash
chmod +x ~/Downloads/TendingRoots.AppImage
```

### 4. Testen ob es läuft

Doppelklick auf `TendingRoots.AppImage` im Dateimanager — oder im Terminal:

```bash
~/Downloads/TendingRoots.AppImage
```

Das Spiel sollte direkt starten. Wenn es funktioniert, weiter mit Schritt 5.

### 5. Als Nicht-Steam-Spiel hinzufügen

Damit das Spiel im Gaming Mode erscheint:

1. **Steam** im Desktop Mode öffnen
2. Menü: **Spiele** → **Ein Nicht-Steam-Spiel meiner Bibliothek hinzufügen...**
3. Auf **Durchsuchen...** klicken
4. Unten rechts den Dateifilter von "Desktop-Dateien" auf **Alle Dateien** umstellen
5. Zu `Downloads` navigieren und `TendingRoots.AppImage` auswählen
6. **Öffnen** → **Ausgewählte Programme hinzufügen**

### 6. Zurück zum Gaming Mode

- Doppelklick auf **Return to Gaming Mode** auf dem Desktop
- Tending Roots erscheint jetzt in der Bibliothek unter **Nicht-Steam**

---

## Optional: AppImage an einen besseren Ort verschieben

`~/Downloads/` wird leicht unübersichtlich. Besserer Speicherort:

```bash
mkdir -p ~/Games
mv ~/Downloads/TendingRoots.AppImage ~/Games/
```

Falls das Spiel bereits als Nicht-Steam-Spiel hinzugefügt wurde, den Pfad in Steam aktualisieren:

1. Steam → Bibliothek → Rechtsklick auf **TendingRoots** → **Eigenschaften**
2. Im Feld **Ziel** den neuen Pfad eintragen: `/home/deck/Games/TendingRoots.AppImage`
3. Im Feld **Startverzeichnis** eintragen: `/home/deck/Games/`

---

## Optional: Controller-Layout anpassen

Tending Roots ist ein Touch-/Maus-basiertes Spiel. Auf dem Steam Deck funktioniert die Steuerung über das **Touchscreen** oder den **rechten Trackpad als Maus**.

Empfohlenes Layout:

| Eingabe | Funktion |
|---------|----------|
| Touchscreen | Direkte Tile-Auswahl (am natürlichsten) |
| Rechtes Trackpad | Mauszeiger bewegen |
| R2 (rechter Trigger) | Linksklick / Tile auswählen |
| Start | Menü öffnen |

Um ein eigenes Layout zu konfigurieren:

1. Im Gaming Mode → Tending Roots auswählen
2. **Controller-Symbol** (rechts) → **Layout bearbeiten**
3. Layout nach Wunsch anpassen

---

## Update auf neue Version

1. Neue `TendingRoots.AppImage` von den [Releases](https://github.com/ipreuss/tending-roots/releases/latest) herunterladen
2. Alte Datei ersetzen (gleicher Dateiname → gleicher Pfad)
3. Ausführbar machen nicht vergessen: `chmod +x TendingRoots.AppImage`
4. Steam-Eintrag muss nicht angepasst werden (solange der Pfad gleich bleibt)

---

## Fehlerbehebung

### "Permission denied" beim Starten

```bash
chmod +x ~/Downloads/TendingRoots.AppImage
```

### AppImage startet nicht (FUSE-Fehler)

Ältere SteamOS-Versionen haben eventuell kein FUSE installiert. Workaround:

```bash
~/Downloads/TendingRoots.AppImage --appimage-extract-and-run
```

Oder FUSE nachinstallieren (benötigt `passwd` für den deck-User):

```bash
sudo steamos-readonly disable
sudo pacman -S fuse2
sudo steamos-readonly enable
```

### Spiel erscheint nicht im Gaming Mode

- Prüfe ob der Steam-Eintrag korrekt ist (Schritt 5)
- Prüfe ob der Pfad zum AppImage stimmt (besonders nach Verschieben)
- Steam neu starten: Im Desktop Mode Steam beenden und neu öffnen

### Touchscreen reagiert nicht

Touchscreen funktioniert nur im Gaming Mode nativ. Im Desktop Mode nutzt das Spiel die Maus als Eingabe.

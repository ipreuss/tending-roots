# Tending Roots auf dem Steam Deck installieren

Tending Roots läuft auf dem Steam Deck als AppImage — eingerichtet über ein einmaliges Setup-Skript, das den Namen "Tending Roots" und die Bibliotheksbilder direkt in Steam einträgt.

## Kurzanleitung

1. `TendingRoots-SteamDeck-<version>.tar.gz` von [GitHub Releases](https://github.com/ipreuss/tending-roots/releases/latest) herunterladen
2. Entpacken (Doppelklick in Dolphin oder `tar xzf ...`)
3. Steam vollständig schliessen
4. `./setup-steam-deck.sh` einmalig ausführen
5. Steam neu starten → Tending Roots erscheint in der Bibliothek mit Name und Artwork

---

## Schritt-für-Schritt-Anleitung

### 1. In den Desktop Mode wechseln

- **Steam-Taste** drücken → **Ein/Aus** → **Zum Desktop wechseln**

### 2. Setup-Tarball herunterladen

- Im Desktop Mode den **Browser** öffnen (Firefox ist vorinstalliert)
- Zu den [Tending Roots Releases](https://github.com/ipreuss/tending-roots/releases/latest) navigieren
- `TendingRoots-SteamDeck-<version>.tar.gz` herunterladen
- Die Datei landet standardmäßig in `~/Downloads/`

### 3. Entpacken

**Option A: Per Dateimanager (Dolphin)**

Rechtsklick auf die `.tar.gz`-Datei → **Archiv extrahieren** → **Extrahieren hier**. Es entsteht ein Ordner `tending-roots-steam-deck/`.

**Option B: Per Terminal (Konsole)**

```bash
cd ~/Downloads
tar xzf TendingRoots-SteamDeck-*.tar.gz
cd tending-roots-steam-deck
```

### 4. Steam schliessen

**Wichtig:** Das Setup-Skript schreibt in Steams Konfigurationsdateien. Steam muss komplett geschlossen sein, sonst überschreibt Steam die Änderungen beim Beenden.

- Steam-Taste → **Steam beenden** (falls noch geöffnet)

### 5. Setup-Skript ausführen

**Option A: Per Dateimanager (Dolphin)**

1. Dolphin öffnen → zum entpackten Ordner `tending-roots-steam-deck/` navigieren
2. Rechtsklick auf `setup-steam-deck.sh` → **Ausführen** (oder Doppelklick, wenn Ausführungs-Rechte gesetzt sind)

**Option B: Per Terminal (Konsole)**

```bash
cd ~/Downloads/tending-roots-steam-deck
./setup-steam-deck.sh
```

Das Skript:
- Legt einen "Tending Roots"-Eintrag in Steam an (kein manuelles "Nicht-Steam-Spiel hinzufügen" nötig)
- Kopiert Capsule- und Header-Artwork in Steams Bibliotheks-Ordner
- Installiert eine `.desktop`-Verknüpfung

Zum Abschluss erscheint: *"Fertig. Starte Steam neu, damit Tending Roots in der Bibliothek erscheint."*

### 5b. Option B — Manueller Weg (Fallback, falls Setup-Skript fehlschlägt)

Sollte das Skript aus irgendeinem Grund nicht laufen, kann das Spiel weiterhin manuell als Nicht-Steam-Spiel hinzugefügt werden:

1. `TendingRoots.AppImage` aus dem entpackten Ordner ausführbar machen: `chmod +x TendingRoots.AppImage`
2. **Steam** im Desktop Mode öffnen
3. Menü: **Spiele** → **Ein Nicht-Steam-Spiel meiner Bibliothek hinzufügen...**
4. Auf **Durchsuchen...** klicken
5. Unten rechts den Dateifilter von "Desktop-Dateien" auf **Alle Dateien** umstellen
6. Zum entpackten Ordner navigieren und `TendingRoots.AppImage` auswählen
7. **Öffnen** → **Ausgewählte Programme hinzufügen**

Bei dieser Variante fehlen Name und Bibliotheksbilder — sie können manuell über den Bibliotheks-Eintrag (Rechtsklick → **Eigenschaften**) gesetzt werden.

### 6. Zurück zum Gaming Mode

- Doppelklick auf **Return to Gaming Mode** auf dem Desktop
- Tending Roots erscheint jetzt in der Bibliothek mit Name und Artwork

---

## Optional: Setup-Ordner an einen besseren Ort verschieben

`~/Downloads/` wird leicht unübersichtlich. Besserer Speicherort:

```bash
mkdir -p ~/Games
mv ~/Downloads/tending-roots-steam-deck ~/Games/
```

**Skript erneut ausführen, um den Eintrag zu aktualisieren** — das Skript erkennt den geänderten Pfad automatisch und aktualisiert den bestehenden Bibliotheks-Eintrag ohne Duplikat:

```bash
cd ~/Games/tending-roots-steam-deck
./setup-steam-deck.sh
```

---

## Controller-Steuerung

Tending Roots unterstützt native Controller-Steuerung — das Spiel erkennt automatisch, wenn ein Gamepad verwendet wird. Auf dem Steam Deck funktioniert die Steuerung direkt ohne weitere Konfiguration.

**Native Controller-Belegung:**

| Eingabe | Funktion |
|---------|----------|
| D-Pad / Linker Stick | Cursor bewegen (Board-Navigation) |
| A | Tile auswählen / Bestätigen |
| B | Auswahl aufheben / Dialog überspringen |
| Start | Menü / Einstellungen öffnen |

Alternativ funktionieren auch **Touchscreen** (direkte Tile-Auswahl) und **rechtes Trackpad als Maus** — das Spiel wechselt automatisch zwischen den Eingabemodi.

### Optional: Controller-Layout anpassen

Falls eine eigene Belegung gewünscht wird:

1. Im Gaming Mode → Tending Roots auswählen
2. **Controller-Symbol** (rechts) → **Layout bearbeiten**
3. Layout nach Wunsch anpassen

---

## Update auf neue Version

1. Neuen `TendingRoots-SteamDeck-<version>.tar.gz` von den [Releases](https://github.com/ipreuss/tending-roots/releases/latest) herunterladen
2. Entpacken über den alten Ordner (oder daneben)
3. `./setup-steam-deck.sh` erneut ausführen — der Eintrag wird in-place aktualisiert, Bibliotheks-Artwork ebenfalls
4. Steam neu starten

---

## Fehlerbehebung

### "Permission denied" beim Starten von `setup-steam-deck.sh`

```bash
chmod +x setup-steam-deck.sh
```

### AppImage startet nicht (FUSE-Fehler)

Ältere SteamOS-Versionen haben eventuell kein FUSE installiert. Workaround:

```bash
./TendingRoots.AppImage --appimage-extract-and-run
```

Oder FUSE nachinstallieren (benötigt `passwd` für den deck-User):

```bash
sudo steamos-readonly disable
sudo pacman -S fuse2
sudo steamos-readonly enable
```

### Setup-Skript meldet "Steam läuft noch"

Steam ist noch aktiv. Komplett beenden (nicht nur Fenster schliessen):

- Steam-Taste → **Steam beenden**, oder im Desktop Mode Systray-Symbol → **Beenden**

Danach das Skript erneut starten.

### Spiel erscheint nicht im Gaming Mode

- Prüfe ob das Setup-Skript erfolgreich lief (keine Fehlermeldung am Ende)
- Steam wirklich beenden und neu starten — ein Library-Reload reicht oft nicht
- Bei bestehendem (manuell angelegtem) Nicht-Steam-Eintrag: `./setup-steam-deck.sh` räumt veraltete Einträge automatisch auf; erneut ausführen

### Touchscreen reagiert nicht

Touchscreen funktioniert nur im Gaming Mode nativ. Im Desktop Mode nutzt das Spiel die Maus als Eingabe.

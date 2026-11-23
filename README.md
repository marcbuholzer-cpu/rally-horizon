# Rally Horizon

**Rally Horizon** ist ein eigenständiges 3D-Rally-Spiel für den Browser, vollständig gebündelt in einer einzigen HTML-Datei (`index.html`). Es unterstützt sowohl einen **1-Spieler-Zeitjagd-Modus** mit Streckenrekorden als auch einen lokalen **2-Spieler-Splitscreen-Modus** auf vier thematisch unterschiedlichen Strecken.

---

## Features

- **1-Spieler & 2-Spieler Splitscreen:** Alleine auf Bestzeitenjagd oder zu zweit am selben Bildschirm (inkl. Fahrzeugkollisionen, Rammen & Funkenflug).
- **4 spielbare Welten** mit individueller Physik, Gravitation, Beleuchtung und dynamischen Gefahren:

| Etappe | Strecke | Gravitation | Strecken-Highlights & Gefahren |
| :--- | :--- | :--- | :--- |
| **01** | **Grand Canyon** | `9,81 m/s²` | 14 enge Steilwandkurven, Holz-Hängebrücke, 4× 360°-Schrauben, 360°-Looping, 5 Schanzen mit Landungsrampe, rollende Felsbrocken & Seitenwind-Böen |
| **02** | **Mond** *(Mare Tranquillitatis)* | `1,62 m/s²` *(Low-G)* | 14 Mond-Steilwandkurven, 4× 360°-Schrauben, 360°-Looping, Astronaut, Rakete & Satellit, herabfallende Meteoriten & eisige Rutschzonen |
| **03** | **Smaragd-Dschungel** | `9,81 m/s²` | Holz-Strecke mit Lianen, Bäumen, Flüssen, Affen & Vögeln, Holz-Hängebrücke, 4× 360°-Holz-Schrauben, 360°-Looping, rutschige Moos-Planken, morsche Bretter & Baumstamm-Schikanen |
| **04** | **Candy Land** *(Regenbogen-Candy)* | `9,81 m/s²` | Regenbogen-Süssigkeiten-Strecke mit Zuckerstangen-Rändern, Waffel-Hängebrücke über einen Regenbogen-Sirup-Fluss, 4× 360°-Schrauben, 360°-Looping, 5 Schanzen, Regenbogen-Glaces & Lollipops als Pflanzen, Riesen-Donuts, rollende Riesen-Bonbons, Zuckerguss-Rutschzonen & Zuckerstangen-Schikanen |

- **Kameraperspektiven:** Dynamische Third-Person- und First-Person-Kamera (inkl. Loop- und Schrauben-Ausrichtung).
- **Rally-HUD:** Live-Timer, Bestzeit/Streckenrekord, Ziel-Kompass mit Distanz- und Fortschrittsanzeige, Minimap, Tacho, Gang- & Drehzahlanzeige sowie Status-Indikatoren (`GEFAHR`, `IN DER LUFT`, `DRIFT`, `HOLPRIG`, `GERAMMT!`).
- **Zielauswertung:** Zeigt Gesamtzeit, Rekord-Delta, Höchstgeschwindigkeit und weitesten Sprung (im 2P-Modus als direkter Duell-Vergleich).
- **Audio & Bestzeiten:** Synthetisierter Sound über die Web Audio API (stummschaltbar) sowie automatische Speicherung der persönlichen Streckenrekorde im Browser (`localStorage`).

---

## Spielen / Starten

Da das gesamte Spiel inklusive Engine und Texturen in `index.html` enthalten ist, sind weder ein Build-Schritt noch eine Internetverbindung erforderlich:

1. **Direkt im Browser öffnen:** `index.html` herunterladen oder das Repository klonen und die Datei per Doppelklick in einem modernen Browser mit WebGL-Unterstützung öffnen.
2. **Optional über einen lokalen Webserver:**
   ```bash
   python3 -m http.server 8000
   ```
   Anschließend `http://localhost:8000` im Browser aufrufen.
3. **Optional via GitHub Pages:** Das Repository kann direkt über GitHub Pages (`main`-Branch, Root-Verzeichnis) als Web-App bereitgestellt werden.

---

## Steuerung

### 1-Spieler-Modus

| Taste | Aktion |
| :--- | :--- |
| `W` `A` `S` `D` oder `↑` `←` `↓` `→` | Gas, Bremse & Lenken |
| `←`/`→` + `↓`/`S` oder `Space` | Driften |
| `C` | Kamera wechseln (First / Third Person) |
| `R` | Fahrzeug zurück auf die Strecke setzen |

### 2-Spieler-Modus (Splitscreen)

| Aktion | Spieler 1 (Links · Blau `#5`) | Spieler 2 (Rechts · Rot `#8`) |
| :--- | :--- | :--- |
| **Fahren & Lenken** | `W` `A` `S` `D` | `↑` `←` `↓` `→` |
| **Driften** | `A`/`D` + `S` oder `Shift` | `←`/`→` + `↓` oder `Enter` |
| **Kamera wechseln** | `C` | `N` |
| **Zurück auf die Strecke** | `R` | `P` |

### Allgemeine Tasten

| Taste | Aktion |
| :--- | :--- |
| `1` / `2` / `3` / `4` | Direkt zur Strecke wechseln (Grand Canyon / Mond / Dschungel / Candy Land) |
| `Backspace` | Aktuelle Etappe neu starten |
| `Esc` | Startmenü öffnen |
| `M` | Ton an / aus |
| `Enter` / `Space` *(im Startmenü)* | Rennen starten |

---

## Technischer Aufbau (`index.html`)

Das Projekt besteht aus einer einzelnen, in sich geschlossenen Datei (`index.html`, ca. 1,75 MB):

- **Rendering:** WebGL mit eingebettetem Three.js.
- **Texturen:** 12 eingebettete PBR-Texturen (Albedo-, Normal- und Roughness-Maps für Grand Canyon, Mond, Dschungel-Boden und Dschungel-Holz) als Base64-Data-URIs in `window.__EMBEDDED_TEXTURES__`.
- **Audio:** Prozedurale Klangerzeugung über die Web Audio API.
- **Persistenz:** Lokale Speicherung der Bestzeiten je Strecke unter dem `localStorage`-Schlüssel `rally_horizon_best_<trackId>`.

# M-AI – Markov-KI für Max for Live

**Ein Echtzeit-Improvisationspartner für Ableton Live, basierend auf einer Markov-Kette erster Ordnung.**

*🇬🇧 [English version](README.md)*

M-AI ist ein Max-for-Live-MIDI-Effekt, der zuhört, was gespielt wird, lernt, welche Töne auf welche folgen, und darauf mit eigenen melodischen Phrasen antwortet – synchron zum Tempo in Ableton. Es braucht kein Vortraining, keinen Datensatz und keine stilistische Vorbereitung: Das gesamte musikalische Material stammt direkt aus dem Live-Spiel.

Das Device wurde für das Stück **_A Duet of Intelligences_** entwickelt – eine Komposition für Pianistin, Komponist\*innen und ein KI-Instrument auf einem Disklavier – und ist im Paper auf der **AIMC 2026** beschrieben (siehe [Hintergrund & Paper](#hintergrund--paper)).

![M-AI Dual-Oberfläche](docs/images/interface-dual.jpg)

---

## Inhalt

| Datei | Beschreibung |
|---|---|
| [`M-AI/MP_M-AI.amxd`](M-AI/MP_M-AI.amxd) | **Dual-Version** – zwei unabhängige Markov-Modelle mit je eigenem Rhythmusgenerator (die in der Aufführung verwendete Version). |
| [`M-AI/MP_AI_Mono.amxd`](M-AI/MP_AI_Mono.amxd) | **Mono-Version** – ein einzelnes Markov-Modell. |
| [`M-AI/Piano Example/`](M-AI/Piano%20Example) | Beispiel-Set für Ableton Live 12 mit Dual-Device und Piano. |
| [`M-AI/README.txt`](M-AI/README.txt) | Ursprüngliche Kurzanleitung. |
| [`docs/paper/`](docs/paper) | Paper *A Duet of Intelligences: Human–AI Co-Creation in Live Piano Performance*. |

![M-AI Mono-Oberfläche](docs/images/interface-mono.jpg)

---

## Voraussetzungen

- **Ableton Live** mit **Max for Live** (Live Suite oder Standard + Max for Live). Das Beispielset wurde mit Live 12 gespeichert, die Devices mit Max 9 erstellt.
- Das Max-External **`ml.markov`** aus dem *ml.\**-Toolkit von Benjamin D. Smith & Guy E. Garnett („Unsupervised Play: Machine Learning Toolkit for Max“, 2012). Es ist **nicht** im Device enthalten und muss separat installiert werden:
  1. Max öffnen (z. B. über *Edit* am Device in Live).
  2. *File → Show Package Manager*, nach **ml.star** suchen und installieren.
  3. Live neu starten.

> Erscheint im Device ein rotes/gestricheltes `ml.markov`-Objekt oder werden keine Noten erzeugt, fehlt das External.

---

## Installation & Schnellstart

1. Repository herunterladen (grüner **Code**-Button → **Download ZIP**) und entpacken.
2. `ml.markov` installieren (s. o.).
3. Entweder `M-AI/Piano Example/Piano Example.als` öffnen **oder** selbst einrichten:
   - `MP_M-AI.amxd` oder `MP_AI_Mono.amxd` als **erstes Gerät** auf eine **MIDI-Spur** ziehen.
   - Danach ein MIDI-Instrument einfügen (Sampler, Synth, Piano …).
   - Spur scharf schalten bzw. Monitoring auf *In*, damit das MIDI-Keyboard das Device erreicht.
4. Empfohlene Einstellungen setzen (siehe unten) und **Wiedergabe oder Aufnahme starten** – der Rhythmusgenerator läuft über den Live-Transport.
5. Spielen. Nach **8 Noten** (*Size*) berechnet das Device ein Modell und beginnt, Phrasen aus den gespielten Tonhöhen zu generieren.

Alle Einstellungen können während der Laufzeit verändert werden; auch Tempoänderungen werden berücksichtigt.

---

## Parameter

### Markov Model

| Regler | Funktion | Empfohlen |
|---|---|---|
| **Enable** | Aktiviert/deaktiviert die Ausgabe Markov-generierter Noten | An |
| **Learn** | Aktiviert/deaktiviert das periodische Lernen des Modells | An |
| **Size** | Nach wie vielen Eingangsnoten ein neues Modell berechnet wird | 8 |
| **Dump** | Leert alle Noten aus dem Zwischenspeicher | – |
| **Reset** | Setzt das Markov-Modell zurück | – |

### Rhythm Generator

| Regler | Funktion | Empfohlen |
|---|---|---|
| **1/1** | Ganze Noten | Aus |
| **1/2** | Halbe Noten | Aus |
| **1/4** | Viertelnoten | An |
| **1/8** | Achtelnoten | An |
| **Density** | Prozentanteil von Tönen gegenüber Pausen | 75 |

### Miscellaneous

| Regler | Funktion | Empfohlen |
|---|---|---|
| **Vel.** | Velocity der ausgegebenen Noten | 100 |
| **8va. Shift** | Transponiert die Ausgabe um *n* Oktaven nach oben/unten | 0 |
| **Pass-Through** | Gibt das eingehende MIDI-Signal an das Instrument weiter | An |

In der Dual-Version gibt es *Markov Model*, *Rhythm Generator* und *Misc.* doppelt (1 = gelb, 2 = blau): So können zwei KI-Stimmen mit unterschiedlichem Verhalten auf denselben Input reagieren.

---

## Funktionsweise

```
MIDI in ──► Notenpuffer (Size) ──► ml.markov (lernt Übergänge)
                                        │
Live-Transport ──► Rhythmusgenerator ───┤  (Notenwert, Density)
                                        ▼
                      nächste Tonhöhe ──► Velocity / Oktave ──► MIDI out
```

- Jede gespielte Note ist ein **Zustand**. Aus den gepufferten Noten wird gezählt, wie oft eine Note auf eine andere folgt. Beispiel: Bei **E G E B E G** und aktueller Note **E** folgt **G** mit 67 % und **B** mit 33 % Wahrscheinlichkeit.
- Ein **Rhythmusgenerator** auf Basis des Max-Objekts `transport` bestimmt, *wann* eine Note erklingt (Zufallsauswahl unter den aktiven Notenwerten, Pausen gemäß *Density*). So bleibt die Ausgabe immer synchron zum Live-Tempo.
- Die erzeugte Tonhöhenfolge wird mit gewählter Velocity und Oktavlage in MIDI-Noten umgewandelt.

---

## Hintergrund & Paper

M-AI entstand für **_A Duet of Intelligences_**, ein Stück für eine Pianistin und ein von dieser KI gesteuertes Disklavier. Im grafisch notierten Schlussteil improvisiert die Pianistin mit der KI, während zwei Komponist\*innen die Parameter des Devices live steuern – Tempo, Rhythmus, Velocity und Oktave – und so die Balance zwischen Annäherung und Reibung verschieben.

> Veronika Reutz Drobnić & Julian Brandhofer (2026). *A Duet of Intelligences: Human–AI Co-Creation in Live Piano Performance.* Proceedings of the 7th Conference on AI Music Creativity (AIMC 2026), Berlin.

- Paper (PDF): [`docs/paper/A-Duet-of-Intelligences_AIMC2026.pdf`](docs/paper/A-Duet-of-Intelligences_AIMC2026.pdf)
- Komponistin: Veronika Reutz Drobnić – <https://veronikareutz.com/>

Bei Verwendung von M-AI bitte das Paper zitieren (GitHubs Button **„Cite this repository“** nutzt [`CITATION.cff`](CITATION.cff)).

---

## Credits

- **Device & Implementierung:** Julian Brandhofer
- **Komposition & Konzept _A Duet of Intelligences_:** Veronika Reutz Drobnić & Julian Brandhofer
- Institut für Musikinformatik und Musikwissenschaft, Hochschule für Musik Karlsruhe
- `ml.markov`: B. D. Smith & G. E. Garnett, *Unsupervised Play: Machine Learning Toolkit for Max* (2012)

## Lizenz

[![Lizenz: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/deed.de)

Die Max-for-Live-Devices, das Beispielset und die Dokumentation stehen unter [CC BY-NC 4.0](LICENSE): Nutzung, Weitergabe und Veränderung sind mit Namensnennung für **nicht-kommerzielle** Zwecke erlaubt. Musik, die mit den Devices entsteht, gehört dir. Für eine kommerzielle Nutzung der Devices selbst bitte Kontakt aufnehmen.

Für das Paper in `docs/paper/` gelten die Rechte der Autor\*innen bzw. der AIMC-Proceedings. `ml.markov` unterliegt der Lizenz seiner Autoren.

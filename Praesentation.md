---
theme: default
class: text-center
---

# Endless Dusk
**Finale Präsentation SWE**  
Team-Projekt (Beric, Mika, Max, Timo, Erik, Felix)

---
class: text-center
---

## 1. Live Demo - "Endless Dusk" in Aktion!

*(Wir starten direkt ins Spiel, um euch unser Projekt vorzustellen)*

**Ablauf-Idee für die Demo:**
1. Start im **Main Menu** (Zeigen der Parallax-Hintergründe & Menü-Führung).
2. **Gameplay:** Bewegen, Ausweichen, automatische Angriffe der Start-Waffen (z.B. Axt).
3. **Core-Mechanic:** XP-Orbs sammeln und ein **Level Up** auslösen.
4. Auswahl eines zufälligen Power-Ups (neue Waffe wie SMG oder Stats-Bonus).
5. Kurzes Überleben einer massiven Gegner-Welle (Wave Spawner mit steigender Intensität).
6. Absichtliches Sterben, um den **Game Over Screen** (Kills & Run-Stats) zu zeigen.

---
class: text-left
---

## 2. Worum es ging & Motivation (Der Pitch)

**Die Vision:**  
Ein 2D "Auto-Battler / Rogue-lite" im Pixelstil, stark angelehnt an *Vampire Survivors*. 

**Motivation:**
- **Ziel:** Schnelle, spaßige Runden für zwischendurch. "Einfach zu lernen, schwer zu meistern".
- **Core Loop:** Spieler kämpft gegen endlose Gegnerwellen, sammelt XP, entwickelt Fähigkeiten und versucht so lange wie möglich zu überleben.
- **Wiederspielwert:** Unendliche Kombinationsmöglichkeiten durch zufällige Waffen-Drops und Power-Ups.

**Geplanter Umfang vs. Umsetzung:**
- Wir haben uns vorgenommen: 2-3 Maps, 2-3 Charaktere und 10-15 Waffen zu entwickeln.

---

## 3. Wie funktioniert das System? (Architektur & Tools)

**Unsere Toolchain:**
- **Engine:** Godot 4 & GDScript für Logik und Game-Engine.
- **Art & Sound:** GIMP / Krita für Pixelart. Audacity / FL Studio für Musik und SFX.

**Architektur im Code:**
- **Entities:** Eigenständige Skripte für `Player`, `BaseEnemy`, `Health` und `XP`.
- **Systeme & Manager:** 
  - `game_manager.gd`: Verwaltet den globalen Game-State (Playing, Paused, Level_Up, Dead).
  - `wave_handler.gd`: Steuert dynamisch den Schwierigkeitsgrad und Gegner-Spawns.
- **Waffen-System:** Modular aufgebaute Waffen, die über unser Level-Up-System (Zufalls-Karten) skalieren.
- **UI:** Dynamische Menüs, die entkoppelt über Godot-Signals agieren.

---
class: text-left
---

## 4. Zeigen des Codes (Code-Struktur & Highlights)

*(Hier wechseln wir in VS Code / Godot Editor - ca. 5-10 Minuten)*

**Was wir im Code zeigen:**
- **Struktur:** Kurzer Blick auf die strikte Ordner-Trennung (`entities/`, `environments/`, `systems/`, `weapons/`, `tests/`).
- **Highlight 1: Globals & State:** Einblick in `game_manager.gd` (Wie elegant die Game-States per Enums gesteuert werden).
- **Highlight 2: Das Waffen-System:** Öffnet eine der Waffen (z.B. `void_orbs.gd`) und zeigt, wie die `apply_level_upgrade()` Funktion Schaden und Effekte manipuliert.
- **Highlight 3: Unit Tests (GdUnit4):** Zeigt kurz `tests/test_game_manager.gd`. Wir erklären unser "Deep Mocking": Wir instanziieren nicht das schwere Spiel, sondern nutzen saubere Dummy-Nodes (z.B. `CanvasLayer.new()`), um Abhängigkeits-Crashes zu vermeiden.

---

## 5. Lessons Learned & Fazit (Recap)

**Lessons Learned:**
- **Godot Node-Abhängigkeiten:** Wir haben gelernt, wie schnell UI-Nodes crashen können, wenn Pfade nicht stimmen. Die Lösung war sauberes Mocking bei den Tests und konsequente Signal-Nutzung.
- **Git & Teamwork:** Strenge Branching-Modelle (wie unsere PR-Branches) und eine klare Aufgabenteilung (z.B. UI, Entities, Environments getrennt) waren Gold wert, um Merge-Konflikte zu vermeiden.

**Fazit:**
*Endless Dusk* war ein großer Erfolg. Wir haben nicht nur ein spielbares, spaßiges Top-Down-Game entwickelt (exportierbar für PC, Mac und Linux), sondern auch stark auf Clean Code und Testabdeckung geachtet. Das technische Fundament ist stabil und voll erweiterbar für geplante Features wie Mobile-Ports oder DLCs!

---
class: text-center
---

# Vielen Dank für eure Aufmerksamkeit!
**Gibt es noch Fragen zum Code oder Spiel?**

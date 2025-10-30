# Tech Stack – Endless Dusk

## Overview
Endless Dusk ist ein 2D-Roguelite-Auto-Battler im Retro-Pixelstil, entwickelt mit Fokus auf Performance, kurze Spielsessions und hohe Wiederspielbarkeit.  
Der Tech Stack wurde so gewählt, dass er schnelles Prototyping, einfache Team-Kollaboration und Cross-Platform-Deployment ermöglicht.

---

## Core Technologies

### 1. Programming Language
- **GDScript (Godot Engine)** – Hauptsprache für Gameplay-Logik  
  → Leichtgewichtig, Python-ähnlich, ideal für Rapid Prototyping.  
- **C# (optional)** – für performancekritische Module oder komplexere Systeme.  

### 2. Game Engine
- **Godot 4.5**  
  → Open-Source-Engine mit exzellenter 2D-Performance, integrierter Physik-Engine, Tilemap-System und Signal-basiertem Event-Handling.  
  → Einfache Export-Pipelines auf Windows, Linux, macOS sowie Mobile-Plattformen.  

### 3. Frameworks & Libraries
- **Godot Input System** – Steuerung und Gamepad-Support  
- **Godot Animation Player / Tween System** – für Animationen und Übergänge  
- **Godot Audio Server** – Soundeffekte und Musikverwaltung  
- **OpenSimplexNoise (built-in)** – zufällige Spawns und Map-Variation  

---

## Asset & Content Pipeline

### Art & Animation
- **GIMP / Krita** – Erstellung und Bearbeitung von Pixel-Art  
- **Aseprite (optional)** – Frame-basierte Animationen  
- **TexturePacker** – Spritesheet-Optimierung  

### Sound & Music
- **Audacity** – Aufnahme und Bearbeitung von SFX  
- **FL Studio** – Komposition dynamischer Musik-Loops  
- **Godot AudioStreamPlayer** – Playback & Lautstärkemanagement  

---

## Software Architecture
- **Monolithische Architektur** mit modularen Szenen-Komponenten  
  → Jede Spielfunktion (Player, Gegner, Waffe, UI) als eigene Scene/Node.  
- **Event-Driven Design** über Godots Signal-System  
  → Lose Kopplung, einfache Erweiterbarkeit.  
- **ECS-ähnliches Pattern (Entity-Component-System)** für flexible Charakter- und Waffen-Konfiguration.  

---

## Infrastructure & DevOps
- **Version Control:** Git + GitHub (Team-Kollaboration & Issue-Tracking)  
- **Continuous Integration:** GitHub Actions (automatische Builds & Tests)  
- **Build Tools:** Godot-CLI (Exportskripte für PC-Versionen)  
- **Project Management:** Google Docs (Sprint-Planung, Roadmap)  
- **Distribution:**  
  - *PC:* Steam / itch.io  
  - *Mobile (später):* Google Play Store / iOS App Store  

---

## Testing & QA
- **Unit Tests:** Godot Unit Test Framework  
- **Playtesting:** Manuell + automatisierte Simulationen von Gegnerwellen  
- **Performance Monitoring:** Godot Profiler, Frame-Time Analyzer  
- **Versioned Builds:** Alpha → Beta → Release Candidate  

---

## Development Tools
- **IDE:** Godot Editor (integrierter Code-, Scene- und Asset-Editor)  
- **Task Management:** Kanban (https://cryptpad.fr/kanban/#/2/kanban/view/q+mij7VzmCB31MUCxd2+zNuilajBaCrM0lGfwvyCix8/)
- **Communication:** Discord/WhatsApp (Dev-Chat, Stand-ups, Feedback)  

---

## Decision Rationale
Der Stack wurde gewählt, um:
1. **Schnelle Iteration** durch ein integriertes Tool-Ökosystem zu ermöglichen.  
2. **Cross-Platform-Export** ohne externe Abhängigkeiten zu sichern.  
3. **Kostenfrei & Open Source** zu bleiben, um Budget und Lizenzrisiken zu vermeiden.  
4. **Leichte Einarbeitung** für alle Teammitglieder mit unterschiedlichem Skill-Level zu gewährleisten.  

Alternative Optionen wie Unity oder Unreal wurden verworfen, da:
- Unity komplexere Lizenzmodelle hat und Overhead für ein 2D-Projekt erzeugt.  
- Unreal Engine für ein leichtgewichtiges 2D-Roguelite überdimensioniert ist.  

---

## Summary
Der gewählte Tech Stack unterstützt die Vision von *Endless Dusk*:  
ein performantes, erweiterbares und optisch kohärentes 2D-Spiel mit minimalem technischen Ballast.  
Er ermöglicht schnelle Entwicklung, einfache Team-Kollaboration und eine klare Skalierbarkeit hin zu weiteren Plattformen.

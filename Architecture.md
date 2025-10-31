# Software Architecture – Endless Dusk

## 1. Introduction
*Endless Dusk* ist ein 2D-Pixelart Roguelite Autobattler, inspiriert von *Vampire Survivors*. Das Spiel ist auf Performance, kurze Spielsessions und hohe Wiederspielbarkeit ausgelegt.  
Die Architektur unterstützt schnelles Prototyping, modulare Erweiterbarkeit und Cross-Platform-Deployment.

> Ziel der Architektur: Lose gekoppelte, modulare Systeme, einfache Erweiterbarkeit und klare Trennung von Spielmechanik, Präsentation und Datenlogik.

---

## 2. Architectural Overview

### 2.1 Monolithic + Modular Node-Based Design
- **Monolithische Hauptstruktur:** Ein Projekt/Build, der das komplette Spiel enthält.  
- **Modulare Komponenten:** Jede Spielfunktion (Player, Gegner, Waffen, UI, Level) als eigene Godot Scene/Node.  
- **Lose Kopplung:** Kommunikation über Godot Signals (Event-Driven Design).

### 2.2 ECS-ähnliches Pattern
- **Entities:** Charaktere, Gegner, Projektile, Items.  
- **Components:** Verhalten, Stats, AI-Module, Waffen, Buffs.  
- **Systems:** Spiel-Logik wie Kampf, Bewegung, Kollisionsabfrage, Level-Management.

### 2.3 Layered View
| Layer | Responsibilities |
|-------|-----------------|
| Presentation | UI, HUD, Animations, Audio |
| Gameplay | PlayerController, EnemyAI, WeaponSystem, ECS-Management |
| Physics/Engine | Godot Physics, Tilemaps, Collision detection |
| Data | Save/Load, Progression, Stats, PlayerPrefs |
| Infrastructure | Event-Bus (Signals), ResourceLoader, Asset Management |

---

## 3. Core Components

### 3.1 Player Module
- **Scene/Node:** `Player.tscn`
- **Components:** Health, Movement, Weapons, Abilities, Buffs
- **Signals:** `onPlayerDamage`, `onAbilityUsed`

### 3.2 Enemy Module
- **Scene/Node:** `Enemy.tscn`
- **Components:** AIBehavior, Health, LootDrop
- **Signals:** `onEnemyDeath`, `onEnemySpawn`

### 3.3 Weapon System
- **Scene/Node:** `Weapon.tscn`
- **Components:** Projectile, Damage, Effects, Cooldowns
- **Signals:** `onWeaponFire`, `onProjectileHit`

### 3.4 Level & Spawn Manager
- **Responsibilities:** Procedural Spawn, Wave Management, Map Generation via OpenSimplexNoise  
- **Signals:** `onWaveStart`, `onWaveEnd`

### 3.5 UI & Audio
- **UI Nodes:** HUD, Menus, Score, Health Bars  
- **Audio Nodes:** Music, SFX, Event-driven feedback (via AudioStreamPlayer)

---

## 4. Event Flow / Signal System
- Signals ersetzen klassische Controller-Kommunikation.
- Beispiele:
  - Player hits Enemy → Enemy emits `onDamageTaken` → WeaponSystem updates  
  - Enemy dies → Enemy emits `onEnemyDeath` → LevelManager spawns loot & updates score  
  - Player collects item → Item emits `onCollected` → Player updates inventory

---

## 5. Tech Stack Alignment

| Concern | Tech Choice | Rationale |
|---------|------------|-----------|
| Game Logic | GDScript | Rapid prototyping, Python-like simplicity |
| Performance Modules | C# | Optional für komplexe Systeme oder Performance-Critical Sections |
| Game Engine | Godot 4.5 | 2D-optimized, cross-platform export, integrated physics & tilemaps |
| Assets | GIMP/Krita, Aseprite, TexturePacker | Pixel-art creation & sprite optimization |
| Sound/Music | Audacity, FL Studio, AudioStreamPlayer | In-game playback, looped tracks, dynamic SFX |
| Events | Godot Signals | Loose coupling, modular event-driven architecture |
| Version Control | Git + GitHub | Team collaboration, CI/CD integration |
| CI/CD | GitHub Actions | Automated builds & tests |
| Deployment | Steam / itch.io (PC), future Mobile | Cross-platform delivery with minimal overhead |

---

## 6. Non-Functional Requirements

| Requirement | Architectural Approach |
|-------------|-----------------------|
| Performance | ECS pattern for lightweight update loops, Godot Profiler for optimization |
| Scalability (Gameplay Systems) | Modular Scenes, event-driven decoupling |
| Maintainability | Clear separation of nodes/scenes, modular components, ADRs for design decisions |
| Cross-Platform | Godot export templates, input abstraction via InputMap |
| Replayability | Procedural generation (OpenSimplexNoise), modular enemy & weapon configs |
| Testing | Godot Unit Test Framework, automated simulation of waves, profiling |

---

## 7. Architecture Decision Records (ADRs)

### ADR 001: Event-Driven Communication
**Status:** Accepted  
**Context:** Need for decoupled components for Player, Enemy, Weapons, LevelManager  
**Decision:** Use Godot Signals for event communication  
**Rationale:** Loose coupling, easy addition of new entities, consistent event flow  
**Consequences:** Debugging signal chains is required; ensures modularity

### ADR 002: ECS-ähnliches Pattern
**Status:** Accepted  
**Context:** Complex interactions between multiple entities (enemies, projectiles, buffs)  
**Decision:** Implement ECS-like component system  
**Rationale:** Flexibility in entity behavior, easier balancing and iteration  
**Consequences:** Slight learning curve for new developers

---

## 8. Future Considerations
- Mobile Input Abstraction for touch controls
- Network layer for potential PvP/autobattler modes
- Modular DLC / expansion system (new weapons, enemies)
- Analytics integration for player behavior tracking

---

## 9. Summary
Die Architektur von *Endless Dusk* ist **modular, event-getrieben und ECS-ähnlich**, auf Performance optimiert und auf einfache Erweiterbarkeit ausgelegt.  
Die Verwendung von Godot-Szenen, Signals und komponentenbasierten Patterns erlaubt schnelle Iterationen und klare Trennung von Gameplay, Präsentation und Datenlogik.  


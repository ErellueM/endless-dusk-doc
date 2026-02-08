# Project: Endless Dusk

## Overview
**Endless Dusk** is a 2D Survivor-like game developed in Godot 4.5 for the SWE lecture at DHBW Stuttgart (2025/26). The player controls a character, fights waves of enemies, collects XP gems, levels up, and acquires weapons/upgrades.

**Team:** Bugisoft
- Bayrakal Beric
- Wagner Timo
- Müller Erik
- Stoetter Mika
- Tillmann Felix
- Tarta Maximilian Robin

## Tech Stack
- **Engine:** Godot 4.5 (Forward Plus)
- **Language:** GDScript

## Project Structure
### Root
- `project.godot`: Project settings, input map, autoloads.
- `Global.gd`: Autoload for global state (e.g., selected character).
- `game_manager.gd`: Manages game states (PLAYING, PAUSED, LEVEL_UP, DEAD).

### Main (`res://main/`)
- **Entities** (`main/entities/`):
  - `player.gd`: Handles movement, stats (Might, Area, Speed, etc.), health/regeneration, and leveling logic.
  - `enemy.gd`: Base enemy logic.
- **Systems** (`main/systems/`):
  - `enemy_spawner.gd`: Handles enemy spawning.
  - `wave_handler.gd`: Manages difficulty progression/waves.
  - `inventory.gd`: Manages player weapons (max capacity, add/remove).
- **Weapons** (`main/weapons/`):
  - `weapon.gd`: Base weapon class.
  - `range_weapon.gd`: Logic for ranged attacks.
- **UI** (`main/ui/`):
  - `CharacterSelection`: Menu for choosing characters.
  - `general_menu`: Main menu logic.
  - `ingameUI`: HUD, Pause Menu, Level Up Screen.
- **Global** (`main/global/`):
  - `AudioManager.tscn`: Background music and sound effects manager.

### User Input
Defined in `project.godot`:
- `pause` (Esc): Toggles pause menu.
- `test` (T): Triggers level up for debugging purposes.
- `ui_accept` (Enter/Space): Trigger test attack.
- `ui_up/down/left/right` (Arrow keys/WASD): Movement.

### Key Mechanics & State
### Player Stats
Defined in `player.gd`, editable in Inspector:
- **Survival**: Max Health, Armor, Recovery.
- **Offensive**: Might (Damage %), Area, Cooldown Mult.
- **Utility**: Magnet Range, Growth (XP Mult), Speed.

### Game Loop
Managed by `game_manager.gd`:
1. **PLAYING**: Standard gameplay loop.
2. **PAUSED**: Pauses tree, shows pause menu.
3. **LEVEL_UP**: Pauses tree, shows upgrade selection.
4. **DEAD**: Game over state.

### Leveling System
- XP gems drop from enemies.
- Player collects them (magnet range).
- XP threshold increases by 20% + 10 flat per level.
- Level up triggers `leveled_up` signal for UI handling.

## Current Progress
- **Basic Gameplay**: Movement, Health/Regeneration, Stat system implemented.
- **Systems**: Inventory for weapons, Wave handling foundation, Enemy spawning.
- **UI**: Structure for menus and in-game overlays exists.
- **Audio**: Manager setup (`MusicManager` autoload).

## To-Do / Next Steps (Inferred)
- Expand weapon/item variety.
- Implement specific enemy behaviors and types.
- Refine Level Up selection screen (connect to inventory).
- Map design and environment integration.
- Save/Load system for persistence.

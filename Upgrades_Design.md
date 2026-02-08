# Upgrade System Design – Endless Dusk

## 1. Übersicht
Dieses Dokument definiert das Upgrade-System für *Endless Dusk*. Es basiert auf der bestehenden Architektur (`main/entities/player.gd`, `main/weapons/`) und erweitert diese um skalierbare Progression. 

**Kern-Design-Philosophie:**
*   **Spürbarer Impact:** Jedes Upgrade muss sich sofort mächtig anfühlen.
*   **Synergien:** Waffen und passive Items sollen sich gegenseitig verstärken.
*   **Automatisierung:** Da es ein Auto-Battler ist, ändern Upgrades *wie* gefeuert wird, nicht *ob*.

---

## 2. General Stats (Basiswerte)
Die Stats sind bereits im `player.gd` vorbereitet. Wir definieren hier ihre genaue Funktion und Scaling-Logik.

| Stat Name | Kategorie | Beschreibung | Scaling Typ |
| :--- | :--- | :--- | :--- |
| **Might** | Offensive | Prozentualer Schadensmodifikator. Basis = 1.0 (100%). | Additiv (+10% = 1.1) |
| **Area** | Offensive | Vergrößert Projektile und Explosionsradien. | Additiv |
| **Cooldown** | Offensive | Reduziert die Zeit zwischen Angriffen. (Berechnung: `Base * (1 - CD_Reduc)`) | Multiplikativ (Cap bei -90%) |
| **Speed** | Utility | Bewegungsgeschwindigkeit des Spielers. | Additiv |
| **Duration** | Offensive | Wie lange Projektile/Effekte anhalten (z.B. Pools, Orbits). | Additiv |
| **Amount** | Offensive | Anzahl zusätzlicher Projektile pro Salve. | Flat Integer (+1) |
| **Recovery** | Survival | HP-Regeneration pro Sekunde. | Flat Float |
| **Armor** | Survival | Reduziert erlittenen Schaden (z.B. `Damage - Armor`). | Flat Integer |
| **Magnet** | Utility | Radius zum Einsammeln von XP-Gems. | Additiv |
| **Growth** | Utility | Multiplikator für erhaltene XP. | Additiv |

---

## 3. Player Upgrades (Passive Items)
Passive Items sind dauerhafte Buffs, die einen Slot im Inventar belegen.
*   **Max Slots:** 6 Passive Items (konfigurierbar).
*   **Level-Cap:** Hardsoft-Cap meist bei Level 5.

### Geplante Items
Hier sind Beispiele für Items, die direkt auf die Stats mappen:

1.  **Titan's Plate (Armor)**
    *   Effekt: +1 Armor pro Level.
    *   *Sinn:* Ermöglicht aggressiveres Spielen in Gegnermassen.
2.  **Berserker's Amulet (Might)**
    *   Effekt: +10% Schaden pro Level.
    *   *Sinn:* Essentiell für das Lategame-Scaling.
3.  **Chronos Dial (Cooldown)**
    *   Effekt: -5% Cooldown pro Level.
    *   *Sinn:* Erhöht DPS drastisch für Waffen mit hoher Feuerrate.
4.  **Magnetic Core (Magnet)**
    *   Effekt: +25% Pickup Range pro Level.
    *   *Sinn:* Quality of Life; weniger Bewegung nötig zum Leveln.
5.  **Wind Boots (Speed)**
    *   Effekt: +10% Movement Speed.
    *   *Sinn:* Ausweichen von Boss-Attacken.
6.  **Life Sap (Recovery)**
    *   Effekt: +0.5 HP Regen/sek.
    *   *Sinn:* Sustain ohne Health-Pots.

---

## 4. Waffen Upgrades
Waffen (`main/weapons/`) haben ihre eigene Level-Progression (Level 1-8). Jedes Level verbessert spezifische Attribute der Waffe, nicht den globalen Spieler.

### Upgrade-Logik pro Level
Anstatt nur "mehr Schaden", sollte jedes Level die *Mechanik* verbessern:
*   **Level 2:** +1 Amount (mehr Projektile).
*   **Level 3:** +20% Base Damage.
*   **Level 4:** +0.5s Duration oder Durchschlagskraft (Pierce).
*   **Level 8:** Maximale Stufe -> Bereit für **Special Upgrade**.

### Beispiel: "Arcane Wand" (Range Weapon)
*   **Basis:** Feuert 1 Projektil auf den nächsten Gegner.
*   **Lvl 2:** Feuert 1 zusätzliches Projektil (+1 Amount).
*   **Lvl 3:** -10% Cooldown.
*   **Lvl 4:** +10 Base Damage.
*   **Lvl 5:** Projektile durchdringen 1 Gegner (+1 Pierce).
*   **Lvl 6:** +1 Amount.
*   **Lvl 7:** +20% Base Damage.
*   **Lvl 8:** Kritischer Treffer-Chance hinzugefügt.

---

## 5. Special Upgrades (Evolutions & Synergies)
Das "Special Upgrade" ist der Höhepunkt des Builds. Es verwandelt eine Waffe in ihre ultimative Form.

### Voraussetzung für Special Upgrade
1.  Die Waffe muss **Level 8** (Max) sein.
2.  Der Spieler muss ein **spezifisches Passiv-Item** besitzen (egal welches Level).
3.  Der Spieler muss eine **Schatzkiste** öffnen (Drop von Boss/Elite Gegner).

### Geplante Evolutionen
*   **Hellfire Gatling**
    *   *Basis:* Arcane Wand + Chronos Dial (Cooldown).
    *   *Effekt:* Keine Verzögerung mehr. Ein konstanter Strahl aus Projektilen.
*   **Invincible Aura**
    *   *Basis:* Garlic Field (AoE) + Life Sap (Recovery).
    *   *Effekt:* Der Schadensbereich entzieht Gegnern Leben und heilt den Spieler (Lifesteal).
*   **Thunder Storm**
    *   *Basis:* Lightning Ring + Titan's Plate.
    *   *Effekt:* Blitze schlagen permanent zufällig ein und betäuben Gegner kurzzeitig.

---

## 6. Technische Umsetzung (Godot/Architecture)
Damit dies in die bestehende Architektur passt, nutzen wir `Resource`-Dateien anstatt Hardcoding.

### Datenstruktur
1.  **UpgradeData (Resource):**
    *   `id`: string (z.B. "upgrade_might")
    *   `icon`: Texture2D
    *   `levels`: Array[Dictionary]
        *   Jeder Eintrag definiert, was passiert: `{"stat": "might", "value": 0.1}`.

2.  **WeaponData (Resource) extends UpgradeData:**
    *   Erweitert das Basis-Upgrade um Waffenspezifika.
    *   `scene_path`: Pfad zur Waffenszene (für den Spawner).
    *   `evolution_requirements`: Referenz auf das benötigte Passive Item.

### Integration in den Game Loop
*   **LevelUp Manager:**
    *   Lädt beim Start alle verfügbaren `UpgradeResources`.
    *   Beim `LEVEL_UP`-Signal: Zieht 3-4 zufällige Optionen aus dem Pool.
    *   Filtert Optionen:
        *   Ist das Item schon Max Level? -> Nicht anzeigen.
        *   Besitzt der Spieler es noch nicht und Slots sind voll? -> Nicht anzeigen.
*   **Anwendung:**
    *   Wird ein **Passives Item** gewählt -> Rufe `player.apply_stat_upgrade(stat_name, value)` auf.
    *   Wird eine **Waffe** gewählt -> Rufe `inventory.upgrade_weapon(weapon_id)` auf.

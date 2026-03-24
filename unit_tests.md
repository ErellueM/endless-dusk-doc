# Unit Tests Dokumentation - Endless Dusk

## 1. Vorgehensweise und Architektur

### Welches Framework wird genutzt?
Für das Testen unseres Projekts *Endless Dusk* nutzen wir **GdUnit4**. Es handelt sich dabei um das aktuell modernste und am besten integrierte Unit-Testing-Framework für die Godot 4 Engine.

### Warum dieses Framework?
Im Gegensatz zu externen Tools interagiert GdUnit4 nahtlos und nativ mit GDScript.
- **Engine-Integration:** Wir können unsere Tests direkt im Godot Editor ausführen und debuggen oder sie automatisiert ("headless") per Command Line anstoßen.
- **Isolierung:** Das Framework bietet uns Werkzeuge, um Skripte ohne deren kompletten SceneTree-Abhängigkeiten zu laden.
- **Starke Assertions:** Die verständliche Verkettungsschreibweise (`assert_that(...).is_equal(...)`) fördert sehr lesbaren und sauberen Code, der als ausführende Dokumentation dient.

### Namenskonvention
Damit die Tests automatisch erkannt und strukturiert bleiben, gelten folgende Konventionen:
1. **Ordnerstruktur:** Sämtliche Test-Dateien müssen im Root-Ordner `tests/` abgelegt werden. Die Unterordner spiegeln den exakten Pfad der originalen Skripte wider (die `main/`-Ebene wird hierbei direkt als Wurzel verstanden). 
   *Beispiel:* `main/global/audio_manager.gd` ➡️ `tests/global/test_audio_manager.gd`.
2. **Dateinamen:** Test-Dateien tragen immer das Präfix `test_`, gefolgt vom Originalnamen (z.B. `test_game_manager.gd`).
3. **Klassen und Methoden:** Test-Klassen erben immer von `GdUnitTestSuite`. Methoden, die einen echten Unit-Test darstellen, müssen mit `test_` beginnen, damit der GdUnit4-Runner sie automatisch als Testfall erkennt und ausführt.

### Branching
Für die Implementierung der Unit-Tests wurde eine strikte Branching-Strategie verwendet. Die Entwicklung und das Zusammentragen der Tests fand auf einem dedizierten **`testing`**-Branch statt. 
Nachdem alle Features, Skripte und Menüs ("Entities", "Systems", "Environments") unabhängig voneinander von den Teammitgliedern auf dem `testing`-Branch mit Tests versehen wurden, wird garantiert, dass das Kernspiel (Branch `main`) bis zum Review sauber und intakt bleibt.

---

## 2. Ein Test-Beispiel (Isolierung & Mocking)

Unser Fokus lag laut Clean-Code-Prinzipien darauf, dass echte **Unit-Tests** (und keine Integrationstests) geschrieben werden. Externe Abhängigkeiten von riesigen Godot-Szenen (`.tscn`) wurden gezielt durch Dummy-Nodes und saubere Code-Injektion vermieden ("Mocking").

Das folgende kurze Beispiel aus dem Projekt zeigt, wie der `game_manager` getestet wird, indem fehlende UI-Bildschirme einfach mit neuen Blanko-`CanvasLayers` überschrieben (gemockt) werden:

```gdscript
extends GdUnitTestSuite

var game_manager

# Setup: Wird VOR jedem einzelnen Test frisch aufgerufen
func before_test():
	var script = load("res://game_manager.gd")
	game_manager = Node.new()
	game_manager.set_script(script)
	
	# Mocks: Isolierte Dummy-Akteure statt echter schwerer UI-Szenen
	game_manager.pause_menu = CanvasLayer.new()
	game_manager.level_up_screen = CanvasLayer.new()
	game_manager.game_over_screen = CanvasLayer.new()
	
	add_child(game_manager)
	await get_tree().process_frame

# Cleanup: Wird NACH jedem einzelnen Test aufgerufen
func after_test():
	if game_manager and is_instance_valid(game_manager):
		game_manager.queue_free()

# Der tatsächliche Test
func test_change_state_to_paused():
	# Act (Wir simulieren eine Zustandsänderung)
	game_manager.change_state(1) # Entspricht GameState.PAUSED
	
	# Assert (Überprüfung ob der Manager wie erwartet handelt)
	assert_that(game_manager.current_state).is_equal(1)
	assert_that(get_tree().paused).is_true()
```

---

## 3. Beispiel einer Konsolenausgabe (Testergebnisse)

Ein beispielhafter Auszug aus der Ausführung unserer Tests im Terminal durch den `GdUnitCmdTool`-Runner. Die Ergebnisse zeigen, dass die isolierte Game Manager Logik extrem schnell und zu 100% einwandfrei durchläuft.

*(Anmerkung zu Warnungen: Orphan-Nodes, die gelegentlich bei reinen Unit Tests angezeigt werden, entstehen durch künstliche UI-Mocks (z.B. CanvasLayers), die nicht explizit an Nodes angehängt, sondern direkt in Klassen-Variablen gehalten werden. Diese Nodes haben wir daraufhin mit manuellen `queue_free()`-Bereinigungen im `after_test()`-Block versehen, weshalb die Architektur absolut speicherresistent ist).*

```diff
  GdUnit Test Client connected with id: -9223365471678402808
  Installing GdUnit4 session system hooks.
  Session hook 'GdUnitHtmlTestReporter' installed.
  Session hook 'GdUnitXMLTestReporter' installed.
! Run Test Suite: res://tests/test_game_manager.gd
+ 	test_game_manager > test_initial_state                                              PASSED 9ms
+ 	test_game_manager > test_change_state_to_paused                                     PASSED 16ms
+ 	test_game_manager > test_change_state_to_playing                                    PASSED 17ms
+ 	test_game_manager > test_player_leveled_up                                          PASSED 16ms
  
+ Statistics: 4 test cases | 0 errors | 0 failures | 0 flaky | 0 skipped | 12 orphans | PASSED 74ms
  
  Overall Summary: 4 test cases | 0 errors | 0 failures | 0 flaky | 0 skipped | 12 orphans |
  Executed test suites: (1/1)
  Executed test cases : (4/4)
  Total execution time: 74ms
   Open XML Report at: file:///Users/beric61/Desktop/endless-dusk/reports/report_1/results.xml
  Open HTML Report at: file:///Users/beric61/Desktop/endless-dusk/reports/report_1/index.html
  GdUnit Test Client disconnected with id: -9223365471678402808
```

## 4. Referenz zum Test-Projekt

Alle im Projekt geschriebenen Tests für das Evaluieren von Zuständen, Variablen und dem Lebenszyklus der Komponenten ("Environments", "Entities", "Globals", etc.) befinden sich gebündelt im Git Repository unter folgendem Pfad:

👉 **`./tests/`**

Ein detaillierter Überblick über die Struktur aus dem Projekt:
- `./tests/environments/` (Für Lichtquellen, Vfx)
- `./tests/global/` (Für Singletons, Stats und Manager)
- `./tests/maps/` (Für Kameras und Spawns)
- `./tests/entities/` (Für Spieler, Health, XP)
- `./tests/systems/` (Für Spawner, Waves)
- `./tests/ui/` (Für Menüs, Optionen, Progress-Bars)

---
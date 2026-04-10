# GDScript-Linting (Lokal & CI)

Dieser Leitfaden beschreibt die Einrichtung einer automatisierten Code-Prüfung (Linting) für unser Godot-Projekt "Endless Dusk". Ziel ist es, durchgehend sauberen Code nach dem offiziellen GDScript-Styleguide zu gewährleisten, ohne den Entwicklungsprozess durch zu strenge Regeln zu blockieren.

## 1. Lokale Einrichtung (Entwicklung)

Bevor der Code in die Cloud geht, wird das Toolkit lokal installiert.

### Installation des Toolkits
Das Tooling basiert auf Python. Zur Installation wird das Terminal genutzt:
```bash
pip install gdtoolkit
```

### Konfiguration
Wir nutzen eine `pyproject.toml` im Hauptverzeichnis des Projekts. Diese Datei sorgt dafür, dass bestimmte "Pingeligkeits-Fehler" (wie die genaue Reihenfolge von Variablen und Signalen) ignoriert werden.

### Integration in VS Code
1.  **Erweiterung:** Suche im VS Code Marketplace nach **"GDScript Toolkit"** und installiere diese.
2.  **Nutzen:** Fehler werden direkt im Editor markiert.
3.  **Manueller Check:** Das gesamte Projekt kann jederzeit manuell geprüft werden:
```bash
find . -type d \( -path "./addons" -o -path "./tests" \) -prune -o -name "*.gd" -print | xargs gdlint
```

---

## 2. Einrichtung der CI-Pipeline (GitHub Actions)

Die Continuous Integration (CI) stellt sicher, dass wir bei jedem Push einen Bericht über die Code-Qualität erhalten.

### Verzeichnisstruktur
Der Workflow muss exakt an diesem Ort liegen:
`.github/workflows/gdscript-lint.yml`

### Der "Safe-Mode"
In unserer CI ist der Linter so eingestellt, dass er den Build **nicht abbricht** (`|| true`). Das bedeutet: Die Action wird grün, aber du kannst im Log sehen, welche Dateien noch "schmutzig" sind. Dies verhindert, dass kleine Formatierungsfehler wichtige Merges blockieren.

---

## 3. Fehlerbehebung: Was tun bei Fehlern?

Wenn `gdlint` Fehler anzeigt, gibt es zwei Wege diese zu lösen:

### A. Automatische Formatierung mit `gdformat`
Für Massenfehler wie falsche Einrückungen oder Leerzeichen:
```bash
gdformat .
```
*Dies passt alle `.gd`-Dateien automatisch an den Styleguide an.*

### B. Manuelle Korrekturen & Klasseneinhaltung
Der Linter bevorzugt eine feste Struktur. Sollten Fehler bezüglich der `class-definitions-order` auftauchen, hilft oft folgende Reihenfolge innerhalb der Datei:
1. `extends` / `class_name`
2. `signals`
3. `enums` / `constants`
4. `export var` / `var`
5. `@onready var`
6. `functions` (z.B. `_ready`, `_process`)

---

## Anhang: Projekt-Dateien

Hier sind die aktuellen Konfigurationen, die im Projekt-Root liegen müssen:
### 📁 [.github/workflows](https://github.com/ErellueM/endless-dusk/tree/main/.github/workflows)
### 📄 [gdscript-lint.yml](https://github.com/ErellueM/endless-dusk/blob/main/.github/workflows/gdscript-lint.yml)
### 📄 [pyproject.toml](https://github.com/ErellueM/endless-dusk/blob/main/.github/workflows/pyproject.toml)
```yaml
name: GDScript Linting (gdlint)

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.x"

      - name: Install gdtoolkit
        run: pip install gdtoolkit

      - name: Run gdlint
        # Wir nutzen "|| true", damit der Workflow informativ bleibt, aber nicht blockiert.
        run: |
          find . -type d \( -path "./addons" -o -path "./tests" \) -prune -o -name "*.gd" -print | xargs gdlint || true
```

### 📄 `pyproject.toml`
```toml
[tool.gdlint]
max-line-length = 200
class-definitions-order = false
unused-argument = false
no-elif-return = false
no-else-return = false
duplicated-load = false
```

---

*Dieser Prozess sorgt dafür, dass sich Code-Reviews auf die Logik statt auf die Formatierung konzentrieren können.*

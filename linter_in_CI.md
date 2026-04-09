Hier ist das aktualisierte Markdown-Dokument. Ich habe einen neuen Abschnitt zur Fehlerbehebung mit `gdformat` hinzugefügt, damit jedes Teammitglied weiß, wie man die "Massen-Fehler" schnell und effizient behebt.

---

# GDScript-Linting (Lokal & CI)

Dieser Leitfaden beschreibt die Einrichtung einer automatisierten Code-Prüfung (Linting) für unser Godot-Projekt "Endless Dusk".
Ziel ist es, durchgehend sauberen Code nach dem offiziellen GDScript-Styleguide zu gewährleisten.

## 1. Lokale Einrichtung (Entwicklung)

Bevor der Code in die Cloud geht, wird der Linter lokal installiert, um Fehler bereits während des Schreibens zu erkennen.

### Installation des Toolkits
Das Tooling basiert auf Python. Zur Installation wird das Terminal (z. B. in VS Code) genutzt:
```bash
pip install gdtoolkit
```

### Integration in VS Code
1.  **Erweiterung:** Suche im VS Code Marketplace nach **"GDScript Toolkit"** und installiere diese.
2.  **Nutzen:** Fehler wie ungenutzte Variablen oder falsche Einrückungen werden nun direkt im Editor durch Wellenlinien markiert.
3.  **Manueller Check:** Das gesamte Projekt kann jederzeit manuell im Terminal geprüft werden:
    ```bash
    gdlint .
    ```

---

## 2. Einrichtung der CI-Pipeline (GitHub Actions)

Die Continuous Integration (CI) stellt sicher, dass kein fehlerhafter Code in den Hauptzweig gelangt.

### Verzeichnisstruktur
Der Workflow muss exakt an diesem Ort im Projekt-Root liegen:
```text
[Projekt-Ordner]/
└── .github/
    └── workflows/
        └── gdscript-lint.yml
```

### Konfiguration des Workflows
Die Datei `gdscript-lint.yml` definiert die Regeln für GitHub. Sie bewirkt, dass bei jedem **Push** oder **Pull Request** auf den `main`-Branch ein virtueller Server gestartet wird, der den Code prüft. Schlägt der Linter fehl, wird der gesamte Prozess als **"failed"** markiert.

---

## 3. Der Prozess-Ablauf (Workflow)

| Phase | Aktion | Ergebnis |
| :--- | :--- | :--- |
| **1. Entwicklung** | Code schreiben in VS Code. | Die Extension zeigt lokale Warnungen sofort an. |
| **2. Vorprüfung** | Optionaler Check via Terminal. | `gdlint .` zeigt potenzielle Probleme vor dem Push. |
| **3. Push/PR** | Code zu GitHub hochladen. | Der GitHub-Workflow startet automatisch im Hintergrund. |
| **4. Validierung** | Blick in den **Actions**-Tab auf GitHub. | **Grüner Haken:** Alles okay. **Rotes X:** Korrektur nötig. |

---

## 4. Fehlerbehebung: Was tun bei "Failure"?

Wenn der Linter fehlschlägt (z. B. "2587 problems found"), müssen diese korrigiert werden, bevor ein Merge erlaubt ist.

### Automatische Formatierung mit `gdformat`
Anstatt hunderte Formatierungsfehler (Leerzeichen, Einrückungen) manuell zu fixen, kann das Toolkit den Code automatisch anpassen:

1.  **Befehl im Terminal ausführen:**
    ```bash
    gdformat .
    ```
    *Dies formatiert alle `.gd`-Dateien im aktuellen Ordner nach dem offiziellen Styleguide.*
2.  **Änderungen prüfen:** Kontrolliere in VS Code die geänderten Dateien.
3.  **Neu committen & pushen:**
    ```bash
    git add .
    git commit -m "style: fix linting issues with gdformat"
    git push
    ```

### Manuelle Korrekturen
Logische Fehler (z. B. `unused-variable`) kann `gdformat` nicht lösen. Diese müssen manuell im Code gelöscht oder korrigiert werden, bis `gdlint .` keine Fehler mehr ausgibt.

---

## 5. Best Practices für Teams

* **Zentralisierung:** Die Datei im Ordner `.github/workflows/` muss auf den `main`-Branch gepusht werden, damit sie für alle Teammitglieder aktiv wird.
* **Merge-Blockade:** In den GitHub-Repository-Einstellungen sollte festgelegt werden, dass ein Merge nur möglich ist, wenn der `gdlint`-Check "grün" ist.
* **Ordner ignorieren:** Sollten Drittanbieter-Addons zu viele Fehler verursachen, kann der Workflow so angepasst werden, dass nur der eigene `scripts/`-Ordner geprüft wird (`gdlint scripts/`).

---

Dieser Prozess sorgt dafür, dass sich Code-Reviews auf die Logik statt auf die Formatierung konzentrieren können.

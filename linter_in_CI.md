# GDScript-Linting (Lokal & CI)

Dieser Leitfaden beschreibt die Einrichtung einer automatisierten Code-Prüfung (Linting) für  unser Godot-Projekt. 
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
Die Datei `gdscript-lint.yml` definiert die Regeln für GitHub. Sie bewirkt, dass bei jedem **Push** oder **Pull Request** auf den `main`-Branch ein virtueller Server gestartet wird, der den Code prüft. Schlägt der Linter fehl, wird der gesamte Prozess als "failed" markiert.

---

## 3. Der Prozess-Ablauf (Workflow)

Der Arbeitsfluss gliedert sich in folgende Phasen:

| Phase | Aktion | Ergebnis |
| :--- | :--- | :--- |
| **1. Entwicklung** | Code schreiben in VS Code. | Die Extension zeigt lokale Warnungen sofort an. |
| **2. Commit** | `git add` und `git commit`. | Der Code wird lokal für den Upload vorbereitet. |
| **3. Push/PR** | Code zu GitHub hochladen. | Der GitHub-Workflow startet automatisch im Hintergrund. |
| **4. Validierung** | Blick in den **Actions**-Tab auf GitHub. | **Grüner Haken:** Code ist sauber. **Rotes X:** Korrekturbedarf. |

---

## 4. Best Practices für Teams

* **Zentralisierung:** Die Datei im Ordner `.github/workflows/` muss auf den `main`-Branch gepusht werden, damit sie für alle Teammitglieder und alle Pull Requests aktiv wird.
* **Merge-Blockade:** Es wird empfohlen, in den GitHub-Repository-Einstellungen ("Branch Protection Rules") festzulegen, dass ein Merge nur möglich ist, wenn der `gdlint`-Check erfolgreich war.
* **Fehlerbehebung:** Falls der CI-Linter einen Fehler meldet, kann die genaue Fehlermeldung und Zeilennummer direkt in der GitHub-Oberfläche unter dem Reiter "Actions" oder innerhalb des Pull Requests eingesehen werden.

---

Dieser Prozess sorgt dafür, dass sich Code-Reviews auf die Logik statt auf die Formatierung konzentrieren können.

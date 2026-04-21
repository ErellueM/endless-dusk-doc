
# Retrospective: Endless Dusk


* **Gruppenmitglieder:**
| Vorname, Name | GitHub-Nutzername |
| :--- | :--- |
| Beric Bayrakal | Beric-61 |
| Timo Wagner | timopromotive |
| Erik Müller | ErellueM |
| Mika Stoetter | Mika1011 |
| Felix Tillmann | Sh4d0wnight |
| Maximilian Robin Tarta | maxitaxi27 |

* **Betrachteter Zeitraum:** Projekt-Gesamtzeitraum (September 2025 – April 2026)

---

## 2. Was gut gelaufen ist (What went well)
* **Methodische Trennung von Projektbereichen:** 
Die frühzeitige Entscheidung, Code und Dokumentation in zwei separaten Repositories zu führen, hat die Arbeitsabläufe erheblich strukturiert. Dies ermöglichte eine klare Versionierung der Abgaben (z. B. Product Vision, TechStack) unabhängig vom Entwicklungsstand des Spiels.
* **Effektive Nutzung von Kanban zur Parallelisierung:** Durch die konsequente Aufgabenverteilung via Cryptpad konnten verschiedene Fachbereiche simultan arbeiten. Während ein Teil des Teams die Spielmechaniken vertiefte, konnten andere Mitglieder parallel das Test-Framework GdUnit4 integrieren und die UI-Systeme ausbauen.
* **Iterative Qualitätssteigerung durch Testing:** Die Einführung automatisierter Unit-Tests im März 2026 markierte einen Wendepunkt in der Stabilität. Die Zusammenarbeit bei der Erstellung von Tests für Entitäten, UI und Kernsysteme hat dazu beigetragen, die Fehlerquote in der finalen Phase zu senken.
* **Kommunikationsfluss:** Die Kombination aus direkten Absprachen im Präsenzkurs und einer schnellen Abstimmung via WhatsApp ermöglichte es, kurzfristige Hürden bei Pull Requests, der klaren Aufgabenaufteilung oder welche zu implementierenden Funktionalitäten Priorität haben zeitnah zu überwinden.

---

## 3. Was verbessert werden kann (What did not go well)
* **Timing der Infrastruktur-Implementierung:**
    * **Symptom:** In der Endphase kam es zu vermehrtem Zeitaufwand durch Korrekturen an der Linter-Pipeline und den CI-Workflows.
    * **Ursache:** Die Priorisierung lag zu Beginn stark auf der funktionalen Entwicklung, wodurch die Automatisierungstools (Linting/CI) erst spät in den Workflow integriert wurden.
    * **Reflektion:** Eine frühere Etablierung dieser Standards hätte den Integrationsprozess im April deutlich geglättet.
* **Komplexität bei der Code-Integration:**
    * **Symptom:** Beim Zusammenführen langlebiger Feature-Branches traten vermehrt Merge-Konflikte auf, die nachträgliche Korrekturen erforderten.
    * **Ursache:** Der Austausch zwischen den Zweigen fand teilweise in zu großen Zeitabständen statt, was die Abweichungen zwischen den Code-Ständen vergrößerte.
    * **Reflektion:** Häufigere Integrationen („Continuous Integration“) hätten die Komplexität der einzelnen Merges reduziert.
* **Verteilung des Domänenwissens in der Kern-Architektur:**
    * **Symptom:** Bestimmte zentrale Logik-Bausteine (wie das Waffen- und Upgradesystem) wurden schwerpunktmäßig von einzelnen Teammitgliedern entwickelt.
    * **Ursache:** Durch die Spezialisierung im Kanban-Board konzentrierte sich das Detailwissen über die Kern-Architektur auf wenige Köpfe, was den Review-Prozess für den Rest des Teams erschwerte.
    * **Reflektion:** Ein gezielterer Wissensaustausch über die zentralen Systeme hätte die kollektive Sicherheit im Umgang mit der Codebase gestärkt.

---

## 4. Maßnahmen zur Verbesserung (Actionable Measures)

| Maßnahme | Detaillierte Beschreibung & Umsetzung | Erfolgskriterium (Metrik) | Verantwortlicher | Zieltermin |
| :--- | :--- | :--- | :--- | :--- |
| **Frühzeitige Setup-Standardisierung** | Vollständige Konfiguration von Lintern (GDLint, GDFormat) und CI-Pipelines (GitHub Actions) innerhalb der ersten Projektwoche. Erst nach Validierung der Infrastruktur beginnt die Feature-Entwicklung. | Automatisierte Pipeline-Checks verhindern das Mergen von unformatiertem oder fehlerhaftem Code von Beginn an. | Maximilian (`maxitaxi27`) | Nächster Projektauftakt |
| **Optimierung der Integrationszyklen** | Einführung einer "Short-lived Branch"-Regel: Entwicklungszweige dürfen maximal 3 Tage bestehen. Ein täglicher Rebase des Arbeitszweigs auf den Hauptzweig (`main`) wird zur Pflicht. | Wegfall von komplexen Merge-Konflikten; keine "Fix errors after merging"-Einträge in der Historie. | Erik (`ErellueM`) | Ab sofort |
| **Wissens-Sharing & Architekturschutz** | Architektonisch kritische Komponenten (z. B. Kern-Logik, Waffensystem) werden verpflichtend im Pair Programming entwickelt oder durch ein detailliertes Walkthrough-Review für das Team dokumentiert. | Erhöhung des „Bus-Faktors“: Mindestens zwei Teammitglieder können jedes Kernmodul unabhängig voneinander warten. | Timo (`timopromotive`) | Nächste Iteration |
| **Test-Mandat für Logik-Features** | Erweiterung der "Definition of Done": Jedes neue funktionale Feature muss durch eine GdUnit4-Test-Suite abgesichert sein, bevor der entsprechende Pull Request akzeptiert wird. | Stetig steigende Testabdeckung und Reduktion von Regressionen bei der Integration neuer Spielmechaniken. | Beric (`Beric-61`) | Ab sofort |
| **Strukturierte Dokumentationspflege** | Proaktive Aktualisierung der Architektur- und Anforderungsdokumente bei jeder größeren Code-Änderung, anstatt einer gesammelten Aktualisierung am Ende der Iteration. | Die Dokumentation spiegelt zu jedem Zeitpunkt den aktuellen Stand der Implementierung wider (kein "Dokumentations-Lag"). | Mika (`Mika1011`) | Nächste Iteration |
---

## 5. Bezug zur Projektarbeit (Evidence)

Die in dieser Retrospektive getroffenen Feststellungen und die daraus abgeleiteten Maßnahmen stützen sich auf konkrete Artefakte und Daten aus der gesamten Projektlaufzeit:

* **Entwicklungsdynamik und CI-Infrastruktur:**
    Die Repository-Historie belegt objektiv, dass technische Hürden in der automatisierten Code-Analyse erst in der finalen Phase des Projekts adressiert wurden. Eine massive Häufung von Korrekturmaßnahmen in der Zeit zwischen dem 10. und 14. April 2026 (belegt durch Commit-Nachrichten wie *„Fix ruleset Linter“*, *„Attempt to fix linter pipeline action“* oder *„Update yml“*) zeigt, dass die Infrastruktur nicht von Beginn an reibungslos funktionierte. Diese späten Anpassungen unterbrachen den Feature-Flow, was die Notwendigkeit eines „Infrastruktur-First“-Ansatzes für künftige Iterationen unterstreicht.

* **Synchronisation zwischen Planung (Kanban) und Implementierung:**
    Das genutzte Board diente während des gesamten Projekts als „Single Source of Truth“ für die Aufgabenverteilung. Der Abgleich zwischen den dortigen Zuweisungen und den tatsächlich umgesetzten Beiträgen zeigt eine hohe Übereinstimmung in der zeitlichen Abfolge. Während die Parallelisierung bei Benutzeroberflächen und visuellen Elementen (insbesondere im Oktober und November 2025) exzellent funktionierte, lässt sich an der Dichte der technischen Beiträge zur „Core Engine“ ablesen, dass die Kern-Logik oft in sehr dichten, aufeinanderfolgenden Schritten entwickelt wurde. Dies stützt die Beobachtung, dass das Detailwissen über diese zentralen Systeme auf eine geringe Anzahl an Verantwortlichen konzentriert blieb (Bus-Faktor).

* **Etablierung von Qualitätsstandards durch Testing:**
    Der Schwenk von einer rein funktionsgetriebenen Entwicklung hin zu einer qualitätsgesicherten Arbeitsweise ist durch den massiven Anstieg von Test-Suiten ab März 2026 klar nachvollziehbar. Die Integration des **GdUnit4-Frameworks** ist direkt im Repository durch die neu geschaffenen Test-Suiten für Waffen- und Upgradesysteme nachweisbar. Strukturierte Einträge wie *„Add unit tests draft“* dokumentieren den erfolgreichen Übergang zu einer testgetriebenen Entwicklung und die Umsetzung der ursprünglich im Kickoff-Dokument definierten Qualitätsziele.

* **Strukturelle Trennung der Arbeitsbereiche:**
    Die methodische Entscheidung, die konzeptionelle Planung und die technische Umsetzung in zwei separaten Repositories zu führen, spiegelt sich in der sauberen Struktur der Arbeitsbereiche wider. Die Dokumentationshistorie zeigt eine kontinuierliche Fortführung von der ersten Product Vision bis hin zur finalen Architekturübersicht, während der technische Bereich fast ausschließlich auf die Evolution des Codes fokussiert blieb. Diese Trennung verhinderte Informationsverluste und ermöglichte eine klare Referenzierung von Anforderungen (z. B. Software-Architektur oder Personas) während der gesamten Laufzeit.

* **Integrationsverhalten und Kommunikation:**
    Regelmäßige Einträge über Fehlerbehebungen unmittelbar nach dem Zusammenführen verschiedener Entwicklungszweige (z. B. Einträge wie *„Fix errors after merging“*) dienen als Beleg für die Herausforderungen bei der Code-Integration. Gleichzeitig belegt die zeitnahe Zusammenführung komplexer Features im Oktober (wie die Charakterauswahl und Gegner-Logik) die hohe Effektivität der hybriden Kommunikation (WhatsApp für schnelle Abstimmung, Präsenztermine für Architekturfragen). Die Protokolle der Pull-Request-Reviews zeigen zudem, dass die Code-Qualität durch gegenseitiges Feedback stabil gehalten wurde.
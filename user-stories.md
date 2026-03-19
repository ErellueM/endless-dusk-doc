# User Stories – Endless Dusk

## Definition of Ready (DoR)

Eine User Story gilt in diesem Projekt als „Ready“, wenn folgende Kriterien erfüllt sind:

### Inhaltliche Klarheit
- Der Nutzen für den Spieler ist klar beschrieben
- Die Funktion passt zum Core-Gameplay

### Anforderungen & Verständnis
- Akzeptanzkriterien sind vollständig und testbar formuliert
- Offene fachliche Fragen wurden geklärt
- Abhängigkeiten zu anderen Features sind identifiziert

### Umsetzungsvorbereitung
- Die Story ist klein genug für einen Sprint
- Story Points wurden vom Team geschätzt
- Technische Umsetzung ist grundsätzlich verstanden

### Qualität & Testing
- Eine Definition of Done ist vorhanden
- Testbarkeit ist gegeben

### Projektspezifisch
- Auswirkungen auf Performance (z. B. viele Gegner) sind berücksichtigt
- UI/UX passt zum bestehenden Spielstil
- Keine Widersprüche zu bestehenden Spielmechaniken

---

## Persona 1: Markus B. – Der „Zwischendurch“-Spieler

### Story 1: Schneller Run-Start
**Als** Zwischendurch-Spieler  
**möchte ich**, dass ich aus dem Hauptmenü sofort einen Run starten kann  
**sodass** ich ohne Wartezeit direkt ins Gameplay komme.

**Akzeptanzkriterien:**
- Zeit vom Klick auf „Start“ bis zur Spielfigur-Steuerung ≤ 3 Sekunden  
- Kein erzwungenes Intro oder Cutscene vor dem ersten Run  
- Ladezeit wird visuell angezeigt (z. B. Ladeindikator)

**Definition of Done:**
- Ladezeitmessung auf Zielhardware dokumentiert  
- QA bestätigt reproduzierbare ≤ 3 Sekunden  
- Kein Blocker zwischen Menü und Gameplay  

**Aufwand:** 5 Story Points

---

### Story 2: Plattformunabhängige UI
**Als** Zwischendurch-Spieler  
**möchte ich**, dass die UI auf verschiedenen Bildschirmgrößen gut funktioniert  
**sodass** ich das Spiel problemlos auf meinem PC spielen kann.

**Akzeptanzkriterien:**
- UI skaliert korrekt für verschiedene Auflösungen (z. B. Full HD, WQHD)  
- Alle UI-Elemente sind sichtbar und nicht abgeschnitten  
- Bedienung vollständig mit Maus und Tastatur möglich  

**Definition of Done:**
- QA testet mindestens 2 Auflösungen  
- Keine überlappenden oder fehlenden UI-Elemente  
- Alle Funktionen erreichbar  

**Aufwand:** 5 Story Points

---

### Story 3: Automatische Angriffe
**Als** Zwischendurch-Spieler  
**möchte ich**, dass mein Charakter automatisch angreift  
**sodass** ich mich nur auf Bewegung konzentrieren kann.

**Akzeptanzkriterien:**
- Angriffe erfolgen automatisch in festen Intervallen  
- Spieler muss keine Angriffstaste drücken  
- Angriffe treffen automatisch Gegner  

**Definition of Done:**
- QA bestätigt, dass keine manuelle Eingabe nötig ist  
- Angriffssystem funktioniert stabil über längere Runs  

**Aufwand:** 3 Story Points

---

### Story 4: Pause & Fortsetzen
**Als** Zwischendurch-Spieler  
**möchte ich**, das Spiel pausieren und fortsetzen können  
**sodass** ich meine Session jederzeit unterbrechen kann.

**Akzeptanzkriterien:**
- Pause stoppt das komplette Spielgeschehen  
- Fortsetzen setzt exakt an derselben Stelle fort  
- Pause-Menü zeigt aktuelle Run-Infos  

**Definition of Done:**
- QA testet mehrfaches Pausieren und Fortsetzen  
- Keine Zustandsverluste im Spiel  

**Aufwand:** 3 Story Points

---

## Persona 2: Lena K. – Die Roguelite-Strategin

### Story 5: Synergien beim Level-Up
**Als** Roguelite-Strategin  
**möchte ich**, Synergien direkt beim Level-Up sehen  
**sodass** ich bessere strategische Entscheidungen treffen kann.

**Akzeptanzkriterien:**
- Jede Auswahl zeigt Effekt und mögliche Synergien  
- Beschreibung max. 2–3 Zeilen  
- Synergien visuell hervorgehoben  

**Definition of Done:**
- QA prüft alle Synergien  
- Texte sind verständlich und korrekt  

**Aufwand:** 5 Story Points

---

### Story 6: Unterschiedliche Start-Charaktere
**Als** Roguelite-Strategin  
**möchte ich**, verschiedene Charaktere wählen  
**sodass** jeder Run neue Strategien ermöglicht.

**Akzeptanzkriterien:**
- Mindestens 3 Charaktere verfügbar  
- Jeder Charakter hat:
  - eigene Startwaffe  
  - eigenen Bonus  

**Definition of Done:**
- QA testet alle Charaktere  
- Unterschiede sind im Gameplay spürbar  

**Aufwand:** 8 Story Points

---

### Story 7: Run-Zusammenfassung
**Als** Roguelite-Strategin  
**möchte ich**, nach einem Run sehen, welche Builds ich genutzt habe  
**sodass** ich meine Entscheidungen reflektieren kann.

**Akzeptanzkriterien:**
- Anzeige nach Run-Ende mit:
  - genutzten Waffen  
  - Items  
  - Level  
  - Run-Dauer  
- Anzeige erscheint automatisch nach dem Run  

**Definition of Done:**
- QA prüft korrekte Anzeige nach mehreren Runs  
- Daten sind vollständig und korrekt  

**Aufwand:** 3 Story Points

---

### Story 8: Meta-Progression
**Als** Roguelite-Strategin  
**möchte ich**, permanente Upgrades freischalten  
**sodass** ich langfristig stärker werde.

**Akzeptanzkriterien:**
- Spieler erhält Währung nach Run  
- Upgrade-System im Menü verfügbar  
- Upgrades wirken sich auf zukünftige Runs aus  

**Definition of Done:**
- QA testet mehrere Runs mit Upgrades  
- Boni werden korrekt angewendet  

**Aufwand:** 8 Story Points

---

### Story 9: Einfluss auf Zufall (RNG)
**Als** Roguelite-Strategin  
**möchte ich**, meine Upgrade-Auswahl beeinflussen können  
**sodass** ich gezielter Builds erstellen kann.

**Akzeptanzkriterien:**
- Re-Roll Funktion vorhanden  
- Mindestens 3 Auswahloptionen pro Level-Up  
- Re-Rolls sind limitiert  

**Definition of Done:**
- QA testet Nutzung und Limitierung  
- Keine unendlichen Re-Rolls möglich  

**Aufwand:** 5 Story Points

---

## Persona 3: Tom S. – Der Genre-Fan

### Story 10: Spürbares Progression-System
**Als** Genre-Fan  
**möchte ich**, schnell stärker werden  
**sodass** sich das Spiel belohnend anfühlt.

**Akzeptanzkriterien:**
- Level-Up innerhalb der ersten 60 Sekunden möglich  
- Stärke des Spielers wächst sichtbar  
- Gegner skalieren mit der Zeit  

**Definition of Done:**
- QA bestätigt Progression im Early Game  
- Kein stagnierendes Gameplay  

**Aufwand:** 8 Story Points

---

### Story 11: Konsistenter Pixel-Art Stil
**Als** Genre-Fan  
**möchte ich**, einen konsistenten Pixel-Art Stil erleben  
**sodass** das Spiel visuell stimmig ist.

**Akzeptanzkriterien:**
- Einheitliche Pixelgröße  
- Konsistente Farbpalette  
- Einheitliche Animationen  

**Definition of Done:**
- QA visuelle Prüfung  
- Style Guide eingehalten  

**Aufwand:** 5 Story Points
